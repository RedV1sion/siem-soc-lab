# README.md

# SIEM / SOC Engineering Lab

Hands-on SIEM and SOC engineering lab focused on threat detection, log analysis, incident investigation, and SOC workflows using IBM QRadar, Splunk, and TheHive.

## Technologies Used

* IBM QRadar
* Splunk
* TheHive
* SIEM
* SOC Operations
* SPL Queries
* AQL-style Queries
* Log Analysis
* Threat Detection
* Incident Response

## Skills Demonstrated

* SIEM deployment and configuration
* Threat detection engineering
* Correlation rule development
* Alert triage and investigation
* Log ingestion and parsing
* Dashboard creation
* Incident response workflows
* Security monitoring

## Project Highlights

* Configured Splunk Universal Forwarders for centralized log ingestion
* Created dashboards for real-time monitoring and alert analysis
* Developed custom correlation rules for brute force and suspicious login detection
* Investigated security incidents using SOC methodologies
* Utilized TheHive for incident case management and investigation tracking

---

# detection-rules/brute-force-detection.md

# Brute Force Detection Rule

## Objective

Detect multiple failed login attempts from the same source IP address.

## Detection Logic

* More than 10 failed logins within 5 minutes
* Same source IP
* Multiple usernames targeted

## Severity

High

## MITRE ATT&CK

* T1110 - Brute Force

## Response Actions

* Investigate source IP
* Review authentication logs
* Block malicious IP if confirmed

---

# splunk-queries/failed-logins.spl

index=wineventlog EventCode=4625
| stats count by src_ip, user
| sort - count

---

# qradar-configs/custom-rules.md

# QRadar Custom Rules

## Suspicious Login Activity

Detects excessive failed login attempts followed by successful authentication.

## Rule Conditions

* Multiple failed authentication attempts
* Successful login from same IP
* Time window: 10 minutes

## Rule Action

* Generate offense
* Assign high severity

---

# incident-reports/phishing-incident-report.md

# Phishing Incident Report

## Incident Summary

A phishing email containing a malicious attachment was detected during SOC monitoring.

## Indicators Observed

* Suspicious sender domain
* Malicious attachment
* User reported unusual activity

## Investigation Actions

* Analyzed email headers
* Isolated affected endpoint
* Reviewed firewall and DNS logs

## Outcome

Phishing email was contained before lateral movement occurred.

---

# soc-notes/alert-triage.md

# Alert Triage Notes

## Alert Validation Steps

1. Identify alert source
2. Review affected assets
3. Check severity level
4. Analyze related logs
5. Determine false positive or true positive

## Investigation Workflow

* Initial detection
* Log analysis
* IOC validation
* Escalation if necessary
* Incident documentation

---

# soc-notes/threat-hunting-notes.md

# Threat Hunting Notes

## Common Indicators

* PowerShell execution
* Suspicious outbound connections
* Privilege escalation attempts
* Unusual authentication behavior

## Hunting Techniques

* Analyze failed login spikes
* Search for suspicious parent-child processes
* Review endpoint activity
* Correlate authentication events
