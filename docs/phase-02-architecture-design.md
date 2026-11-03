# Phase 02 — Enterprise SOC Architecture Design

**Status:** IN PROGRESS — RAM, CPU, and SSD verified; Windows and hypervisor inventory pending  
**Branch:** `feature/enterprise-soc-expansion`  
**Baseline:** Phase 01 completed (existing one-host Splunk environment verified)  

## Phase objective
Design a safe, low-cost, reproducible SOC training environment that extends the working single-host Splunk investigation lab to multiple isolated telemetry sources, without overwriting the foundation.

## Verified current environment
- Windows host `NSLightningWave` (exact current hardware resources not yet measured).
- Splunk Enterprise 10.4.3 with valid 10 GB/day Developer Personal License, expiration May 2027.
- Index `soc_lab` successfully searches Windows Security and Sysmon Operational events.
- Last-24-hours validation: 603,330 Sysmon events and 10,226 Security events.
- Saved failed-login alert exists and is enabled; actual firing behavior needs separate validation.
- Classic SOC Authentication Monitoring dashboard is functional with a shared Last 30 days time filter.
- Original `main` branch and `v1.0-foundation` preserved.

## First task — Hardware capacity inventory (no configuration changes)
Record these facts before choosing virtual machines or other security agents:
- [x] Total RAM installed: **40.0 GB DDR4** (39.7 GB usable), ~22.7 GB available during capture.
- [x] CPU: **Intel Core i5-1235U (12th Gen), 10 cores, 12 logical processors**, virtualization enabled.
- [x] Storage: NVMe `Windows-SSD (C:)`, **1.81 TB total, 1.62 TB free** per File Explorer.
- [ ] Windows edition and build.
- [ ] Whether a hypervisor (Hyper-V, VirtualBox, or VMware) is already installed.
- [ ] Whether Windows host can safely run one or more isolated VMs without disrupting Splunk ingestion.

Evidence files (save locally first):
- `screenshots/enterprise/phase-02/01_system_memory.png` — Task Manager > Performance > Memory.
- `screenshots/enterprise/phase-02/02_system_cpu.png` — Task Manager > Performance > CPU.
- `screenshots/enterprise/phase-02/03_storage_capacity.png` — File Explorer > This PC showing C: drive free space and total size (next screenshot).

Local screenshot folder:
`C:\Users\munam\OneDrive\Documents\Cybersecurity-Portfolio\SOC Analyst Investigation Lab\screenshots\enterprise\phase-02\`

## Planned architecture — not yet implemented

```text
        Isolated Windows endpoint(s) / test VM(s)
               | Windows Security logs + Sysmon
               v
   Forwarder / supported collection method (to choose)
               |
               v
   NSLightningWave — Splunk Enterprise
               | Indexes, normalized fields
               v
   SPL detections -> investigations -> dashboards/alerts
```

The final topology, VM counts, collection method, and network isolation design depend on available resources. Avoid adding high-volume telemetry indiscriminately, even with a 10 GB/day license.

## Planned deliverables
- [ ] Hardware/resource inventory with evidence.
- [ ] A clearly labeled actual-versus-proposed architecture diagram.
- [ ] Endpoint/VM and data flow matrix.
- [ ] Network isolation and safe simulation boundaries.
- [ ] Estimated storage/index retention and ingestion budget.
- [ ] Phase 02 acceptance criteria and screenshot evidence.

## Rules for continuation
- Preserve existing `soc_lab`, saved alert, original screenshots, and dashboard.
- Use `feature/enterprise-soc-expansion` for GitHub changes; do not merge into `main` prematurely.
- For every future edited code/config file, provide the complete replacement and exact path.
- Capture screenshots **only when the named milestone appears** and save them under Phase 02.
- Keep the up-to-date resume point in `docs/CURRENT-PROGRESS.md`.


## Storage capacity verified — November 3, 2026
Windows File Explorer screenshot verified local C: SSD capacity **1.81 TB** and free space **1.62 TB**. Filename for Phase 02 evidence: `03_storage_capacity.png` (user instructed to save locally). Together with the previously documented 40 GB DDR4 and i5-1235U 10-core/12-logical CPU, this indicates enough apparent resources for a modest lab. Exact VM count, memory allocation, and disk use remain to be designed after OS/hypervisor inventory. Next evidence: `04_windows_system_about.png` from Settings > System > About, with device identifiers redacted.
