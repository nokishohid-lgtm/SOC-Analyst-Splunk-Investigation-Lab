# SOC Analyst Splunk Investigation Report

**Windows Failed Authentication Detection, Investigation, and Validation**

Prepared by: Noki Shohid
Date: September 2026

---

## Executive Summary

I built and tested a complete SOC analyst workflow for suspicious Windows
authentication activity in an authorized personal Windows 11 lab. I enabled
Windows Security auditing and Sysmon, ingested both into Splunk index
`soc_lab`, generated controlled failed logons against `SOC-Test`, searched
Event ID 4625, and created a threshold detection rule for 5+ failures within
5 minutes.

The detection triggered, the saved alert produced history, and the dashboard
showed activity. I then repeated the test and reproduced the result.

**Core conclusion:** I validated a defensive detection use case for repeated
failed Windows authentication. I did not prove external compromise, credential
theft, lateral movement, or the presence of a real threat actor.

---

## Environment

| Component | Value |
|---|---|
| OS | Windows 11 Pro 25H2 (Build 26200.9278) |
| Host | NSLightningWave |
| Test account | SOC-Test |
| Telemetry | Windows Security Event Log, Sysmon |
| SIEM | Splunk Enterprise |
| Index | `soc_lab` |
| Event | Windows Event ID 4625 |
| MITRE ATT&CK | T1110.001 — Password Guessing |

---

## Detection Question

Can Splunk reliably identify at least five Windows failed authentication events
for a host/user within a five-minute window and provide enough evidence for a
SOC analyst to investigate?

---

## SPL Detection Logic

**Baseline:**
