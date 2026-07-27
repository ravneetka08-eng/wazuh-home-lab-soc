# SQL Injection Attack

## Objective

The objective of this exercise was to simulate a SQL Injection attack against the Damn Vulnerable Web Application (DVWA) and investigate how Wazuh detects malicious web requests through Apache log monitoring.

This exercise demonstrates how vulnerable web applications can be exploited through unsanitized user input and how Security Information and Event Management (SIEM) solutions can detect and investigate these attacks using centralized log collection.

---

# Background

SQL Injection (SQLi) is one of the most common web application vulnerabilities.

It occurs when user input is directly incorporated into SQL queries without proper validation or parameterization.

Instead of treating the input as data, the database interprets it as SQL commands.

Successful SQL Injection attacks may allow attackers to:

- Bypass authentication
- Read sensitive database information
- Modify records
- Delete data
- Escalate privileges
- Execute administrative database commands

DVWA intentionally contains this vulnerability for educational purposes.

---

# Lab Environment

| Component | Purpose |
|-----------|---------|
| Kali Linux | Attacker Machine |
| Ubuntu DVWA | Vulnerable Web Application |
| Apache2 | Web Server |
| Wazuh Agent | Endpoint Monitoring |
| Wazuh Manager | SIEM |
| Wazuh Dashboard | Security Investigation |

---

# Attack Workflow

```

Kali Linux

↓

DVWA SQL Injection Module

↓

Apache Web Server

↓

Apache Access Log

↓

Wazuh Agent

↓

Wazuh Manager

↓

Detection Rule 31164

↓

Dashboard Alert

```

---

# Attack Procedure

## Step 1

Login to DVWA.

---

## Step 2

Navigate to

```

DVWA → SQL Injection

```

---

## Step 3

Enter the following payload into the User ID field:

```

'1'

```

Alternative payloads tested included:

```

' OR '1'='1

```

and

```

'1'

```

---

## Step 4

Submit the request.

DVWA processed the request and generated an HTTP request containing the SQL Injection payload.

---

# Apache Log Evidence

Apache recorded the request inside:

```

/var/log/apache2/other_vhosts_access.log

```

Example log entry:

```

GET /DVWA/vulnerabilities/sqli/?id=%271%27&Submit=Submit HTTP/1.1

```

The log captured:

- Timestamp
- Source IP
- HTTP Method
- Requested URL
- SQL Injection payload
- User Agent

---

# Wazuh Detection

The Wazuh Agent continuously monitored Apache logs and forwarded them to the Wazuh Manager.

The built-in rule engine detected the malicious request.

Alert Details

Rule ID

```

31164

```

Description

```

SQL Injection attempt

```

Severity

```

6

```

---

# Dashboard Investigation

The alert appeared within the Wazuh Dashboard.

Information available included:

- Timestamp
- Source IP
- Target Agent
- Rule ID
- Rule Description
- Severity Level
- Complete Apache Request
- Log Source

This confirmed successful end-to-end detection.

---

# Investigation Process

The attack was investigated by:

- Reviewing Apache access logs
- Verifying Wazuh log collection
- Confirming Rule 31164 triggered
- Reviewing Security Events
- Analysing the request URL
- Identifying the attacking IP address

---

# MITRE ATT&CK Mapping

| Technique | ID |
|-----------|----|
| Exploit Public-Facing Application | T1190 |

---

# Security Recommendations

SQL Injection can be prevented by:

- Parameterized queries
- Prepared statements
- Input validation
- Least privilege database accounts
- Stored procedures
- Web Application Firewalls (WAF)
- Continuous log monitoring

---

# Skills Demonstrated

This exercise demonstrated practical experience with:

- SQL Injection testing
- Apache log analysis
- SIEM investigation
- Detection engineering
- Threat hunting
- Wazuh Dashboard analysis
- Web application security

---

# Lessons Learned

This exercise demonstrated how SQL Injection attempts can be successfully detected through Apache log monitoring and Wazuh's built-in detection rules.

By investigating both raw web server logs and SIEM alerts, the attack lifecycle could be reconstructed from initial exploitation to alert generation. This highlights the importance of centralized logging and rule-based detection for identifying web application attacks.
