# Mwalika - Stage 1 Pitch Overview

This document provides an overview of the pitch for stage 1. Including parts of the script and what is expected on each slide during the presentation, this document is written as a "screenplay" for the presentation, with notes on what should be said and shown on each slide.

## Opening + Problem Statement (1.5 mins)

<!-- Opening -->

> **Slide 1**: Title slide with tagline "Guiding every Kenyan through the digital nation"

Hello everyone, my name is Alvin Karanja, and I’m the creator of Mwalika.

Kenya has made huge progress digitising government services through the eCitizen platform, but there is a problem.

**Access to digital services does not mean citizens can actually use them.**

<!-- Problem -->

> **Slide 2**: Problem statement with key statistics and visuals showing the challenges of digital government services in Kenya.
> Key Statistics:
>
> - 47% of Kenyans have basic digital literacy, with only 30% able to complete online forms without assistance.
> - Cybercafes charge up to KES 1000 per service
> - 80% of the population has access to a smartphone, but many still struggle with digital services.

According to the Kenya National Bureau of Statistics, only 47% of Kenyans have basic digital literacy, and only 30% can complete online forms without assistance.

In reality, millions of citizens rely on cybercafés just to access basic government services.

These intermediaries often charge up to 1000 shillings per service, creating unnecessary costs and exposing citizens to fraud and identity theft.

> **Slide 3**: Slide title showing 'Access ≠ Usability' with short text describing user challenges with government services:
>
> - Complex interfaces
> - Unclear instructions
> - Lack of support

And yet, 80% of Kenyans already have smartphones.

The issue isn’t connectivity, the issue is usability.

Many digital government platforms are difficult to navigate, instructions are unclear, and citizens often have no support when something goes wrong.

I want to ask you judges, how can we expect citizens to benefit from digital government services if they can't even access them? Is it fair for more than half of the population to be left behind in the digital nation? To struggle to access basic services?

No, I believe that all Kenyan citizens should have equal access to the services offered by the government. That is the problem Mwalika was built to solve.

<!-- Solution -->

## Solution Overview (1 mins)

> **Slide 4**: Slide showing Mwalika assets such as landing page, app screenshots, and logo in the center.

Mwalika is an AI-powered digital guide for government services.

Instead of forcing citizens to navigate complex websites, they can simply ask questions in natural language.

Behind the scenes, Mwalika uses modern LLMs combined with a structured knowledge graph of **all** the government services on the eCitizen platform.

This allows the system to provide accurate, step-by-step guidance, including:

- Information on which agency is responsible for the service
- and what link to follow to access the service

Importantly, Mwalika uses a RAG architecture, meaning responses are grounded in official government data rather than generated guesses.

The result is simple.

No more confusion navigating government websites.
And no more expensive intermediaries.

Just a personal digital guide available to every Kenyan, 24 hours a day.

<!-- Demo -->

## System demo (3 mins)

> **Slide 5**: Slide showing "demo" title and move on the the live demo of the system, have a backup video demo ready in case of technical difficulties.

Rather than just describing Mwalika, let me show you how it works.

Mwalika is publicly available for anyone to use at mwalika.com, and I encourage each of you to try it out after this presentation.

### Landing page

Users first arrive at the Mwalika landing page, which explains how Mwalika helps citizens navigate government services.

The platform supports both English and Swahili, making it accessible to a wider range of users across Kenya.

### Agent interaction

From here, users can open the assistant and simply ask a question.

For example, I can ask Mwalika about the process of registering a new business in Kenya.

```txt
How do I register a new business in Kenya?
```

--- during thinking phase ---

During the thinking phase, the system retrieves relevant government services and compiles a concise explanation addressing the user's query.

The agent uses the knowledge graph to identify the responsible ministry and agency for business registration, and it retrieves the relevant information about the service from the eCitizen data, including links to the correct pages to access the service directly.

--- during response stream ---

We see that the relevant information about registering a business is displayed, the agent notes that the relevant government agency responsible for this service is BRS, and it provides links to the corresponding pages on the eCitizen platform

--- after response ---

Occasionally, the system also prompts users to provide feedback. This allows us to continuously refine and enhance the system over time based on user insights.

--- second query ---

Recently I renewed my driver's license, and hopefully with the prize money from the competition, I can also purchase my first car, so I can ask Mwalika about the process of registering a new vehicle and getting a new license plate. But this time, we will change the language to Swahili to demonstrate the system's multilingual capabilities.

```txt
Je, ninasajilije gari langu jipya na kupata leseni ya udereva?
```

--- during thinking phase ---

Mwalika is able to understand the query in Swahili, and it goes through the same process of retrieving relevant information from the knowledge graph and providing a clear response to the user.

Mwalika is capable of handling code switching, so if a user were to ask a question that contains both English and Swahili, the system would still be able to understand and respond appropriately.

As we can see, Mwalika responds in Swahili, providing the relevant information about the vehicle registration process and the requirements for obtaining a new driver's license.

### Extra features

On the sidebar, I have given users the ability to report issues and provide feedback on their experience.

This feedback is crucial for the continuous improvement of the system, as it allows us to identify and address any issues or areas for enhancement based on real user experiences.

<!-- Security and Sovereignty -->

## Security and Sovereignty (2 mins)

> **Slide 6**: Slide showing overview of security features headers
>
> - Data privacy
> - System security
> - Digital sovereignty
>

Because Mwalika is designed for government services, security and digital sovereignty were core design priorities from the beginning.

The system is built around three principles:

- Privacy by design
- Layered system security
- National data sovereignty

> **Slide 7: Privacy by Design**: Title slide with bullet points describing anonymisation techniques used in the system
>
> - No PII is collected or stored
> - Redaction logic to remove PII from user prompts before processing
> - Data can be permanently deleted upon user request

First, Mwalika does not collect or store any personally identifiable information.

The system includes automatic redaction logic that removes sensitive information from prompts before processing.

Users can also permanently delete their interaction data at any time.

> **Slide 8: System Security**: Slide showing diagram of security layers with bullet points describing each layer
>
> - AWS Web Application Firewall for edge level security
> - Application level security features to monitor and block malicious behaviour

At the infrastructure level, the system uses a multi-layered security model.

Edge-level protection is provided by AWS Web Application Firewall, which blocks malicious traffic before it reaches the application.

Within the application itself, several safeguards are implemented:

- request rate limiting
- abuse detection for malicious input patterns
- behavioural monitoring for unusual activity

> **Slide 9: Behaviour Monitoring**: Title slide with bullet points describing behaviour monitoring features
>
> - Monitoring large volumes of requests
> - Monitoring large input lengths
> - Monitoring for unusual patterns of behaviour

The system actively monitors unusual behaviour patterns, such as large request volumes or abnormal input lengths.

When suspicious activity is detected, the system automatically blocks access at either the IP level or user token level, giving us fine grain control over potential abuse while minimizing disruption to legitimate users.

> **Slide 10: Data Sovereignty**: Slide showing data sovereignty features
>
> - All processing takes place on AWS resources located in Africa
> - All tools have open source alternatives that can be self hosted on local infrastructure if needed

Finally, Mwalika was designed with national data sovereignty in mind.

All processing currently runs on infrastructure located in Africa, with the ability to migrate to Kenyan infrastructure as local cloud regions become available.

All components of the system also offer self-hostable open-source alternatives, ensuring that sensitive government or citizen data never needs to leave sovereign infrastructure once the system is fully deployed.

<!-- National resilience -->

## National Resilience (1 mins)

> **Slide 11: National Resilience**: Slide showing overview of national resilience features
>
> - High availability
> - Real time support to vulnerable citizens during crises
> - Scalability to handle surges in demand during emergencies

Mwalika is not just a convenience tool, it also strengthens the resilience of digital public services.

Government services are most valuable when citizens can access them reliably, especially during periods of high demand or sudden policy changes.

During peak periods, such as tax deadlines or service backlogs, many citizens struggle to get support.

Mwalika can provide consistent, real-time guidance at scale, reducing pressure on manual support channels and helping citizens reach the correct services faster.

Because the system is built on a modular architecture, it can scale to handle increased demand without degrading the user experience.

Even under pressure, Mwalika can continue to provide accurate guidance, ensuring that citizens can access the services they need when they need them most.

<!-- National impact -->

## National Impact (1.5 mins)

> **Slide 12: National Impact**: Slide showing emotive visuals with notes on the potential impact of Mwalika on Kenyan citizens, with a focus on accessibility and equity.
>
> - Improved access to government services for all citizens
> - Reduced reliance on intermediaries and associated costs
> - Increased efficiency and satisfaction with government services

Mwalika was built for the everyday Kenyan citizen.

For the mother trying to obtain a birth certificate for her child.
For the entrepreneur registering their first business.
And for the millions of citizens who simply want government services to be easier to access.

Mwalika has the potential to create a more inclusive digital future for all Kenyans:

1. **Greater digital inclusion**: Enabling citizens with limited digital literacy to access services independently.

2. **Reduced reliance on intermediaries**: This reduces costs for citizens and limits opportunities for fraud or identity misuse.

3. **More efficient public service delivery**: Government systems become easier to use, reducing the need for customer support personnel and administrative burden.

Furthermore, Mwalika will distinguish Kenya as a leader in digital governance and AI innovation in Africa, setting a precedent for other nations to follow and potentially attracting further technological advancements and investments to the country.

<!-- Future vision -->

## Future Vision (1 mins)

> **Slide 13: Future Vision**: Slide showing roadmap for future development of Mwalika, with a focus on expanding capabilities and impact.
>
> - Customer feedback and initial improvements
> - Expansion of features such as voice interaction and proactive notifications
> - Integration with government systems for task completion

But this is only the first step.

Future development would focus on three areas.

1. **Voice-based interaction**: Allowing citizens to speak directly to the system using speech-to-text and text-to-speech capabilities.

2. **Deeper integration with government systems**: Enabling the assistant to guide users through forms in real time and help fill out applications directly within the chat interface.

3. **Agentic task assistance**: Allowing Mwalika to help complete applications and submit requests with appropriate safeguards.

This would completely transform the way citizens interact with government services, and set a new standard for digital governance globally.

<!-- Closing -->

## Closing (1 min)

> **Slide 14: Closing**: Closing slide with tagline "Mwalika - Guiding every Kenyan through the digital nation" and contact information.

In conclusion, Mwalika is not just a government chatbot. It is a guide to government services, a tool for digital inclusion, and a catalyst for national prosperity.

By bridging the gap between citizens and digital government services, Mwalika has the potential to create a more inclusive digital future for all Kenyans.

Thank you for your time, I would now like to open the floor for any questions you may have.

## Q&A

Need the following additional slides prepared for potential questions:

- Main Q&A slide with title "Questions & Answers"
- References slide with links to key references and sources used in the presentation
- Data architecture slide showing the technical architecture of the system for any technical questions that may arise
- Slide detailing the exact checks and measures in place for security
- A slide detailing the WAF rules and configurations in place for edge level security
- Slide explaining knowledge graph and data from ecitizen scrape
