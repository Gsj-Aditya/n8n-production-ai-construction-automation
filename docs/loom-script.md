# Loom Demo Script

Target length: **4–6 minutes**.

## Recording preparation

- Close unrelated applications and browser tabs.
- Use synthetic names and controlled test destinations.
- Zoom the n8n canvas to the section being discussed.
- Keep credentials and Header Auth values hidden.
- Copy the V4 webhook key before recording and use the clipboard-based demo runner.
- Create a fresh event ID for the recorded run.
- Open HubSpot, controlled Gmail, Slack, V4 Data Table, and n8n executions in separate prepared tabs.

## 0:00–0:30 — Problem

> Construction companies receive leads through forms and manually validate, classify, enter, notify, and follow up on them. Urgent work can be missed, retries can create duplicate Deals, and provider failures can silently lose inquiries. I built this n8n system to manage the complete lifecycle reliably.

Show the architecture diagram.

## 0:30–1:05 — Architecture

> An authenticated webhook receives the inquiry. The workflow validates and deduplicates it, uses structured AI extraction, applies deterministic business rules, synchronizes HubSpot, acknowledges the customer, alerts the team, and schedules a controlled follow-up.

Briefly point to the corresponding canvas sections. Do not explain every node.

## 1:05–2:05 — Live inquiry

Run one prepared authenticated synthetic inquiry.

> This is an urgent roof-leak request. The payload includes a stable event ID, customer details, active damage, location, and budget.

Show the HTTP 202 response with inquiry ID. Open the execution and show only these checkpoints:

```text
validation passed
AI output valid
priority urgent
HubSpot synchronized
Gmail sent
Slack sent
follow-up scheduled
```

## 2:05–2:50 — Business outputs

Show the HubSpot Contact and associated Deal.

> The system searches before writing, so retries do not blindly create duplicates. The Deal contains the inquiry ID, classification, priority, summary, budget, and next action.

Show controlled Gmail and Slack messages.

## 2:50–3:25 — Duplicate protection

Submit the same event again.

> The second request returns duplicate and stops before AI and all external providers. This prevents repeat cost and customer communication.

Show the duplicate execution's short node list.

## 3:25–4:20 — Reliability

Show a stored dead letter and Error Handler execution.

> Expected provider failures use three retries and normalized fallback. Unexpected crashes invoke a separate Error Trigger workflow. The handler classifies the failure, links it to the inquiry, stores a dead letter, and alerts operations.

Show the resolved Slack-only recovery.

> Recovery is bounded. This incident retried only Slack; it did not rerun Gmail, AI, or CRM.

## 4:20–4:50 — Observability

Show Operations Health and a correlation trace.

> Operators can see backlog, unresolved errors, overdue follow-ups, slow executions, and trace one inquiry through its execution and recovery history.

## 4:50–5:15 — Close

> This project demonstrates how I approach client automation: clarify the business rules, control side effects, validate AI output, make failures visible, and provide a system that can be operated and handed over—not only a workflow that works once.

End on the architecture or README, not the full canvas.

## Avoid in the recording

- Reading code line by line
- Touring all nodes
- Showing credentials or secrets
- Spending time on Docker commands
- Claiming universal production readiness
- Showing client-like personal data
- Leaving test failures unexplained
