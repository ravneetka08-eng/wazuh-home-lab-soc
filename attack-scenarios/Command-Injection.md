# Command Injection

## Objective

To exploit a command injection vulnerability in DVWA and investigate how command execution attempts appear in system and web logs.

---

# Lab Setup

Attacker

- Kali Linux

Target

- Ubuntu DVWA

Monitoring

- Wazuh SIEM

---

# Attack Description

Command Injection occurs when user input is passed directly to a system shell.

An attacker can execute arbitrary operating system commands.

---

# Payload

```
127.0.0.1 && whoami
```

---

# Result

The application returned:

```
www-data
```

This confirmed that the injected operating system command executed successfully.

---

# Apache Log

The HTTP request was recorded inside:

```
other_vhosts_access.log
```

---

# Investigation

Verified:

- Apache logs
- Wazuh logs
- Dashboard events

Observed:

The command execution was visible in Apache logs and available for investigation.

---

# MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Command and Scripting Interpreter | T1059 |

---

# Impact

If exploited in production, attackers could:

- Execute system commands
- Download malware
- Read sensitive files
- Escalate privileges

---

# Skills Demonstrated

- Command Injection
- Linux command execution
- Apache log investigation
- Threat hunting
