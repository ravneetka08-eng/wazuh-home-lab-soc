# Cross-Site Scripting (XSS)

## Objective

The objective of this exercise was to simulate a Reflected Cross-Site Scripting (XSS) attack against DVWA and investigate how malicious JavaScript payloads can be identified using Apache logs and Wazuh.

The exercise also included validating a custom Wazuh detection rule using **wazuh-logtest**.

---

# Background

Cross-Site Scripting (XSS) occurs when a web application returns untrusted user input to a user's browser without proper sanitization.

Instead of displaying the input as text, the browser interprets it as executable JavaScript.

There are three common types of XSS:

- Reflected XSS
- Stored XSS
- DOM-based XSS

This lab focused on Reflected XSS.

Possible impacts include:

- Session hijacking
- Cookie theft
- Credential theft
- Browser redirection
- Phishing
- Defacement

---

# Lab Environment

| Component | Purpose |
|-----------|---------|
| Kali Linux | Attacker Machine |
| Ubuntu DVWA | Vulnerable Web Application |
| Apache2 | Web Server |
| Wazuh Agent | Endpoint Monitoring |
| Wazuh Manager | SIEM |
| Wazuh Dashboard | Investigation |

---

# Attack Workflow

```

Kali Linux

↓

DVWA Reflected XSS Module

↓

Apache Web Server

↓

Apache Access Log

↓

Wazuh Agent

↓

Wazuh Manager

↓

Custom Detection Rule

↓

Security Investigation

```

---

# Attack Procedure

## Step 1

Login to DVWA.

---

## Step 2

Navigate to

```

DVWA → XSS (Reflected)

```

---

## Step 3

The application asks:

```

What's your name?

```

Instead of entering normal text, the following payload was supplied:

```html
<script>alert(1)</script>
```

---

# Understanding the Payload

```
<script>
```

Starts a JavaScript block.

```
alert()
```

Displays a browser popup.

```
1
```

A harmless value proving JavaScript execution.

```
</script>
```

Ends the script block.

This payload is commonly used during penetration testing because it safely demonstrates that JavaScript execution is possible.

---

# Result

After clicking Submit, a browser popup displaying

```
1
```

appeared.

This confirmed that:

- User input was not sanitized.
- JavaScript executed successfully.
- The page was vulnerable to Reflected XSS.

---

# Apache Log Evidence

Apache recorded the request inside

```
/var/log/apache2/other_vhosts_access.log
```

Example:

```
GET /DVWA/vulnerabilities/xss_r/?name=%3Cscript%3Ealert%281%29%3C%2Fscript%3E
```

Notice that the payload is URL encoded.

```
<script>
```

becomes

```
%3Cscript%3E
```

---

# Detection Validation

A custom Wazuh detection rule was developed and validated using

```
sudo /var/ossec/bin/wazuh-logtest
```

The Apache log containing the encoded payload was supplied to Logtest.

Result:

```
Rule ID: 100200

Possible XSS attack detected

Alert to be generated
```

This confirmed that the custom rule correctly identified the XSS payload before deployment.

---

# Investigation Process

The investigation included:

- Reviewing Apache access logs
- Searching for encoded script payloads
- Validating the custom rule using wazuh-logtest
- Confirming successful payload execution
- Reviewing the generated detection result

---

# MITRE ATT&CK Mapping

| Technique | ID |
|-----------|----|
| Exploit Public-Facing Application | T1190 |

---

# Security Recommendations

Cross-Site Scripting vulnerabilities can be mitigated through:

- Output encoding
- Input validation
- Content Security Policy (CSP)
- HTTPOnly cookies
- Secure coding practices
- Web Application Firewalls
- Continuous security monitoring

---

# Skills Demonstrated

This exercise demonstrated:

- Reflected XSS exploitation
- URL encoding analysis
- Apache log analysis
- Wazuh custom rule validation
- Detection engineering
- Threat hunting
- Security investigation

---

# Lessons Learned

This exercise demonstrated how a simple JavaScript payload can verify the presence of a Cross-Site Scripting vulnerability.

Although the XSS payload did not generate a built-in Wazuh dashboard alert like the SQL Injection exercise, the custom detection rule was successfully validated using **wazuh-logtest**, demonstrating how detection engineering can be used to extend Wazuh's monitoring capabilities for web application attacks.
