# Upwork Proposal Kit

## Short proposal opening

> I recently built a production-oriented n8n lead workflow with authenticated intake, validation, AI classification, HubSpot Contact/Deal synchronization, Gmail and Slack communication, persistent follow-up, and controlled recovery. Your requirement is similar in the areas of **[insert two exact client requirements]**. I would first confirm **[one important business rule]**, then implement and test the workflow against both success and failure cases.

Do not send this unchanged. Replace the bracketed text with details from the job post.

## Evidence paragraph

> My portfolio example includes duplicate protection, schema validation, provider retries, centralized error handling, dead-letter records, stage-specific reprocessing, and correlation tracing. I can share the short demo and sanitized workflow architecture so you can evaluate how I handle reliability and handoff—not only the happy path.

## Discovery questions

1. What event starts the workflow, and can the source provide a stable event ID?
2. Which fields are required before automatic processing is allowed?
3. Which system is the source of truth for customer and opportunity records?
4. How should existing Contacts and Deals be matched?
5. Which actions are safe to retry, and which could create duplicate side effects?
6. What should happen when AI confidence is low or fields conflict?
7. Which failures require immediate notification versus a retry queue?
8. What human action should suppress an automated reminder?
9. What authentication, data-retention, and access controls are required?
10. What evidence and documentation are needed for acceptance and handoff?

## Suggested specialized profile title

```text
n8n Automation Engineer | AI, APIs, CRM and Reliable Workflows
```

## Suggested overview opening

> I build n8n automations that connect APIs, AI models, CRMs, email, and team tools while controlling duplicates and failure side effects. My data-engineering background helps me design clear data contracts, validation, observability, and recovery paths around the automation—not only connect nodes.

## Suitable job categories

- n8n workflow automation
- HubSpot CRM automation
- AI lead qualification
- API integration
- Email and Slack automation
- webhook and data-processing pipelines
- workflow debugging and reliability
- migration from manual operations to automated systems
