# Phase 01 — Foundation Preservation & Baseline Audit

**Status:** COMPLETE for baseline preservation and existing-environment verification  
**Completed:** November 3, 2026  
**Working branch:** `feature/enterprise-soc-expansion`  
**Preserved original:** `main` and release `v1.0-foundation`

## Scope and definition of complete

This phase inventories and preserves the original Windows failed-authentication Splunk lab, restores usable search licensing, confirms historical and recent data, and verifies the existing saved alert and dashboard. It does **not** represent a full enterprise SOC rollout or a newly executed alert trigger/false-positive validation. Those are later-phase deliverables.

## Baseline preservation

- Original repository: `nokishohid-lgtm/SOC-Analyst-Splunk-Investigation-Lab`.
- Original `main` branch remains unchanged during the expansion.
- Foundation snapshot published: `v1.0-foundation`.
- Development branch: `feature/enterprise-soc-expansion`.
- Progress checkpoint: `docs/CURRENT-PROGRESS.md`.

## Verified environment

| Component | Observation |
|---|---|
| Splunk edition/version | Splunk Enterprise 10.4.3 |
| Build | `4174a2deda5d` |
| Host | `NSLightningWave` |
| Original index | `soc_lab` |
| Current license | Developer Personal License; Enterprise group active; 10 GB/day |
| License state after Windows restart | Valid; no current license alerts or violations |
| Collected sources | Windows Security log, Sysmon Operational |
| Saved alert | Repeated Failed Windows Logins by Username — 5 in 5 Minutes; enabled |
| Dashboard | SOC Authentication Monitoring; Classic; owner admin; functional |

### Recovered licensing issue

The Enterprise trial expired on November 1, 2026 and regular searches were blocked. A new Developer Personal License was installed and shown VALID, but the running service still used Trial even after in-app restart attempts. Diagnostics showed the on-disk `active_group = Enterprise` while live REST returned Trial active. A normal Windows restart loaded the updated Enterprise group and a 10 GB/day pool. No index deletion or Splunk reinstall was required.

## Search verification

The user ran this inventory query with both **All time** and **Last 24 hours**:

```spl
index=soc_lab
| stats count min(_time) as firstSeen max(_time) as lastSeen by host source sourcetype
| convert ctime(firstSeen) ctime(lastSeen)
| sort -count
```

| Time range | Sysmon Operational events | Windows Security events | Total |
|---|---:|---:|---:|
| All time | 22,842,574 | 330,079 | **23,172,653** |
| Last 24 hours | 603,330 | 10,226 | **613,556** |

All data came from host `NSLightningWave`. Recent events were visible on November 3, 2026, confirming recent ingestion as well as successful searches.

A separate **All time** query for `index=soc_lab source="WinEventLog:Security" EventCode=4625` returned **126 matching failed-logon events** (last seen October 25, 2026).

## Dashboard review and correction

The original Classic dashboard was preserved but both panels were empty because each search used a fixed `-24h@h` time boundary, whereas the latest Event ID 4625 observation was October 25. The dashboard was updated to include a shared time picker defaulting to Last 30 days.

The user showed both populated panels after the change:
- Failed Windows Logins Over Time
- Failed Logins by Host

Complete corrected Simple XML is versioned at `dashboards/soc-authentication-monitoring.xml` on the development branch. The original default-time-window behavior was documented; the newly working dashboard was visually verified.

## Published evidence — verified on GitHub

Directory: `screenshots/enterprise/phase-01/`

- `17_splunk_historical_ingestion_restored.png`
- `18_splunk_recent_ingestion_check.png`
- `19_splunk_existing_alerts_audit.png`
- `22_event4625_baseline_presence.png`
- `24_splunk_authentication_dashboard_30d.png`

All five files were directly verified as present on the expansion branch. Screenshot 13, which includes a personal email in the license banner, was intentionally **not** published; the raw license file and XML are never evidence for a public repository.

## Acceptance criteria

- [x] Original foundation release and branch preserved.
- [x] Enterprise Developer license active with usable search.
- [x] Historical and last-24-hours telemetry verified.
- [x] Original enabled saved alert present.
- [x] Event ID 4625 historical data confirmed.
- [x] Dashboard displays expected historical results after time-range correction.
- [x] Five selected screenshots published on enterprise branch.
- [x] Dashboard XML and progress checkpoint tracked on enterprise branch.

## Explicitly deferred work

The saved alert's status is **Enabled**, but current firing behavior, notification action, threshold tuning, and false-positive handling have not been retested in this phase. Multi-endpoint onboarding, retention/capacity analysis, richer detection engineering, incident workflows, and enterprise architecture implementation also remain for future phases.

## Next

Start `docs/phase-02-architecture-design.md` with an actual hardware inventory (RAM, CPU, free disk capacity) before deciding on virtual machines or additional agents.
