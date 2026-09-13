# SPL Detection Queries

Numbered SPL queries used in the SOC Analyst Splunk Investigation Lab.

| File | Purpose |
|---|---|
| `01-basic-event-search.spl` | Raw Event ID 4625 search |
| `02-host-count.spl` | Count failed logons per host |
| `03-five-minute-threshold.spl` | 5+ failures in 5 minutes (baseline detection) |
| `04-username-aware-detection.spl` | Adds parsed username grouping |
| `05-rolling-validation.spl` | Rolling 5-minute window for validation |

All queries target `index=soc_lab`.
