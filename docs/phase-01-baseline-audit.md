# Phase 01 — Existing SOC Lab Baseline Audit

**Project:** Enterprise Splunk SOC & Detection Engineering (expanding an existing lab)  
**Status:** IN PROGRESS — offline baseline documented, live data audit blocked by licensing  
**Date:** November 2, 2026 (Eastern time)  
**Working branch:** `feature/enterprise-soc-expansion`  
**Preserved original:** `main`, release `v1.0-foundation`

## Purpose

Preserve the original completed Windows authentication investigation and establish verified conditions before expanding the lab. This audit separates documented historical results from current observations and unverified capabilities.

## Original completed foundation (according to repository README)

- Windows 11 Pro 25H2 (build 26200.9278) host `NSLightningWave`.
- Splunk Enterprise index `soc_lab` collecting Windows Security logs and Sysmon telemetry.
- Safe lab test account `SOC-Test`.
- Event ID 4625 detection: at least 5 failed logons per five-minute window.
- Saved alert, authentication dashboard, MITRE ATT&CK T1110.001 mapping.
- Positive test reproduced; negative single-failure test did not meet threshold.
- Source IP `::1` was loopback; no real adversary or compromise was claimed.
- Original incident report, SPL queries and numbered screenshots exist on `main`.

These represent **previously documented lab outcomes**, not necessarily currently operational detections.

## Repository preservation — verified

- GitHub repository: `nokishohid-lgtm/SOC-Analyst-Splunk-Investigation-Lab`.
- Default and original branch: `main` (left unchanged).
- Published original release: `v1.0-foundation` (November 2, 2026 ET).
- Expansion branch: `feature/enterprise-soc-expansion`.
- Phase screenshot folder: `screenshots/enterprise/phase-01/`.
- Progress checkpoint: `docs/CURRENT-PROGRESS.md`.

## Current Splunk environment — user observed

| Item | Observed value | Verification status |
|---|---|---|
| Splunk Web | `http://localhost:8000` | Accessible; Administrator logged in |
| Splunk Enterprise version | `10.4.3` | Verified in About |
| Build | `4174a2deda5d` | Verified in About |
| Server | `NSLightningWave` | Verified in About |
| License group | Trial | Verified on Licensing page |
| Trial expiration | November 1, 2026 10:45:48 PM | Verified on Licensing page |
| Licensed daily volume | 0 MB | As displayed |
| Volume used today | 352 MB | As displayed on November 2 ET |
| Warning count | 6 | As displayed |
| Historical `soc_lab` search | Failed: licensing error in `tstats` | Verified via screenshot |
| Current data ingestion | Unknown | Not measurable until searching is restored |
| Native alerting | Unknown in current state | Must verify after licensing resolved |

The error displayed while running the Phase 01 historical SPL query was:
`Error in 'tstats' command: Your Splunk license expired or you have exceeded your license limit too many times.`

A separate Search History screenshot showed earlier `soc_lab` searches from September 2026; this does **not** establish present retention or ingestion health.

## Licensing remediation — pending

- User registered with the Splunk Developer Program.
- Submitted a Developer License request on November 2, 2026 ET.
- Portal showed: **Your request is under review. Expect an email in 3–5 business days.**
- The request is **not yet approved**. Licensing must not be changed until a valid applicable license is received and its terms reviewed.
- No changes have been made to the index, ingestion settings, original alerts, or original GitHub branch.

## Evidence inventory — local screenshot filenames

Local location: `C:\\Users\\munam\\OneDrive\\Documents\\Cybersecurity-Portfolio\\SOC Analyst Investigation Lab\\screenshots\\enterprise\\phase-01\\`.

- `01_branch_comparison_main.png` — user provided earlier
- `02_branch_comparison_expansion.png` — user provided earlier
- `03_original_repository_baseline.png` — user provided earlier
- `04_foundation_release_published.png` — user provided earlier
- `05_splunk_home_accessible.png` — user provided earlier
- `06_splunk_license_status.png` — user confirmed local save
- `07_splunk_version_about.png` — user confirmed local save
- `08_splunk_historical_ingestion_blocked.png` — user confirmed local save
- `09_splunk_search_history.png` — user confirmed local save
- `11_splunk_developer_license_page.png` — user confirmed local save
- `12_splunk_developer_license_request.png` — save submitted-review confirmation

A missing `10_splunk_developer_registration_confirmed.png` is intentional, not a deficiency: the license-page screenshot already documents successful registration. Local copies have not been independently inspected; sanitize before publishing on GitHub.

## Remaining tasks to complete Phase 01

- [ ] User confirms the submitted-request screenshot is saved locally.
- [ ] Obtain an eligible, valid Splunk license or select and document an appropriate alternative.
- [ ] Re-run the historical SPL telemetry inventory using **All time**.
- [ ] Re-run using **Last 24 hours** and compare current ingestion.
- [ ] Record host/source/sourcetype coverage and any missing events.
- [ ] Record actual alerting capability under selected license.
- [ ] Review and sanitize the Phase 01 screenshots; add necessary evidence to expansion branch.
- [ ] Update this audit and `docs/CURRENT-PROGRESS.md`; mark complete only when verified.

## Safe offline work while request is under review

Proceed to Phase 02 architecture planning as a draft (host inventory, resource limits, isolated networking, event flows). Do not claim that the multi-endpoint design is implemented. Do not delete data or change licensing to bypass the current error.

## Reference: SPL to re-run after licensing restored

```spl
index=soc_lab
| stats count min(_time) as firstSeen max(_time) as lastSeen by host source sourcetype
| convert ctime(firstSeen) ctime(lastSeen)
| sort -count
```

Run once with **All time**, then again with **Last 24 hours**. Capture the actual results separately.
