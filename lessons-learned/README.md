# Lessons Learned

## What I Learned

This project helped me understand the complete SOC investigation workflow from log collection to detection, investigation, documentation, and validation.

I learned how to:

- Identify Windows Security Event ID 4625 for failed login attempts.
- Analyze Windows authentication events in Splunk.
- Write SPL queries for security monitoring.
- Create a detection threshold for repeated failed logins.
- Create Splunk alerts and dashboards.
- Investigate suspicious authentication activity using event evidence.
- Map observed activity to MITRE ATT&CK.
- Recommend security remediation.
- Validate a detection rule using authorized test activity.
- Document findings in an incident report.

## Challenges

One challenge was identifying the correct Windows and Splunk fields for username, source information, failure reason, and logon activity.

I also learned that SPL detection logic may need to be adjusted depending on how Windows event fields are extracted and normalized in Splunk.

## Key Takeaway

Detecting suspicious activity is only the beginning of a SOC investigation.

A SOC analyst must also:

- Review the evidence.
- Understand the context.
- Assess the potential risk.
- Document the findings.
- Recommend remediation.
- Validate that the detection works correctly.

## Future Improvements

In a future version of this project, I would improve the detection by including:

- Username
- Source IP address
- Logon type
- Failure reason

I would also test additional authentication scenarios and tune the detection threshold to reduce false positives.
