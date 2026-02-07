# Amani Rashid (KRA) Stakeholder Meeting Notes

**Date:** February 2026  
**Attendee:** Amani Rashid  
**Organisation:** Kenya Revenue Authority (KRA)  
**Role:** Cyber Security Analyst  

## Objectives of the Meeting

- Amani is a cyber security analyst at KRA.
- For my stakeholder engagement, he fits into the category of government technical/policy stakeholder.
- The objective is to ensure the project is aligned with government priorities and regulatory frameworks, and to validate the cyber security and data governance assumptions behind the Mwalika platform.

## Questions and Answers

### General Government Tech and Policy Questions

1. What programming languages, frameworks, and architectural patterns are currently used for KRA digital services, particularly for APIs exposed via the eCitizen platform? Do you have visibility into the technology stacks used by other major government digital services?

   **Answer:**  
   Specific internal technology stacks, programming languages, and architectural patterns were not disclosed. This indicates that such details are either not publicly shared or vary across systems and agencies. From a project perspective, this reinforces the need to design Mwalika as an adjacent system that does not rely on assumptions about internal government implementations.

2. How are KRA digital services hosted and operated today?  
   Specifically, are systems primarily cloud-hosted (e.g. Azure, AWS, GCP), on-premises within KRA infrastructure, or a hybrid model?  
   Is this approach consistent across other government agencies?

   **Answer:**  
   Detailed hosting models were not discussed. The absence of a clear, standardised hosting answer suggests that hosting approaches may vary and are governed internally. This further supports avoiding tight coupling or dependency on internal infrastructure assumptions when designing external or adjacent systems.

3. Are there existing API exposure or integration policies that govern how third-party or adjacent systems may interact with KRA services?  
   Are similar policies applied uniformly across other government digital platforms?

   **Answer:**  
   No specific API exposure or third-party integration policies were shared. This implies that any interaction with KRA systems is highly controlled, case-specific, and subject to internal governance rather than open or standardised integration mechanisms.

---

### Data Security and Data Governance Questions

1. What are the primary cybersecurity standards, frameworks, or internal protocols that KRA follows to protect sensitive taxpayer and financial data?

   **Answer:**  
   KRA is mandated to comply with the Kenya Data Protection Act and is an ISO 27001-certified organisation. In addition to these external standards, KRA maintains internal policies and controls to safeguard taxpayer and citizen data.

2. From a data sovereignty and security perspective, would using self-hosted, open-source large language models materially reduce risk compared to using externally hosted AI APIs from providers such as OpenAI or Google?

   **Answer:**  
   Yes. In accordance with the Kenya Data Protection Act, Kenyan data must not be exposed to external AI engines. Using externally hosted AI APIs would introduce unacceptable data exposure and compliance risk. Self-hosted, open-source models materially reduce this risk by ensuring full control over data processing and storage.

3. Are there formal government or inter-agency policies regarding data residency that apply to KRA systems?  
   For example, are there requirements that taxpayer or citizen data must remain within national borders at all times?

   **Answer:**  
   While specific policy documents were not referenced, KRA’s obligations under the Data Protection Act imply strong data residency and sovereignty requirements. Sensitive taxpayer and citizen data is expected to remain within controlled, compliant environments and not be transmitted to external or foreign systems without clear legal basis.

---

### Threat Modelling and Risk Questions

1. From your experience, what are the most likely threat vectors or abuse scenarios you would anticipate from an AI-assisted system integrated with KRA services?

   **Answer:**  
   The primary concern is data confidentiality and exposure of sensitive taxpayer information. Any AI-assisted system introduces risk if it allows uncontrolled data access, leakage to third parties, or insufficient governance over how data is processed and retained.

2. Does KRA currently have internal guidance, policies, or position papers regarding the use of AI or automated systems that interact with its digital services?  
   Are you aware of similar policies within other government agencies?

   **Answer:**  
   No explicit AI-specific policies were discussed. In the absence of dedicated AI frameworks, existing data protection and cybersecurity laws serve as the governing baseline for evaluating AI and automation systems.

3. In your view, what would constitute the minimum security, compliance, and governance requirements for an AI system to be permitted to interact with KRA services, even in a limited or pilot capacity?

   **Answer:**  
   At minimum, the system would need to demonstrate strict compliance with the Data Protection Act, alignment with ISO 27001 principles, strong data confidentiality guarantees, and clear governance over data access, processing, and retention.

---

### General and Strategic Questions

1. From a personal and professional standpoint, what assurances, controls, or safeguards would you need to see in place to be comfortable with an AI system interacting with KRA services?

   **Answer:**  
   The system must demonstrably protect data confidentiality, comply fully with Kenyan data protection laws, and operate within well-defined security and governance controls. Efficiency gains from AI are valuable, but only if these safeguards are non-negotiable.

---

## General Notes (Pitch-Relevant Takeaways)

- Validated that **self-hosted AI models are effectively the only viable option** for systems interacting with KRA-related workflows.
- Confirmed that **external AI APIs (e.g. OpenAI, Google)** introduce unacceptable compliance and data sovereignty risks under the Kenya Data Protection Act.
- Reinforced that **data protection and governance, not AI capability, are the primary gating factors** for government adoption.
- Demonstrated that the absence of explicit AI policy defaults institutions to **conservative, law-first interpretations**, making external data exposure a non-starter.
- Validated the decision to position Mwalika as an **adjacent, assistive system** rather than a deeply integrated one.
- Supports a strong differentiation narrative: projects relying on externally hosted AI models are **structurally misaligned** with KRA and broader government compliance requirements.
- Confirms that ISO 27001 alignment is a **baseline expectation**, not a competitive advantage, for any serious government-facing system.
- Provides credible stakeholder-backed justification for prioritising **digital sovereignty, auditability, and controlled infrastructure** over rapid integration or automation.
