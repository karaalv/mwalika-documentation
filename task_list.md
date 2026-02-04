# Mwalika High Level Task List

## Overview

- This document defines the high-level execution order for completing the Mwalika project. It exists to guide sequencing and dependency management rather than to track individual work items.
- A more granular, itemised task breakdown is managed within the `Mwalika` GitHub Project, which is used to track individual issues, progress, and status.
- This task list specifically covers **Phase 2: Development and Testing**, as defined in the [project roadmap](roadmap.md).
- For architectural detail and system composition, refer to the [System Architecture Plan](./architecture/system_architecture_plan.md).
- For a full description of scope, inclusions, exclusions, and MVP boundaries, refer to the [Mwalika MVP Scope](./research/proposed_solution_scope.md) document.
- This document is intentionally concise but sufficiently descriptive to preserve execution intent when revisited later.

## Project Setup

- Each major system component will be developed in its own repository to enforce modularity and separation of concerns.
- This documentation repository serves as the coordination layer, capturing system design decisions, integration points, and execution intent rather than implementation detail.
- The following repositories will be created as part of the initial setup. This list is not exhaustive and may expand as required:
  - `mwalika-agent`  
   Core conversational agent logic, including LLM integration, dialogue management, tool calling, and default agent behaviour.
  - `mwalika-frontend`  
   Web-based client application enabling user interaction with Mwalika.
  - `mwalika-backend`  
   Backend services responsible for session handling, API orchestration, workflow coordination, and integration with storage and AI services.
  - `mwalika-infrastructure`  
   Infrastructure-as-code definitions, deployment configuration, and hosting documentation for all system components.

### Development Environments

- As this is a hackathon-focused MVP, development will be conducted primarily against a single development environment.
- There will be no fully separated staging or production environments. A lightweight test environment will exist solely to support basic end-to-end validation.
- Each repository will include clear local setup instructions covering dependencies, configuration, and environment variables.
- Development will primarily occur on local machines. Cloud resources are used mainly for hosting and final MVP deployment, with selective use during development to validate compatibility.

## General Development Principles

- Testing, documentation, logging, and monitoring are treated as inline responsibilities, not separate phases.
- Every task implicitly includes:
  - relevant unit and integration tests,
  - basic load or stress validation where appropriate,
  - logging and observability hooks,
  - minimal but sufficient documentation.
- This approach prioritises production feasibility and auditability over speed-only implementation.

## Task List

### 1. Agent Context Corpus Aggregation

- Assemble the structured knowledge required for Mwalika to operate credibly.
- Activities include:
  - Collecting publicly available information on Kenyan government services, agencies, and ministries.
  - Aggregating FAQs, service descriptions, and procedural guidance relevant to eCitizen.
  - Structuring and normalising this data into formats suitable for retrieval and LLM grounding.
- The primary effort is scraping and cleaning data from the eCitizen platform. This step is non-negotiable and represents the core execution bottleneck.
- The resulting dataset is treated as a standalone structured representation of Kenyan government services and may be reused by other systems if required.

#### 1.1 Deliverables

- A structured, queryable dataset covering Kenyan government services.
- Documentation describing data sources, scraping methodology, and preprocessing steps.
- A summary outlining dataset coverage, known gaps, and limitations.
- Completion of this task unblocks core agent development.

---

### 2. Core Agent Functionality Implementation

- Establish the baseline conversational intelligence of the Mwalika agent.
- Scope includes:
  - Integrating the LLM with the context corpus for grounded response generation.
  - Implementing dialogue management, including clarification, confirmation, and assumption handling.
  - Defining and enforcing default agent behaviour.
- Initial implementation focuses exclusively on text-based interaction.
- Cloud-hosted databases and AI services are used initially for speed and reliability and are configured to allow later replacement with self-hosted alternatives.
- Cloud services remain available as a fallback even if self-hosted components are introduced.

#### 2.1 Deliverables

- A functional conversational agent capable of service discovery and general government QnA.
- Verified integration with the structured context corpus.
- Architecture documentation covering agent flow, LLM usage, and dialogue behaviour.
- Test cases validating correctness and robustness across representative queries.

---

### 3. Client Application Development

- Deliver the primary user-facing interface for Mwalika.
- Scope includes:
  - Building a web-based chat interface that is simple, accessible, and resilient.
  - Integrating the frontend with backend services for real-time communication.
  - Completing all required eCitizen client forks and Mwalika-specific UI surfaces.
  - The client initially supports text-only interaction.
- All service discovery links are live and route users to official eCitizen pages.
- UX and agent behaviour are iterated together to optimise clarity, trust, and perceived intelligence.

#### 3.1 Deliverables

- A functional web client supporting real-time interaction with the Mwalika agent.
- Stable frontend-backend integration.
- Documentation describing frontend structure and integration points.

---

### 4. Extended Agent Capabilities, Voice and Language Support

- Introduce accessibility-critical capabilities rather than optional enhancements.
- Scope includes:
  - Voice input and output via speech-to-text and text-to-speech.
  - Full Swahili language support for both text and voice interactions.
  - Mandatory on-screen transcription of all voice interactions.
- Implementation spans both frontend and backend.
- Voice support is positioned as a core accessibility feature for users with limited literacy or preference for spoken interaction.
- On-device transcription and audio handling are used where possible to improve accessibility and robustness.

#### 4.1 Deliverables

- Voice-enabled Mwalika agent supporting English and Swahili.
- Transparent text transcripts for all voice interactions.
- Documentation covering voice and multilingual implementation details.
- Test results validating reliability and usability of voice interactions.

---

### 5. Mock Workflow Development for Simulated Task Execution

- Demonstrate agentic task execution using simulated workflows for high-impact services.
- Scope includes:
  - Defining step-by-step mock workflows for selected government services.
  - Implementing workflows as isolated, modular components.
  - Integrating workflows with the agent and client UI.
- All workflows are explicitly labelled as simulations.
- Service discovery and general QnA act as a functional baseline if workflow execution must be deprioritised.

#### 5.1 Deliverables

- Working mock workflows for selected services.
- Integrated agent and UI support for simulated execution.
- Documentation describing workflow design and constraints.
- Tests validating end-to-end user guidance through workflows.

> Note: If time constraints arise, priority is given to service discovery and information access. Workflow execution may be selectively deprioritised or scoped to services aligned with national security themes.

---

### 6. Cloud Deployment and Hosting

- Deploy the system to cloud infrastructure to ensure accessibility and operational credibility.
- Scope includes:
  - Provisioning cloud infrastructure for frontend, backend, and agent services.
  - Establishing basic deployment pipelines.
  - Applying standard security practices.
  - Configuring the system for reasonable horizontal scaling.

#### 6.1 Deliverables

- A publicly accessible deployment of the Mwalika system.
- Deployment and security documentation.
- Performance and accessibility test results.

> Cloud hosting is the primary delivery mechanism for the hackathon MVP. Self-hosted components are treated as stretch goals and feasibility demonstrations rather than strict requirements.

---

### 7. Self Hosted AI Infrastructure Implementation

- Explore and validate a self-hosted AI layer.
- Scope includes:
  - Hosting `gpt-oss-20b` for LLM inference.
  - Self-hosted STT and TTS services.
  - Model orchestration APIs.
  - Integration with the existing agent and client.
- Work proceeds iteratively and may stop at partial proof-of-concept if time constrained.

#### 7.1 Deliverables

- A partially or fully functional self-hosted AI layer.
- Setup and configuration documentation.
- Performance benchmarks and reliability tests.

---

### 8. Self Hosted Data Storage and Retrieval Implementation

- Transition data storage and retrieval away from managed cloud services.
- Scope includes:
  - Self-hosted databases for corpus and application data.
  - Retrieval and indexing pipelines.
  - Security and compliance validation.
- This task may be partially completed depending on available time.

#### 8.1 Deliverables

- Integrated self-hosted storage and retrieval components.
- Documentation and performance validation results.

---

### 9. Final Testing, Validation, and Pitch Preparation

- Consolidate all work into a stable, defensible system.
- Scope includes:
  - Full end-to-end testing across all major features.
  - Performance validation focusing on latency, response time, and uptime.
  - Validation of audit logs, traceability, and transparency mechanisms.
  - Preparation of pitch materials and demo narrative.

#### 9.1 Deliverables

- A stable, demo-ready Mwalika system.
- Comprehensive testing documentation.
- Final pitch slides, scripts, and demo flows.

#### 9.2 Demo Hardening

- Harden the system specifically for live demonstration by:
  - identifying and mitigating failure points,
  - rehearsing demo flows and timing,
  - preparing contingency plans such as pre-recorded fallbacks.
