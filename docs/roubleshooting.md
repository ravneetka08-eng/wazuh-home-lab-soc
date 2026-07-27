# Troubleshooting

## Problems Encountered

### Wazuh Agent Offline

Issue

Agent disconnected from manager.

Resolution

Verified manager IP.

Restarted Wazuh Agent.

Confirmed successful reconnection.

---

### Apache Logs Not Appearing

Issue

SQL Injection alerts were not generated.

Resolution

Verified Apache log monitoring inside ossec.conf.

Restarted Wazuh Agent.

---

### Dashboard Missing Alerts

Issue

XSS events appeared in Apache logs but not on the dashboard.

Resolution

Validated detection using wazuh-logtest.

Confirmed the need for a custom rule.

---

### SSH Connectivity

Issue

SSH communication initially failed.

Resolution

Verified networking.

Checked SSH service.

Confirmed credentials.

---

### Rootcheck Alerts

Observed

Rule 510

Explanation

Normal rootcheck scans identifying suspicious binaries.

---

# Lessons from Troubleshooting

Always verify

- Agent connectivity
- Log ingestion
- Decoder
- Rule
- Dashboard
- Network
