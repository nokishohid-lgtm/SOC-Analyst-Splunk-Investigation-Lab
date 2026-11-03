# Enterprise Splunk SOC — CURRENT PROGRESS

**Repository:** `nokishohid-lgtm/SOC-Analyst-Splunk-Investigation-Lab`  
**Original branch:** `main` — leave untouched  
**Working branch:** `feature/enterprise-soc-expansion`  
**Active phase:** 01/20 — Baseline Preservation and Audit  
**Checkpoint date:** November 2, 2026 (Eastern time)  
**Phase status:** IN PROGRESS — not complete

## Verified by GitHub connection
- [x] Existing repository accessible and original project verified.
- [x] Repository default branch is `main`.
- [x] Original README, screenshots, SPL queries and incident report folders exist.
- [x] New branch `feature/enterprise-soc-expansion` successfully created from `main`.
- [x] Progress checkpoint file added to expansion branch.
- [ ] Baseline release/tag `v1.0-foundation` — not yet created or verified.
- [ ] Screenshot 01 original main branch — user capture pending.
- [ ] Screenshot 02 baseline release — user capture pending.
- [ ] Screenshot 03 expansion branch — user capture pending.
- [ ] Splunk version and license verification — pending.
- [ ] Splunk `soc_lab` historical telemetry search — pending.
- [ ] Splunk `soc_lab` last-24-hours telemetry search — pending.
- [ ] Phase 01 audit document — pending.
- [ ] Screenshot evidence published after sanitization — pending.

## Next exact action for user
1. Open `https://github.com/nokishohid-lgtm/SOC-Analyst-Splunk-Investigation-Lab/tree/main` and confirm the original `main` branch.
2. With the original main file list visible, take a screenshot and save it locally as `screenshots/enterprise/phase-01/01_repository_main_baseline.png`.
3. Open **Releases** → **Draft a new release**. Create tag `v1.0-foundation` from `main`, title `SOC Analyst Splunk Lab — Foundation v1.0`, and publish.
4. When published, save `screenshots/enterprise/phase-01/02_foundation_tag_release.png` and show the screenshot in chat.
5. Do not overwrite or delete any original files on `main`.

## Screenshot location
`Documents/Cybersecurity-Portfolio/SOC-Analyst-Splunk-Investigation-Lab/screenshots/enterprise/phase-01/`

Screenshot timing means **immediately after the required screen is visible**, not a wall-clock appointment. Use `Win + Shift + S`, then explicitly save the PNG into the correct folder. Redact secrets and personal identifiers before GitHub upload.

## Local folder status
Not verified. If the project is not cloned locally, create a project folder at the location above and download or clone the expansion branch when ready.

## Pause / resume
Update this entire file whenever a task is verified or blocked, including last step, test result, screenshot filenames, and next action. Save and commit changes to the expansion branch. Resume with: "Continue from `docs/CURRENT-PROGRESS.md`."

## Limits
The existing README documents previous testing only; current Splunk service, license and ingestion have not yet been rechecked. Do not mark Phase 01 complete until the actual results and evidence have been reviewed.


## Developer License request under review — November 2, 2026 ET
- User captured developer portal notice: "Your request is under review. Expect an email in 3–5 business days."
- Request is not yet approved; wait for Splunk's email before applying a license. Submission confirmation screenshot name: `12_splunk_developer_license_request.png` (user was instructed to save; local-save confirmation not yet received).
- Created `docs/phase-01-baseline-audit.md` on this expansion branch, recording baseline, license-blocked searches, evidence inventory, and Phase 1 remaining tasks.
- Next project action: Begin **Phase 02 architecture design draft** while Phase 01 ingestion-validation remains blocked. Inventory available Windows/VM hardware and network isolation, document planned telemetry flow, and do not configure new ingestion or claim phase 01 complete.
- Do not change license, reinstall Splunk, delete indexes, or merge into `main`.


## Verified installed Developer license — November 2, 2026 ET
- User inspected installed licenses on the NSLightningWave Splunk 10.4.3 server.
- Splunk Developer Personal License is listed as **VALID**, with Enterprise type/stack and 10 GB/day allowance; expiration May 1, 2027 per approval email.
- Original Download Trial remains EXPIRED; this is expected and does not require removal.
- User's previous main Licensing page still showed **Trial license group**, so active group has **not yet been verified changed**.
- **Next action:** Licensing > Change license group > Enterprise license > Save > Restart Now if prompted. Verify main Licensing page shows Enterprise and 10 GB/day; save status-only screenshot `13_splunk_developer_license_installed.png`. Do not publish license file, hashes, or full license details.
- **Following action:** Search & Reporting > All time > execute saved historical `soc_lab` inventory SPL, capture `14_splunk_historical_ingestion_restored.png` on successful results or capture error and troubleshoot.


## License diagnostic checkpoint — November 3, 2026
- Splunk CLI `list licenser-groups` could not be completed because the local `admin` password was rejected; do not repeat password guesses.
- Read-only elevated PowerShell `splunk.exe btool server list --debug | Select-String -Pattern "active_group\\s*="` returned `etc/system/local/server.conf active_group = Enterprise`.
- This confirms the **effective on-disk configuration** is Enterprise, but is not yet proof that the running license manager recognizes the 10 GB allowance or that `soc_lab` search works.
- Installed Developer Personal License was previously shown VALID with 10 GB/day. The stale Licensing page previously showed trial expiration and 0 MB, with past trial warnings.
- Next step: Splunk Web > Settings > Licensing, hard-refresh, inspect active group and allowance, then Search & Reporting > All time run `index=soc_lab | head 5` or the saved baseline inventory SPL; capture resulting success or error. If still blocked, inspect licensing warnings and current license pool rather than reinstall or reset.
- No screenshot of keys or license XML should ever be added to the public repository.


## 2026-11-03: Search still blocked after group configuration change
- Actual Splunk Licensing page still displayed **Trial license group**, expired trial, and **0 MB** daily allowance; installed Developer Enterprise license remained VALID 10 GB.
- Read-only `btool server list --debug` returned `active_group = Enterprise` in local server.conf. This establishes on-disk effective configuration only, **not runtime activation**.
- The actual user test `index=soc_lab | head 5` with **All time** failed with `Error in 'litsearch' command: Your Splunk license expired or you have exceeded your license limit too many times.`
- Screenshot user supplied; save locally as `14_splunk_search_license_verification.png`.
- Next safe diagnostic: test `_internal` licensing logs because license restrictions typically allow internal index searches. Use `index=_internal sourcetype=splunkd ("license" OR "DISABLED_DUE_TO" OR "pool") | sort - _time | head 20 | table _time component log_level _raw` with Last 24 hours. Report error if internal index is blocked too.
- Do not reinstall, delete license files, rerun duplicate uploads, clear license warnings, or repeat restarts.


## 2026-11-03 internal licensing search result (confirmed)
- Last-24-hours Splunk search over `index=_internal sourcetype=splunkd ("license" OR "pool" OR "DISABLED_DUE_TO")` returned **20 events** on the user screenshot.
- Recent `LicenseUsage` lines for `soc_lab` Windows Security and Sysmon sources show `pool=auto_generated_pool_download-trial` and `poolsz=0`. This suggests a zero-capacity trial pool is still being used at runtime, despite `btool server ...` showing `active_group = Enterprise` on disk.
- User to save screenshot locally as `15_splunk_internal_license_diagnostics.png` (save not yet confirmed).
- Next read-only check in Splunk Search & Reporting: `| rest /services/licenser/groups | table title is_active stack_ids`. Inspect whether `Enterprise` or `Trial` reports `is_active=1`. This REST endpoint is in Splunk 10.4 official docs. If a search licensing error occurs, capture error only; do not change settings.
