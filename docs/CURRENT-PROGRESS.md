# Enterprise Splunk SOC — CURRENT PROGRESS

**Last verified:** November 3, 2026 (Eastern time)  
**Repository:** `nokishohid-lgtm/SOC-Analyst-Splunk-Investigation-Lab`  
**Original branch:** `main` (preserved; do not overwrite)  
**Development branch:** `feature/enterprise-soc-expansion`  
**Completed:** Phase 01/20 — Foundation Preservation & Baseline Audit  
**Current:** Phase 02/20 — Architecture Design (PAUSED at SSD capacity evidence)

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


## Phase 02 Memory inventory — November 3, 2026
- User screenshot of Windows Task Manager > Performance > Memory verified **40.0 GB DDR4** installed (39.7 GB usable), **17.0 GB** in use (43%), **22.8 GB** available at capture, memory speed **3200 MT/s**, two of two memory slots used, and **276 MB** hardware reserved.
- Windows Task Manager also showed `Disk 0 (C:)` as NVMe SSD and a `VirtualBox Host-Only` Ethernet adapter, neither of which proves available disk space nor completed VM installations.
- Evidence filename to save locally: `screenshots/enterprise/phase-02/01_system_memory.png`; local save still awaiting confirmation.
- **Next:** Task Manager > Performance > CPU, capture `screenshots/enterprise/phase-02/02_system_cpu.png` showing CPU model, cores, logical processors and virtualization status. Then assess C: disk capacity/free space. Do not assign VM counts until both CPU and storage verified.


## All 20 screenshot directories prepared — November 3, 2026
- Verified the GitHub enterprise expansion branch has `screenshots/enterprise/phase-01/` through `phase-20/`, each tracked via `.gitkeep`. Folder creation is complete **on GitHub only**.
- The user's local Windows `phase-02` folder did not exist, producing File Explorer 'Windows can't find ...phase-02' error. Existing local `phase-01` is the safest anchor for creating remaining folders.
- User instructed to execute a guarded PowerShell command: check actual `...\\screenshots\\enterprise\\phase-01` is a folder; use its parent to create `phase-01` through `phase-20` on OneDrive with `New-Item -ItemType Directory -Force`; open `phase-02` automatically. Do not claim local folders were created until user runs the command.
- Then save existing Task Manager Memory screenshot `01_system_memory.png` and capture CPU screenshot `02_system_cpu.png` inside local `phase-02`. Phase 02 hardware inventory remains in progress.


## CPU specification verified — November 3, 2026
- User supplied and confirmed saved local files `01_system_memory.png` and `02_system_cpu.png` in the Phase 02 screenshot folder.
- Hardware: Intel **Core i5-1235U (12th Gen)**, **10 cores**, **12 logical processors**, **1.30 GHz base speed**, **virtualization enabled**. Task Manager showed **40.0 GB DDR4** (39.7 GB usable) and roughly 22.7 GB available at capture; `Disk 0 (C:)` is an NVMe SSD.
- Next task: File Explorer > This PC, capture visible Local Disk (C:) **free space and total capacity** as `03_storage_capacity.png` inside local `screenshots/enterprise/phase-02/`. Do not decide VM count until available disk space is measured.


## PAUSE CHECKPOINT — November 3, 2026
**User paused intentionally. No Phase 02 installation, configuration changes, or VM creation should be presumed.**

Verified saved locally per user: `screenshots/enterprise/phase-02/01_system_memory.png` and `02_system_cpu.png`. Host `NSLightningWave`: 40 GB DDR4 (~22.7 GB available at capture), Intel Core i5-1235U, 10 cores/12 logical processors, virtualization enabled, NVMe C: SSD (free space UNKNOWN). All `phase-01` through `phase-20` folders were created locally by user and separately verified in GitHub expansion branch.

**NEXT ACTION UPON RESUMING:** Windows File Explorer > This PC > Local Disk (C:) > Properties (if necessary), capture capacity and free-space screen as `03_storage_capacity.png` under `C:\\Users\\munam\\OneDrive\\Documents\\Cybersecurity-Portfolio\\SOC Analyst Investigation Lab\\screenshots\\enterprise\\phase-02\\`. Send screenshot for review.

**Remaining Phase 02 steps (in order):**
1. Save `03_storage_capacity.png`, verify free and total disk space.
2. Verify Windows edition/build (Settings > System > About); save `04_windows_system_about.png` after screen visible, redact device IDs.
3. Verify installed hypervisor and any existing VMs in VirtualBox/Hyper-V without altering settings; save `05_virtualization_inventory.png` if screenshot useful and redacted.
4. Determine conservative VM/resource sizing (RAM/CPU/disk) that protects current Splunk instance; assess telemetry volume/retention.
5. Draft proposed SOC architecture (host, isolated client endpoint(s), log transport, index, dashboard, detection workflow) and network isolation/authorized simulation scope. Distinguish existing vs proposed.
6. Update `docs/phase-02-architecture-design.md` with topology, design tradeoffs, sizing, event flow, phased implementation steps, and acceptance criteria.
7. Verify/sanitize Phase 02 screenshots; upload selected evidence to `screenshots/enterprise/phase-02/` on `feature/enterprise-soc-expansion`; commit documentation and audit results.
8. Mark Phase 02 complete only when planned architecture and evidence are reviewed; Phase 03 implementation follows separately.

Do not reinstall Splunk, change licensing, merge into `main`, or start VM deployment without hardware capacity and isolation plan. Resume with: **Continue Phase 2 from docs/CURRENT-PROGRESS.md; start with screenshot 03.**
