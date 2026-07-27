# Cross-Site Scripting (XSS)

## Objective

The objective of this exercise was to simulate a Reflected Cross-Site Scripting (XSS) attack against DVWA and evaluate how Wazuh processes and detects malicious web requests.

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

Cross-Site Scripting (XSS) occurs when a web application accepts untrusted input and returns it to the browser without proper sanitization.

An attacker can inject JavaScript into a vulnerable page.

Possible impacts include:

- Session hijacking
- Cookie theft
- Credential theft
- Browser redirection
- Defacement

---

# Attack Steps

1. Login to DVWA.
2. Navigate to:

DVWA → XSS (Reflected)

3. Enter the payload:

```html
<script>alert(1)</script>
```

4. Click Submit.

A JavaScript alert box appeared, confirming that the payload executed.

---

# Apache Log Evidence

The request was recorded in:

```
/var/log/apache2/other_vhosts_access.log
```

Example:

```
GET /DVWA/vulnerabilities/xss_r/?name=%3Cscript%3Ealert%281%29%3C%2Fscript%3E
```

---

# Detection Validation

The payload was tested using:

```
sudo /var/ossec/bin/wazuh-logtest
```

Result:

```
Possible XSS attack detected
```

Severity

```
10
```

Status

```
Alert to be generated
```

---

# Investigation

The Apache logs confirmed the request.

The payload successfully executed in DVWA.

The detection logic was validated using Wazuh Logtest.

---

# MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Exploit Public-Facing Application | T1190 |

---

# Skills Demonstrated

- Apache log analysis
- URL encoding analysis
- Wazuh rule testing
- Detection validation
- Detection engineering

---

# Lessons Learned

This exercise demonstrated how Wazuh can identify malicious web requests and how custom detection rules can be validated before deployment.
