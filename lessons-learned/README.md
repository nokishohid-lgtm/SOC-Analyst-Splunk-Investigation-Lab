# Lessons Learned

## Technical Lessons

- Windows Event ID 4625 is useful authentication telemetry, but the surrounding fields are required for meaningful triage.
- SIEM detection is stronger when events are grouped by time, host, and user rather than alerting on every raw event.
- Field parsing matters: the username had to be verified and extracted before it could be added to the detection logic.
- A saved alert and dashboard convert an ad hoc search into an operational SOC workflow.
- Validation is essential — a query that looks correct must be tested with known activity.

## Analytical Lessons

- A suspicious pattern is not the same as confirmed malicious activity.
- Source context changes the conclusion: a loopback source supports a lab explanation, not an external-attack claim.
- Every major statement in an incident report should be supported by evidence.
- The strongest portfolio language separates fact, inference, recommendation, and validation.

## What I Would Improve Next

- Add negative testing so isolated login failures do not trigger the alert.
- Test multiple users and hosts to measure false positives and grouping behavior.
- Tune the alert schedule and time range.
- Add successful-logon correlation (Event ID 4624 after repeated failures).
- Add source-IP enrichment to distinguish loopback from remote.
- Use a dedicated Windows Forwarder or multi-host lab.
- Document and test a remediation control (e.g., account lockout policy).
- Version-control the SPL rule, incident report, and documentation.
