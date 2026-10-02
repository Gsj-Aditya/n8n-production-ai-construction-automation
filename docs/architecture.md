# Architecture and Design Decisions

## Components

| Component | Responsibility |
|---|---|
| V4 main workflow | Authenticated intake, AI, CRM, communication, follow-up |
| Error Handler | Captures unexpected stopped executions |
| Dead-Letter Reprocessor | Reviews and retries the smallest safe boundary |
| Operations Health | Aggregates lifecycle and incident metrics |
| Correlation Trace | Reconstructs one inquiry across execution and recovery |
| Inquiry table | Current business and operational state |
| Dead-letter table | Failure-attempt history and resolution |
| Alert-state table | Incident fingerprint, cooldown, and notification state |

## AI boundary

The LLM extracts facts and classifications. Deterministic workflow rules decide priority, assignment, CRM permissions, pipeline stage, acknowledgment type, and next action. AI output is validated before it can cause CRM side effects.

## Idempotency

`source + source_event_id` creates a stable deduplication key and inquiry ID. Duplicate requests stop before AI or provider calls. HubSpot Deals also store the inquiry ID and are searched before creation, protecting against partial-failure retries.

## Failure boundaries

Expected provider errors use node retries and continue as normalized partial failures. Unexpected stopped executions invoke the central Error Handler. Dead-letter recovery never blindly replays the entire workflow.

## Follow-up control

Wait state is persisted by n8n. When it resumes, the workflow rereads the HubSpot Deal stage. A reminder is sent only when the Deal remains in `New Inquiry`; human progress suppresses it.
