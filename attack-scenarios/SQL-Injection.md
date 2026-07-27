# SQL Injection Attack

## Objective

The objective of this exercise was to simulate a SQL Injection attack against the Damn Vulnerable Web Application (DVWA) and investigate how Wazuh detects malicious HTTP requests through Apache log monitoring.

---

# Lab Setup

Attacker

- Kali Linux

Target

- Ubuntu DVWA

Monitoring

- Wazuh Agent
- Wazuh Manager
- Wazuh Dashboard

---

# Attack Description

SQL Injection occurs when an application accepts untrusted user input and directly includes it in a SQL query without proper validation.

Attackers exploit this weakness to:

- Bypass authentication
- Retrieve database information
- Modify records
- Delete data

DVWA intentionally contains this vulnerability for security training.

---

# Attack Steps

1. Open DVWA.
2. Login.
3. Navigate to

```
DVWA → SQL Injection
```

4. Enter the payload

```
'1'
```

5. Submit the request.

---

# Apache Log Evidence

Example

```
GET /DVWA/vulnerabilities/sqli/?id='1'&Submit=Submit HTTP/1.1
```

Apache recorded the request inside

```
/var/log/apache2/other_vhosts_access.log
```

---

# Wazuh Detection

The Wazuh Agent collected the Apache log and forwarded it to the Wazuh Manager.

The built-in detection engine matched:

Rule ID

```
31164
```

Description

```
SQL injection attempt
```

Severity

```
6
```

---

# Dashboard Investigation

Inside the Wazuh Dashboard the following information was visible:

- Timestamp
- Source IP
- Target Agent
- Rule ID
- Rule Description
- Severity
- Apache Request

This confirmed successful end-to-end detection.

---

# MITRE ATT&CK

| Technique | ID |
|-----------|-----|
| Exploit Public-Facing Application | T1190 |

---

# Detection Flow

Attack

↓

Apache Access Log

↓

Wazuh Agent

↓

Wazuh Manager

↓

Rule 31164

↓

Alert

↓

Dashboard

---

# Outcome

✅ SQL Injection generated

✅ Apache log collected

✅ Wazuh detected attack

✅ Dashboard alert generated

✅ Attack investigated

---

# Lessons Learned

This exercise demonstrated:

- Apache log monitoring
- Wazuh rule processing
- Web attack detection
- Alert investigation
- SOC analyst workflow
