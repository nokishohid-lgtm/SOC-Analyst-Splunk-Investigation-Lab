# SOC Analyst Splunk Investigation Lab

## Project Overview

This project demonstrates a basic SOC analyst investigation workflow using Windows Security Event Logs and Splunk Enterprise.

I generated repeated failed Windows login attempts in an authorized lab environment, detected the activity in Splunk, investigated Windows Event ID 4625, created a detection rule and dashboard, mapped the activity to MITRE ATT&CK, and documented remediation and validation steps.

## Objective

The objective was to detect and investigate repeated failed Windows authentication attempts that could indicate password-guessing or brute-force activity.

## Lab Environment

* Windows 11
* Windows Security Event Logs
* Sysmon
* Splunk Enterprise
* PowerShell
* MITRE ATT&CK

## Investigation Scenario

Repeated failed login attempts were generated against the test account `SOC_TEST`.

Windows recorded the failed authentication attempts as Security Event ID 4625. The events were ingested into Splunk and analyzed to determine whether the activity met the detection threshold.

## Detection Query

```spl
index=soc_lab EventCode=4625
| bin _time span=5m
| stats count by _time host
| where count >= 5
```

The detection identifies hosts with five or more failed Windows login attempts within a five-minute period.

## Findings

The investigation confirmed repeated failed Windows authentication attempts within the configured five-minute detection window.

The activity was generated intentionally in an authorized lab environment, but similar behavior in a production environment could indicate password guessing or brute-force activity.

## MITRE ATT&CK Mapping

* **Tactic:** Credential Access
* **Technique:** T1110 — Brute Force
* **Sub-technique:** T1110.001 — Password Guessing

## Remediation Recommendations

* Enable multi-factor authentication.
* Enforce strong password policies.
* Configure account lockout policies.
* Monitor repeated authentication failures.
* Investigate suspicious source addresses.
* Restrict unnecessary remote access.
* Configure SIEM alerts for authentication anomalies.
* Review user accounts regularly.

## Validation

The detection rule was validated by generating at least five failed login attempts within five minutes and confirming that Splunk successfully identified the activity.

## Evidence

The `screenshots` folder contains evidence collected during the lab, including:

1. Windows lab environment
2. Sysmon configuration
3. Windows logon auditing
4. Splunk environment
5. Sysmon events in Splunk
6. Windows Event ID 4625
7. Failed login events in Splunk
8. Detection query
9. Splunk alert
10. SOC dashboard
11. MITRE ATT&CK mapping
12. Detection validation

## Skills Demonstrated

* SOC investigation
* SIEM monitoring
* Splunk SPL
* Windows Event Log analysis
* Authentication monitoring
* Detection engineering
* Alert creation
* Dashboard creation
* MITRE ATT&CK mapping
* Incident documentation
* Detection validation

## Project Workflow

**Windows Event → Splunk Detection → Alert → Investigation → Evidence → MITRE ATT&CK → Remediation → Validation → Incident Documentation**

## Disclaimer

This project was completed in an authorized personal lab environment for educational and cybersecurity portfolio purposes.
