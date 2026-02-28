# Mwalika Agent — Architecture Overview

**Version:** 1.0.0

## 1. Introduction

Mwalika is a retrieval-augmented generation (RAG) agent built to help users discover Kenyan government services via the eCitizen platform. It operates exclusively over a structured, curated knowledge base derived from publicly available eCitizen data, ensuring responses are accurate, traceable, and grounded in official government information.

## 2. Agent Core

The agent core is the central coordination layer responsible for:

- Orchestrating user interactions and control flow
- Constructing prompts and interfacing with the LLM
- Retrieval and entity resolution
- Response generation
- Tool routing and execution

### Behaviour

The agent follows a standard RAG pattern:

1. Interpret user intent.
2. Retrieve relevant entities from the structured corpus.
3. Generate a response grounded in retrieved context.

Key characteristics:

- Context-aware, retrieval-grounded responses
- Clarifying questions when intent is ambiguous
- Explicit grounding in ministries, agencies, and services
- Accuracy and structured reasoning prioritised over inference

### Tools

The agent exposes two primary retrieval tools:

| Tool              | Purpose                                                                                                |
|-------------------|--------------------------------------------------------------------------------------------------------|
| **Corpus Search** | Retrieves entities and metadata (ministries, departments, agencies, services) relevant to a user query |
| **FAQ Search**    | Searches the curated FAQ dataset for direct answers to common queries                                  |

### Architectural Boundaries

- Does not manage database connections directly
- Does not scrape or mutate corpus data
- Does not access external web resources

## 3. Corpus and Retrieval

### Corpus Scope

The corpus enables resolution of user requests related to Kenyan government services across two retrieval modes:

- **Contextual Retrieval** — structured detail on ministries, departments, agencies, and services
- **Intent Resolution** — mapping natural language queries to the correct service entity

### Corpus Structure

The eCitizen ecosystem follows a strict hierarchy:

```txt
Ministry → Department → Agency → Service
```

The corpus contains approximately **~6,000 entities**. Raw structured data is ~2 MB; embeddings add ~72–120 MB in Qdrant.

### Embedding Model

- Model: `text-embedding-3-large`
- Dimensions: 3072
- Vectors are normalised; cosine similarity is used (equivalent to dot product on normalised vectors)
- The same model is used for both corpus and query embeddings

Each entity is embedded using structured concatenated text:

```txt
Ministry: [Name]
Ministry Description: [Summarised, max 150 tokens]
Department: [Name]
Agency: [Name]
Agency Description: [Summarised, max 150 tokens]
Service: [Name]
```

### FAQs

The FAQ section (~15 entries, ~15 words per answer) is **not indexed in the vector store**. It is passed to the agent deterministically via a tool call during reasoning, avoiding unnecessary indexing overhead.

### Retrieval Algorithm (v1.0)

**Step 1 — Query Synthesis**
The agent synthesises a concise retrieval query from the user message. Non-English queries are translated to English before embedding; responses are translated back if necessary.

**Step 2 — Type Filtering**
The agent filters by entity type based on intent (e.g. service queries filter to `type = service`), reducing retrieval noise.

**Step 3 — Vector Similarity Search**

- Initial retrieval: top 3 results
- If all top 3 scores < $\phi$ → expand to top 5
- If best result < $\gamma$ → ask user for clarification

Threshold values ($\phi$ and $\gamma$) are determined through evaluation.

**Step 4 — Metadata Enhancement**
Entity IDs from retrieval are used to fetch full structured data from MongoDB. Related entities (e.g. parent ministry) are joined at the application layer.

**Step 5 — Response Generation**
The agent generates a response using retrieved embeddings, full entity data, and joined relational metadata, providing deterministic service links and responsible ministry/agency attribution.

## 4. Storage Architecture

The system uses two storage backends with clearly separated responsibilities.

| System | Responsibility |
|--------|---------------|
| **Qdrant** | Vector similarity search only |
| **MongoDB** | Structured entity data and application state |
| **Agent** | Joins relationships and assembles response context |

Embeddings are stored **only in Qdrant**. MongoDB does not store embedding vectors.

### Qdrant

- Single collection: `mwalika_corpus`
- Each item stores a minimal payload:

```typescript
interface CorpusItem {
    id: string;
    vector: number[];
    payload: {
        type: 'ministry' | 'department' | 'agency' | 'service';
        schema_version: string;
        entity_id: string;
    };
}
```

### MongoDB

```txy
mongodb
├── mwalika_corpus        → ministries, departments, agencies, services, faqs
├── chats                 → sessions, memories (chat history)
├── mwalika_identity      → users (anonymous user records)
└── mwalika_security      → user_usage_stats, ip_usage_stats, blocked_entities
```

**Sessions** track active and historical conversations. **Memories** store each message as a separate document (enabling efficient pagination and incremental retrieval), structured as an array of typed content blocks (`text`, `image`, `link`).

**Users** are anonymous:

```typescript
interface AnonymousUser {
    user_id: string;
    language_preference: 'english' | 'swahili';
    created_at: string;
    last_active_at: string;
}
```

Security collections track per-user and per-IP usage stats, token counts, WebSocket connection IDs, and blocked entity records.

### Conventions

- All fields use `snake_case` across MongoDB, Qdrant payloads, and API contracts
- Timestamps stored as ISO 8601 strings (UTC)

## 5. Streaming Architecture

### Overview

Mwalika uses a **WebSocket-based streaming architecture** to deliver agent responses in real time. The system supports token-level streaming, structured content blocks, multi-tab connections, and is designed to scale to a distributed architecture with minimal changes.

### Payload Format

Text content is streamed as **Markdown chunks**:

```json
{
    "type": "text",
    "payload": "The capital of France is **Paris**.",
    "memory_id": "12345678",
    "sequence_number": 1
}
```

Structured content (images, links, action cards) is sent as **NDJSON-style blocks** — self-contained and independently renderable.

Each stream carries a unique `stream.id` and monotonically increasing `stream.seq` for deterministic ordering, duplicate protection, and debug traceability.

### Infrastructure Components

**WebSocketManager** — one per connection:

- Maintains a bounded per-connection message queue
- Enforces single-writer pattern (no concurrent writes)
- Applies backpressure (producers block if client is slow)
- Runs heartbeat loop for liveness detection

**SocketRegistry** — maps `user_id → connection_id → WebSocketManager`:

- Supports multi-tab, multi-device connections
- Concurrency-safe (asyncio.Lock, no locks held during I/O)
- Enables broadcast to user or targeted delivery to a specific connection

**EventBus (InMemoryBus)** — decouples agent execution from transport:

- Agent publishes events to the bus, never calls WebSocketManager directly
- Keeps agent code transport-agnostic
- Designed as a placeholder for future migration to Redis PubSub, Redis Streams, Kafka, or NATS

**EventForwarder** — background task that:

- Consumes events from the EventBus
- Routes to SocketRegistry (targeted or broadcast)
- The only component aware of both systems

All components are instantiated in FastAPI lifespan for clean startup and shutdown.

## 6. Security Architecture

### Threat Model

The dominant threat is **automated abuse and resource exhaustion**, not data exfiltration. Mwalika is a public discovery service handling no sensitive personal data.

Primary risks: API abuse, DDoS, LLM token exhaustion, WebSocket flooding, injection attempts.

### Layered Defence

**Edge Layer (AWS CloudFront + WAF):**

- DDoS mitigation and IP filtering
- Rate-based rules and request inspection
- Early rejection of malicious traffic

**Application Layer:**

- Token-based authentication (usage tracking and abuse prevention)
- `front-end-token` authenticates client server
- `refresh-token` (7-day, HTTP-only cookie) + short-lived `access-token` (5-min, memory-only, Bearer)
- Per-IP and per-token rate limiting
- WebSocket controls: 16KB max message, 50,000 daily token cap per user, 5-min idle timeout

### Data Privacy (KDPA Compliance)

Mwalika acts as Data Controller under the Kenya Data Protection Act, 2019. OpenAI and Sentry act as Data Processors.

Mwalika collects **no PII** — no names, IDs, phone numbers, emails, or financial data. Only operational metadata (IP addresses, token usage) is processed, retained for **7 days of inactivity**, then automatically deleted.

All data in transit is TLS-encrypted (HTTPS/WSS). Data at rest is encrypted via MongoDB Atlas and AWS KMS. Secrets are stored in AWS Secrets Manager. Least-privilege access enforced via AWS IAM.

Cross-border transfers to OpenAI contain no PII (user prompts only). Infrastructure runs in AWS Africa (`af-south-1`).

## 7. Planned Enhancements

- Speech-to-text (STT) and text-to-speech (TTS) integration
- Guardrail enforcement and policy-aware response filtering
- Distributed EventBus (Redis / Kafka / NATS)
- Automated dependency vulnerability scanning
- Container image hardening and security header enforcement (CSP, HSTS)
- Migration to self-hosted LLM infrastructure (eliminating cross-border data transfer risk)
- Expanded audit logging for administrative actions
