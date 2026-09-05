# SPL Queries

This folder contains the Splunk Search Processing Language (SPL) queries used in the SOC Analyst Splunk Investigation Lab.

## Failed Login Detection

The detection query identifies repeated Windows failed login attempts using Security Event ID 4625.

```spl
index=soc_lab EventCode=4625
| bin _time span=5m
| stats count by _time host
| where count >= 5
