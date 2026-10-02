# Upwork Portfolio Case Study

## Title

Production AI Lead Automation with n8n, HubSpot, Gmail, Slack, and Groq

## Short description

Built a production-oriented construction inquiry automation that validates and deduplicates leads, extracts structured project details with AI, creates associated HubSpot Contacts and Deals, sends customer acknowledgments and priority Slack alerts, and controls follow-ups based on live CRM stage.

The system includes provider retries, manual-review fallbacks, centralized unexpected-error handling, dead-letter records, safe stage-specific reprocessing, correlation tracing, operational health metrics, and an authenticated webhook.

## Problem

A construction company can receive urgent, incomplete, duplicate, irrelevant, and high-value inquiries through the same channel. Manual handling delays response and makes CRM quality inconsistent. A basic webhook-to-CRM automation can also create duplicate records or lose leads when an API fails.

## Implementation

- Designed a canonical inquiry contract and validation rules.
- Added deterministic identity and duplicate protection.
- Used Groq structured output for project classification and extraction.
- Kept priority, routing, ownership, and CRM decisions deterministic.
- Implemented HubSpot search-before-write Contact/Deal synchronization.
- Added Gmail acknowledgment, Slack priority alerting, persistent follow-up Wait, and Deal-stage suppression.
- Added centralized Error Trigger handling and linked dead-letter records.
- Built dry-run-first recovery that retries only the failed boundary.
- Added Header Auth, correlation IDs, health metrics, and trace lookup.

## Result

The final system processes a lead from authenticated input through CRM and communication while keeping duplicate and failure side effects controlled. The test matrix covers rejection, manual review, spam, urgent processing, duplicate replay, provider failures, Wait recovery, centralized errors, and safe reprocessing.

## Skills demonstrated

```text
n8n workflow architecture
API integration
HubSpot CRM
Gmail OAuth2
Slack API
LLM structured output
JSON Schema
idempotency
error handling
observability
safe reprocessing
Docker Compose
```

## Suggested Upwork caption

> I designed and tested the full lifecycle rather than only connecting APIs: validation, business rules, duplicate protection, CRM reconciliation, communication, persistent follow-up, failure visibility, and controlled recovery.
