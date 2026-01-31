# Mwalika Proposed Solution and MVP Scope

## Executive Summary

Mwalika is an agentic AI assistant designed to help Kenyan citizens navigate and interact with government services available on the eCitizen platform.

For the MVP, Mwalika delivers three core outcomes:

1. **Guided assistance** for government services, helping users discover the correct service, understand the process, and navigate to the appropriate eCitizen service page using live links.
2. **General information and FAQ-style support** for a broad range of government services, enabling users to ask natural-language questions about any service, agency, or ministry.
3. **Simulated agentic task execution** for a limited set of high-demand services using mock workflows, demonstrating how Mwalika can perform actions on behalf of users without direct integration with government systems.

This document defines the proposed solution, the MVP scope, and the justification for feature prioritisation. It acts as a specification guide for the project. Detailed technical design decisions and implementation details are documented separately in the Technical Design and Architecture documentation.

## Overview

- Mwalika is an agentic AI system designed to assist Kenyan citizens in navigating the eCitizen platform for accessing government services.
- The system functions as a conversational virtual assistant, capable of understanding user queries, providing guidance, and supporting users through service discovery and execution flows.
- The name **Mwalika** is derived from the Swahili word *mwalimu*, meaning teacher or instructor, reflecting the system’s purpose of guiding, supporting, and empowering users.
- A significant proportion of Kenyan citizens are not familiar with AI-driven systems. As such, Mwalika adopts a warm, human-centred identity to demystify the technology and encourage trust and adoption.
- The MVP prioritises clarity, simplicity, and practical usefulness over full automation, ensuring a focused and achievable scope within the hackathon timeline.

## Core Capabilities

### Conversational Assistance

- Mwalika operates as a natural language conversational agent powered by modern large language model (LLM) technology.
- Users can interact with the system using text or voice input, with responses provided in English or Swahili.
- All voice interactions include on-screen text transcriptions to ensure transparency and accessibility.

### Default Agent Behaviour

- By default, Mwalika will:
  - Ask clarifying questions to resolve ambiguity.
  - Confirm assumptions before proceeding with guidance or simulated execution.
  - Collect only the minimum information required to support a given task.
- This behaviour applies to all workflows, and is mandatory before initiating any simulated service execution.

### Government Service Assistance

Mwalika provides three distinct levels of support:

1. **Service Discovery**
   - Identifies relevant government services based on user intent.
   - Explains which agency and ministry are responsible for a given service.
   - Redirects users to the correct live eCitizen service page using official links.

2. **Guided Form Assistance**
    - Explains form sections and required information in plain language.
    - Provides step-by-step guidance for completing applications.
    - For the MVP, all form interactions are simulated using mock data and workflows.

3. **Simulated Agentic Task Execution**
   - Demonstrates how Mwalika can perform tasks on behalf of users using predefined mock flows.
   - No real government APIs or production systems are accessed.

### General Information and FAQs

- Mwalika supports general QnA across government services, agencies, and ministries.
- Responses are based on a curated knowledge base derived from publicly available online resources, including:
  - eCitizen service listings
  - Ministry and agency descriptions
  - Public procedural guidance
- The exact number of services supported will be determined after completion of data collection. While the eCitizen platform states “over 22,000 services”, an actual count will be computed during the scraping process and documented.
- For all informational responses, Mwalika will:
  - Indicate whether guidance is explicit or inferred.
  - Provide links to official sources where applicable.
  - Clearly communicate uncertainty when information is not definitive.

### Personalisation

- Personalisation is limited in scope for the MVP and includes:
  - User name
  - Preferred language
  - County
- No sensitive identifiers are required or stored by default.

## Government Integration Scope

- Direct integration with live government systems is out of scope for the MVP.
- All task execution flows are simulated using mock data and predefined workflows.
- This approach allows realistic demonstrations while avoiding security, regulatory, and coordination constraints associated with live systems.

### Mocked Services for MVP Execution

The following services are implemented as simulated agentic workflows:

- **Kenya Revenue Authority (KRA)**  
  Filing returns for personal income tax (PIT)

- **National Transport and Safety Authority (NTSA)**  
  Renewing a driving licence

- **Business Registration Service (BRS)**  
  Registering a new business name

These services were selected due to their high usage and broad relevance.

### Support for All Other Services

- While only three services support simulated execution, Mwalika provides guided assistance and informational support for all other government services.
- Users can:
  - Ask questions about any service.
  - Understand which agency and ministry are responsible.
  - Navigate directly to the correct eCitizen service page via live links.
- Requirements for non-mocked services are not fully known due to fragmentation and lack of structured public data.
- For these services, Mwalika provides best-effort guidance with clear disclaimers and links to supporting references.

### Audit and Transparency

- Users can view an audit log of their interactions with Mwalika.
- Logs include:
  - Collected user information
  - Guidance provided
  - Simulated actions performed
- Sensitive information is minimised and redacted where appropriate.

## Deployment, Security, and Scalability

### Deployment

- The MVP is deployed as a web-based application accessible on desktop and mobile browsers.
- The system is fully self-hosted on AWS infrastructure.

### Data Sovereignty and Model Hosting

- No external LLM APIs are used.
- All language models, vector databases, and supporting services are self-hosted.
- This ensures control over data, aligns with national data sovereignty principles, and reduces dependency on third-party providers.

### Security

- All data is encrypted in transit using TLS.
- The network flow follows:
  - Client → CloudFront (TLS termination)
  - CloudFront → Origin (TLS-encrypted)
- Additional encryption mechanisms beyond TLS are not implemented for the MVP, as they are unnecessary for the defined scope. However, they are considered in the broader system architecture for future phases.
- Security measures include:
  - Data minimisation and redaction of sensitive information
  - No collection of passwords or one-time codes
  - Adherence to standard web application security best practices

### Scalability

- The system architecture is modular and designed to support future expansion.
- The MVP supports a moderate number of concurrent users suitable for demonstrations and early testing.
- Scalability strategies include:
  - Horizontal and vertical scaling
  - Caching
  - Optimised resource management
- Full scalability implementation is deferred to later phases.

## Feature Summary Tables

### Core Government Assistance Features

| Feature | Description |
|------|------------|
| Conversational Interface | Natural language interaction in English and Swahili via text and voice |
| Service Discovery | Identifies relevant services and responsible agencies |
| Live Service Handoff | Redirects users to official eCitizen service pages |
| Guided Assistance | Step-by-step explanations of service processes |
| General Government QnA | Informational support across ministries, agencies, and services |
| Clarifying Questions | Default agent behaviour to confirm assumptions |
| Audit Log | Transparent record of user interactions and actions |

### Mocked Agentic Execution Features

| Feature | Description |
|------|------------|
| KRA PIT Filing | Simulated tax return filing workflow |
| NTSA Licence Renewal | Simulated driving licence renewal |
| BRS Business Registration | Simulated business name registration |

### Deployment and Platform Features

| Feature | Description |
|------|------------|
| Self-hosted LLMs | No reliance on external AI APIs |
| TLS Encryption | Encrypted data in transit via CloudFront and origin |
| Data Minimisation | Limited data collection and redaction |
| Modular Architecture | Designed for future scaling and integration |
