# Enterprise Splunk SOC — CURRENT PROGRESS

**Last verified:** November 3, 2026 (Eastern time)  
**Repository:** `nokishohid-lgtm/SOC-Analyst-Splunk-Investigation-Lab`  
**Original branch:** `main` (preserved; do not overwrite)  
**Development branch:** `feature/enterprise-soc-expansion`  
**Completed:** Phase 01/20 — Foundation Preservation & Baseline Audit  
**Current:** Phase 02/20 — Architecture Design (hardware inventory is next)

## Phase 01 completion — verified

- [x] Foundation release `v1.0-foundation` preserved.
- [x] Active Splunk Enterprise 10.4.3 Developer License (10 GB/day).
- [x] Splunk host `NSLightningWave`, index `soc_lab`.
- [x] All time: **23,172,653** events (22,842,574 Sysmon, 330,079 Windows Security).
- [x] Last 24 hours: **613,556** events (603,330 Sysmon, 10,226 Windows Security).
- [x] **126** Event ID 4625 failed-login events found in historical data.
- [x] Existing failed-login alert present and **Enabled** (actual firing not re-tested).
- [x] Classic `SOC Authentication Monitoring` dashboard repaired with shared **Last 30 days** picker; two populated charts verified.
- [x] Five sanitized, selected evidence screenshots uploaded and directly verified on GitHub.

**Audit:** `docs/phase-01-baseline-audit.md`  
**Versioned dashboard XML:** `dashboards/soc-authentication-monitoring.xml`  
**Published evidence:** `screenshots/enterprise/phase-01/` files 17, 18, 19, 22, 24.

## Phase 02 — Immediate next step

**Goal:** Design a safe, resource-conscious architecture for expanding the existing single-host SOC lab. Do not install additional VMs, agents, or heavy logging until system capacity is measured.

**Step 1 — Memory screenshot**
1. On Windows press `Ctrl + Shift + Esc` to open Task Manager.
2. Click `Performance` and then `Memory`.
3. Capture a screenshot once total installed RAM is visible.
4. Save locally as `01_system_memory.png` under `screenshots/enterprise/phase-02/`.
5. Share the screenshot in chat for verification.

**Step 2 — CPU screenshot (after memory check)**
Open Task Manager > Performance > CPU and save as `02_system_cpu.png` in the same folder. After that we will assess available storage and plan a feasible isolated topology.

**Phase 02 plan:** `docs/phase-02-architecture-design.md` (created; design not yet implemented).

## Exact local screenshot folder root

`C:\Users\munam\OneDrive\Documents\Cybersecurity-Portfolio\SOC Analyst Investigation Lab\screenshots\enterprise\`

Create `phase-02` if not present. Files on the user's PC and files in GitHub are separate until uploaded.

## Working rules

1. Give the user one precise Windows/GitHub/Splunk action set at a time.
2. Provide complete replacement code for edits, exact filename and destination; never overwrite unrelated foundation files.
3. Explicitly identify when screenshots are needed and exactly where to save them.
4. Never publish license files, raw license XML, passwords, or screenshots with unredacted private data.
5. A phase is complete only when its stated deliverables have been verified.
6. Preserve work on `feature/enterprise-soc-expansion`, avoid a pull request or merge until appropriate.
7. For pauses/resumption: say `Continue from docs/CURRENT-PROGRESS.md`.

## Deferred engineering validations

- Actual scheduled alert triggering/notification and tuning, false-positive analysis, new endpoints, architecture implementation: **not yet verified**. These are later-phase work, not failed Phase 01 baseline criteria.
