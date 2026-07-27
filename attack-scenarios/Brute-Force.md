# Brute Force Attack

## Objective

The objective of this exercise was to simulate a brute force attack against the DVWA login functionality and investigate how authentication attempts are recorded, monitored, and analysed using Wazuh SIEM.

The goal was to understand how repeated authentication attempts appear in web server logs, Linux authentication logs, and the Wazuh Dashboard, and to evaluate how security monitoring can be used to identify password guessing attacks.

---

# Background

A brute force attack is a password guessing technique where an attacker repeatedly attempts different username and password combinations until valid credentials are discovered.

Unlike exploiting software vulnerabilities, brute force attacks exploit weak authentication mechanisms and poor password practices.

Common targets include:

- Web application login pages
- SSH servers
- Remote Desktop Protocol (RDP)
- FTP services
- VPN gateways
- Email services

---

# Lab Environment

| Component | Purpose |
|-----------|---------|
| Kali Linux | Attacker |
| Ubuntu DVWA | Vulnerable Web Application |
| Apache2 | Web Server |
| Wazuh Agent | Endpoint Monitoring |
| Wazuh Manager | SIEM |
| Wazuh Dashboard | Alert Investigation |

---

# Attack Workflow

The attack followed the sequence below.

```
Kali Linux

↓

DVWA Login Page

↓

Repeated Login Attempts

↓

Apache Access Log

↓

Wazuh Agent

↓

Wazuh Manager

↓

Rules Engine

↓

Dashboard Investigation
```

---

# Attack Procedure

## Step 1

Login to DVWA.

---

## Step 2

Navigate to

```
DVWA → Brute Force
```

---

## Step 3

Use a valid username with multiple incorrect passwords.

Example

Username

```
admin
```

Passwords attempted

```
password
123456
admin
letmein
qwerty
```

Each failed attempt generated a new HTTP request.

---

# Log Generation

Every login attempt was recorded by Apache.

Example

```
GET /DVWA/vulnerabilities/brute/?username=admin&password=password&Login=Login
```

The requests were stored inside

```
/var/log/apache2/other_vhosts_access.log
```

---

# Wazuh Monitoring

The Wazuh Agent continuously monitored Apache logs and forwarded them to the Wazuh Manager.

During this project, authentication activity and Apache logs were successfully collected.

Although a dedicated brute force detection rule was not implemented, the collected logs provide sufficient evidence to develop custom correlation rules in the future.

---

# Investigation Process

The investigation consisted of:

1. Reviewing Apache access logs.
2. Confirming repeated login attempts.
3. Verifying that Wazuh ingested the logs.
4. Searching the Wazuh Dashboard for related events.
5. Reviewing timestamps and source IP addresses.

---

# Evidence Collected

Evidence included:

- Apache Access Logs
- Wazuh Security Events
- Agent Information
- Source IP Address
- HTTP Requests
- Authentication Attempts

---

# Detection Opportunities

Indicators that may suggest a brute force attack include:

- Multiple failed login attempts
- High request frequency
- Repeated requests from the same IP address
- Multiple password attempts for the same username
- Authentication failures over a short period

---

# Example Custom Detection Logic

A future custom Wazuh rule could trigger an alert when:

- Five or more failed login attempts
- From the same source IP
- Within one minute

Example rule concept

```
IF

Failed Logins >= 5

AND

Same Source IP

AND

Time Window <= 60 seconds

THEN

Generate High Severity Alert
```

---

# MITRE ATT&CK Mapping

| Technique | ID |
|-----------|----|
| Brute Force | T1110 |

---

# Security Recommendations

To reduce the risk of brute force attacks:

- Implement Multi-Factor Authentication (MFA)
- Enforce strong password policies
- Configure account lockout thresholds
- Implement rate limiting
- Use CAPTCHA after repeated failures
- Monitor authentication logs continuously
- Alert on abnormal login behaviour
- Block malicious IP addresses automatically

---

# Skills Demonstrated

During this exercise the following skills were developed:

- Authentication monitoring
- Apache log analysis
- Linux log analysis
- Wazuh Dashboard investigation
- Threat hunting
- Detection engineering concepts
- Incident investigation
- Security event correlation

---

# Future Improvements

Future enhancements for this lab include:

- Create a custom brute force detection rule
- Configure Active Response to block attacking IP addresses
- Integrate Fail2Ban with Wazuh
- Implement email notifications for repeated login failures
- Correlate web authentication logs with Linux authentication logs
- Generate MITRE ATT&CK dashboards for authentication attacks

---

# Lessons Learned

This exercise demonstrated that brute force attacks generate a predictable pattern of repeated authentication attempts that can be identified through centralized log collection and correlation.

Although a dedicated brute force detection rule was not implemented during this project, the collected evidence provides an excellent foundation for developing custom Wazuh detection rules and automated response mechanisms in future work.
