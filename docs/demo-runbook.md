# Loom Recording Runbook

## Goal

Show that the builder understands the business workflow and reliability boundaries. Do not demonstrate every node.

## Recommended recording

Record the screen at 1080p with a clean desktop. Use the script in `loom-script.md` and target 4–6 minutes.

## Prepared tabs

1. Architecture diagram in GitHub README preview
2. V4 n8n canvas positioned at intake/AI/CRM
3. V4 executions
4. HubSpot Contacts and Deals
5. Controlled Gmail inbox
6. Slack test channel
7. V4 inquiry Data Table
8. Error Handler/dead-letter evidence
9. Operations Health output

## Live demo command

Copy the V4 Header Auth value to the clipboard without showing it. From the private working project, run:

```bash
./scripts/run_v4_loom_demo_from_clipboard.sh
```

The script sends the same synthetic urgent inquiry twice:

```text
First request  -> accepted
Second request -> duplicate
```

The secret is read from the clipboard and never printed. Run the demo fixture only once per recording attempt; change its source event ID before another full attempt.

## What to show

- HTTP accepted response and inquiry ID
- A few named execution checkpoints
- HubSpot Contact and associated Deal
- Controlled Gmail acknowledgment
- Slack urgent alert
- Lifecycle row and correlation ID
- Duplicate execution stopping before AI/providers
- Existing dead-letter/recovery evidence rather than intentionally crashing during the recording

## After recording

- Archive the synthetic Loom Contact and Deal.
- Restore any temporary test interval.
- Confirm V4 remains authenticated and published.
- Confirm the video contains no credential page, token, private clipboard content, personal browser data, or unrelated notification.
- Upload to Loom as view-only and paste the URL into README and Upwork portfolio entry.
