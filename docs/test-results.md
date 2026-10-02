# Verified Test Results

| Scenario | Verified outcome |
|---|---|
| Missing/wrong Header Auth | HTTP 403; no execution or row |
| Correct Header Auth | Successful V4 execution and correlation record |
| Invalid core input | Rejected with five field errors; no stored intake |
| Missing contact | Stored manual review; operations Slack only |
| Spam solicitation | AI classified and filtered; no CRM or communication |
| Urgent qualified inquiry | Contact, associated Deal, Gmail, Slack, and follow-up |
| Duplicate urgent event | Duplicate response; no repeated provider node |
| Existing Deal | Reused without creating another Deal |
| Follow-up send | Wait resumed, Deal rechecked, email sent |
| Follow-up suppression | Deal advanced; reminder suppressed after restart |
| Gmail failure | Error persisted; Slack continued |
| Slack failure | Gmail persisted; Slack error recorded |
| Unexpected Code failure | Error Handler created and linked dead letter |
| Unsafe reprocessing | Workflow-logic error refused without mutation |
| Safe reprocessing | Slack-only retry resolved on attempt one |
| Operations dashboard | Health reasons and attention records matched data |
| Correlation trace | Inquiry, execution, error, and dead-letter history joined |

Detailed internal results are available in the project build documentation. All external test records were synthetic and cleaned from HubSpot after evidence collection.
