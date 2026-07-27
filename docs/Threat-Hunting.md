# Threat Hunting

## Overview

Threat hunting is the proactive process of searching for malicious activity that may not yet have triggered high-confidence alerts.

This project used the Wazuh Dashboard and Linux logs to investigate attack activity generated against DVWA.

---

# Threat Hunting Process

1. Generate attack.
2. Locate Apache log.
3. Verify Wazuh ingestion.
4. Search dashboard.
5. Identify rule.
6. Review source IP.
7. Review request.
8. Investigate timeline.
9. Confirm detection.

---

# Hunts Performed

## SQL Injection

Evidence

Apache access log

Rule

31164

Result

Successfully detected.

---

## Cross-Site Scripting

Evidence

Apache access log

Payload

<script>alert(1)</script>

Validated using

wazuh-logtest

---

## Command Injection

Payload

127.0.0.1 && whoami

Observed

www-data

---

## SSH Activity

Investigated

- sudo
- PAM
- Login events

---

## File Integrity

Investigated

Rootcheck

Syscheck

---

# Tools Used

- Wazuh Dashboard
- grep
- tail
- journalctl
- ossec.log
- alerts.log
