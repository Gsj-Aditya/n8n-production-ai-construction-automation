# Setup and Client Handoff

## Prerequisites

- n8n 2.33.0 or newer
- Groq API credential
- HubSpot service/private-app credential
- Gmail OAuth2 credential with send scope
- Slack bot credential with `chat:write`
- Three n8n Data Tables created from the provided schemas

## Import order

1. Error Handler
2. Main V4 workflow
3. Dead-Letter Reprocessor
4. Operations Health
5. Correlation Trace

## Configuration checklist

1. Create Data Tables from `config/data-tables/`.
2. Select the correct table in every Data Table node.
3. Select Groq, HubSpot, Gmail, Slack, and Header Auth credentials.
4. Replace controlled test email and Slack channel placeholders.
5. Provision HubSpot custom properties and record actual pipeline/stage IDs.
6. Link the Error Handler in the main workflow's Error Workflow setting.
7. Keep every imported workflow inactive during configuration.
8. Run authentication, rejection, manual-review, spam, happy-path, and duplicate tests.
9. Confirm production follow-up intervals.
10. Publish only the workflows intended to run.

## Production controls

- Use HTTPS and a stable `WEBHOOK_URL`.
- Add rate limiting before n8n.
- Keep the webhook secret in a server-side secret store.
- Remove HubSpot schema-write scopes after provisioning.
- Define payload and execution-retention policies.
- Back up the n8n database/volume and test restoration.
- Prefer PostgreSQL and queue mode when concurrency or availability requires it.

## Handoff evidence

Provide the client with:

- architecture and field mapping;
- credential/scope list without secret values;
- test matrix and known limitations;
- recovery and incident runbook;
- deployment and backup procedure;
- sanitized workflow exports.
