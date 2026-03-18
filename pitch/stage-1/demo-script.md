# Mwalika Pitch 1 - Demo Script

## Landing page

Users first arrive at the Mwalika landing page, which explains how Mwalika helps citizens navigate government services.

The platform supports both English and Swahili, making it accessible to a wider range of users across Kenya.

## Agent interaction

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

## Extra features

On the sidebar, I have given users the ability to report issues and provide feedback on their experience.

This feedback is crucial for the continuous improvement of the system, as it allows us to identify and address any issues or areas for enhancement based on real user experiences.

## Whilst transitioning back to slides

Mwalika is publicly available for anyone to use at mwalika.com, and I encourage each of you to try it out after this presentation.