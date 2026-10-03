# Production AI Construction Inquiry Automation

An n8n portfolio project that turns inbound construction inquiries into validated, AI-enriched, traceable CRM opportunities with customer acknowledgment, internal alerts, controlled follow-up, centralized error handling, and safe recovery.

**[Watch the demo on Loom](https://www.loom.com/share/8bb9f5e4262d42f8a14e2481bac17089)** — a walkthrough of the business flow, integrations, duplicate protection, and error recovery.

## Business problem

Construction companies receive inquiries through forms, email, referrals, and phone notes. Staff manually validate details, identify urgent work, create CRM records, notify the right person, acknowledge the customer, and remember follow-ups. This creates several risks:

- urgent damage is missed;
- duplicate submissions create duplicate CRM records;
- incomplete requests are handled inconsistently;
- provider failures silently lose leads;
- reminders continue after a salesperson has acted;
- nobody can quickly trace what happened to one inquiry.

## Solution

```text
Authenticated Webhook
→ Normalize and Validate
→ Generate Identity and Deduplicate
→ Store Intake
→ Structured AI Classification
→ Deterministic Business Rules
→ HubSpot Contact and Deal Synchronization
→ Gmail Acknowledgment
→ Priority-Based Slack Alert
→ Durable Wait
→ HubSpot Stage Recheck
→ Send or Suppress Follow-Up
→ Persist Lifecycle and Operational Status
```

Unexpected crashes invoke a separate Error Trigger workflow. Failed attempts become linked dead letters and can be reviewed through a manual, dry-run-first, stage-bounded reprocessor.

## Architecture

![Architecture of the AI construction inquiry automation](assets/01-architecture.png)

## What I built

- Canonical JSON normalization and validation
- Stable inquiry, deduplication, execution, and correlation identifiers
- Schema-constrained Groq classification with independent validation
- Deterministic priority, ownership, next-action, and CRM rules
- HubSpot Contact search/create/update and associated Deal creation
- Search-before-write protection against duplicate Deals
- Gmail acknowledgment templates and priority-based Slack alerts
- Persistent Wait scheduling with HubSpot stage-based reminder suppression
- Provider retries with normalized partial-failure states
- Central Error Trigger workflow for unexpected crashes
- Dead-letter storage and main-record linking
- Human-controlled, bounded reprocessing that retries only the failed operation
- Operations dashboard, correlation trace, health thresholds, and alert fingerprinting
- Header-authenticated V4 webhook

## Reliability behavior

| Condition | Behavior |
|---|---|
| Missing/incorrect webhook key | Reject before workflow execution |
| Invalid core payload | HTTP 400; no storage or external action |
| Missing contact method | Store for manual review and notify operations |
| Duplicate source event | HTTP 200 duplicate; no repeated side effect |
| Low-confidence/malformed AI | Manual review; no CRM automation |
| Spam/not-a-fit | Store classification; skip CRM and communication |
| HubSpot Contact ambiguity | Stop for manual review instead of guessing |
| Existing Deal | Reuse it instead of creating a duplicate |
| Provider outage | Retry three times, then persist normalized failure |
| Unexpected workflow crash | Error Handler creates and links a dead letter |
| Failed communication recovery | Retry only the failed provider |
| Deal progressed during Wait | Suppress automated follow-up |

## Verified evidence

- Authentication rejection and success paths
- Blocking validation, manual review, spam, urgent, and duplicate routes
- HubSpot Contact–Deal association through API read-back
- Gmail and Slack delivery IDs persisted
- Wait resume, follow-up send, and follow-up suppression
- Controlled Gmail and Slack failures
- Centralized unexpected-error handling
- Unsafe retry refusal and successful Slack-only recovery
- Operations dashboard and correlation trace

See [`docs/03-test-evidence.md`](docs/03-test-evidence.md).

### Portfolio evidence

#### Urgent inquiry classified and routed

![Urgent inquiry business rules](assets/02-successful-inquiry.png)

#### Failed Slack action recovered safely

![Slack-only recovery resolved on the first attempt](assets/03-safe-recovery.png)

## Technology

- n8n 2.33.0 in Docker Compose
- Groq structured output using `openai/gpt-oss-20b`
- HubSpot CRM API
- Gmail OAuth2
- Slack API
- n8n Data Tables
- JSON Schema and deterministic JavaScript rules

## Repository structure

```text
workflows/
  01-main-automation.json
  02-central-error-handler.json
  03-safe-reprocessor.json
  04-operations-health.json
  05-correlation-trace.json

docs/
  01-architecture.md
  02-setup-and-handoff.md
  03-test-evidence.md

config/
  ai/            LLM system prompt and classification boundaries
  schemas/       Inbound and structured AI-output contracts
  data-tables/   Persistent table definitions

examples/        Four representative synthetic inquiry payloads
docker-compose.yml
```

The numbered workflow and document names show the recommended reading/import order.

## Why the AI system prompt is included

[`config/ai/classifier-system-prompt.md`](config/ai/classifier-system-prompt.md) is the instruction sent to Groq before each inquiry. It defines what the model may extract, the allowed classifications and signals, and what it must leave to deterministic workflow rules. Including it lets a reviewer evaluate the AI boundary rather than treating the model call as a black box.

## Running the project

The workflows are inactive templates. Import them, create your own credentials and Data Tables, replace all `CONFIGURE_*` placeholders, link the Error Handler in the main workflow settings, and publish only after completing the setup checklist.

See [`docs/02-setup-and-handoff.md`](docs/02-setup-and-handoff.md).

## Security

- No API keys or live credential IDs are included.
- The intake webhook uses Header Auth.
- Public deployment requires HTTPS and upstream rate limiting.
- A browser form should call a trusted backend that adds the webhook secret server-side.
- HubSpot, Gmail, and Slack should use least-privilege scopes.
- Customer-payload retention must be defined per deployment.

## Scope

The demo runs locally with synthetic inquiry data and a controlled email-recipient override. The repository does not include a hosted endpoint, credentials, or a universal retry policy. Recovery rules must reflect each client's systems and side effects.

## Engineering outcome

```text
input
→ business logic
→ automation
→ integrations
→ output
→ error handling
→ observability
→ safe recovery
```
