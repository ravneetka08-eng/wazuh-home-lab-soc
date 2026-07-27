# Command Injection Attack

## Objective

The objective of this exercise was to exploit a command injection vulnerability in the Damn Vulnerable Web Application (DVWA) and investigate how malicious requests are captured and analysed using Apache logs and Wazuh SIEM.

This exercise demonstrates how unsanitized user input can allow an attacker to execute operating system commands on a web server.

---

# Background

Command Injection is a vulnerability that occurs when an application passes user-supplied input directly to a system shell without proper validation or sanitization.

Instead of treating the input as data, the operating system interprets it as executable commands.

This allows attackers to execute arbitrary operating system commands with the privileges of the web server process.

Potential impacts include:

- Remote Code Execution (RCE)
- Information Disclosure
- File Manipulation
- Downloading Malware
- Installing Backdoors
- Privilege Escalation (if additional vulnerabilities exist)

---

# Lab Environment

| Component | Purpose |
|-----------|---------|
| Kali Linux | Attacker |
| Ubuntu DVWA | Vulnerable Target |
| Apache2 | Web Server |
| Wazuh Agent | Endpoint Monitoring |
| Wazuh Manager | SIEM |
| Wazuh Dashboard | Security Investigation |

---

# Attack Workflow

```
Kali Linux

↓

DVWA Command Injection Module

↓

Apache Web Server

↓

Operating System Shell

↓

Apache Access Log

↓

Wazuh Agent

↓

Wazuh Manager

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
DVWA → Command Injection
```

---

## Step 3

The page requests an IP address to ping.

Instead of supplying only an IP address, the following payload was entered:

```
127.0.0.1 && whoami
```

---

# Understanding the Payload

The payload consists of two parts.

```
127.0.0.1
```

This is a legitimate IP address that the application attempts to ping.

```
&&
```

The logical AND operator.

It instructs Linux to execute the next command after the first command completes successfully.

```
whoami
```

A Linux command that prints the current user executing the process.

---

# Result

DVWA returned:

```
www-data
```

This confirmed that:

- The injected command executed successfully.
- The Apache web server executed commands as the **www-data** user.
- The application was vulnerable to command injection.

---

# Why "www-data"?

Apache does not run as the root user.

Instead, it runs under a restricted service account.

On Ubuntu, this account is typically:

```
www-data
```

This limits the privileges available to the web server and helps reduce the impact of successful attacks.

---

# Apache Log Evidence

The HTTP request was recorded inside:

```
/var/log/apache2/other_vhosts_access.log
```

Example request:

```
GET /DVWA/vulnerabilities/exec/?ip=127.0.0.1&&whoami
```

The Apache logs confirmed that the malicious payload reached the application.

---

# Wazuh Investigation

The Wazuh Agent monitored the Apache logs and forwarded them to the Wazuh Manager.

The investigation involved:

- Reviewing Apache access logs
- Searching Security Events
- Reviewing timestamps
- Verifying source IP addresses
- Confirming successful log ingestion

Although a dedicated command injection detection rule was not implemented, the attack was successfully observed through the collected web logs.

---

# MITRE ATT&CK Mapping

| Technique | ID |
|-----------|----|
| Command and Scripting Interpreter | T1059 |
| Exploit Public-Facing Application | T1190 |

---

# Security Recommendations

Command Injection vulnerabilities can be mitigated by:

- Input validation
- Allow-listing acceptable input
- Avoiding system() and shell_exec()
- Parameterized APIs
- Least privilege execution
- Web Application Firewalls (WAF)
- Runtime monitoring
- Centralized logging

---

# Skills Demonstrated

This exercise demonstrated practical experience with:

- Linux command execution
- Command Injection exploitation
- Apache log analysis
- Threat hunting
- Wazuh investigation
- Web application security
- Incident analysis

---

# Future Improvements

Future enhancements include:

- Develop custom Wazuh command injection rules
- Correlate multiple command execution attempts
- Trigger Active Response
- Integrate Sigma detection rules
- Automatically block malicious IP addresses

---

# Lessons Learned

This exercise demonstrated how vulnerable applications can unintentionally execute operating system commands when user input is not properly validated.

Although only the harmless `whoami` command was executed for educational purposes, the same vulnerability could allow attackers to perform much more serious actions in a real-world environment. The investigation highlighted the importance of centralized log collection, security monitoring, and detection engineering in identifying command injection attempts.
