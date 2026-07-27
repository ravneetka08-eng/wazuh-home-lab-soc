# wazuh-home-lab-soc
Security Operations Center (SOC) Home Lab using Wazuh SIEM, DVWA, Kali Linux and Ubuntu for attack simulation, detection engineering and threat hunting.

# 🛡️ SOC Home Lab – Wazuh SIEM | Detection Engineering | Threat Hunting

![Platform](https://img.shields.io/badge/Platform-VirtualBox-blue)
![OS](https://img.shields.io/badge/Linux-Ubuntu-orange)
![SIEM](https://img.shields.io/badge/SIEM-Wazuh-red)
![Attacker](https://img.shields.io/badge/Attacker-Kali-success)
![Status](https://img.shields.io/badge/Project-In%20Progress-yellow)

---

# Overview

This project demonstrates the design and implementation of a Security Operations Center (SOC) home lab for monitoring, detecting, and investigating cyber attacks using open-source security tools.

The lab simulates realistic attack scenarios against a deliberately vulnerable web application (DVWA) while collecting and analysing security events using Wazuh SIEM. The project focuses on Blue Team operations, detection engineering, log analysis, threat hunting, and incident investigation.

Rather than simply installing security software, this project demonstrates the complete security monitoring lifecycle—from attack generation to log collection, detection, investigation, and response.

---

# Project Objectives

- Build a multi-machine SOC lab
- Deploy a centralized SIEM platform
- Monitor Linux endpoints
- Collect Apache web logs
- Simulate common web attacks
- Investigate alerts
- Develop custom Wazuh detection rules
- Practice threat hunting
- Strengthen Linux administration skills
- Gain practical SOC Analyst experience

---

# Lab Environment

| Machine | Purpose |
|----------|----------|
| Kali Linux | Attacker Machine |
| Ubuntu DVWA | Web Server (Apache + PHP + MariaDB) |
| Ubuntu Wazuh | Wazuh Manager + Dashboard + Indexer |

Virtualization Platform

- VirtualBox

Operating Systems

- Ubuntu Linux
- Kali Linux

---

# Technologies Used

## SIEM

- Wazuh Manager
- Wazuh Dashboard
- Wazuh Indexer
- Wazuh Agent

## Operating Systems

- Ubuntu Linux
- Kali Linux

## Web Technologies

- Apache2
- PHP
- MariaDB
- DVWA

## Networking

- SSH
- Linux Networking
- Apache Logging

## Security

- File Integrity Monitoring
- Rootcheck
- Detection Engineering
- Threat Hunting
- Incident Investigation

---

# Lab Architecture

```
                Kali Linux
          (Attack Simulation)
                    │
                    │
        SQLi | XSS | Command Injection
                    │
                    ▼
           SafeLine WAF (Optional)
                    │
                    ▼
          Ubuntu DVWA Web Server
        Apache • PHP • MariaDB
                    │
             Apache Access Logs
                    │
              Wazuh Agent
                    │
                    ▼
            Wazuh Manager SIEM
                    │
        Decoder → Rules → Alerts
                    │
                    ▼
             Wazuh Dashboard
```

---

# Data Flow

```
Attacker

↓

Apache Web Server

↓

Apache Access Logs

↓

Wazuh Agent

↓

Wazuh Manager

↓

Decoders

↓

Detection Rules

↓

Security Alerts

↓

Dashboard

↓

SOC Investigation
```

---

# Skills Demonstrated

## SIEM Deployment

- Installed Wazuh Manager
- Installed Wazuh Dashboard
- Installed Wazuh Indexer
- Connected endpoints
- Verified agent communication

---

## Endpoint Monitoring

- Installed Wazuh Agent
- Configured endpoint monitoring
- Troubleshot connectivity
- Validated log forwarding

---

## Apache Log Monitoring

Configured monitoring for

- access.log
- error.log
- other_vhosts_access.log

Verified successful ingestion into Wazuh.

---

# Attack Scenarios

## SQL Injection

### Objective

Understand how SQL Injection attacks are detected.

Activities

- Executed SQL Injection against DVWA
- Generated malicious HTTP requests
- Analysed Apache logs
- Investigated Wazuh Rule 31164
- Reviewed dashboard alerts

Outcome

Successfully detected SQL Injection attempts using built-in Wazuh rules.

---

## Cross-Site Scripting (XSS)

Payload

```html
<script>alert(1)</script>
```

Activities

- Generated reflected XSS
- Analysed Apache logs
- Tested Wazuh detection
- Developed custom XSS detection rule
- Validated rule using wazuh-logtest

Outcome

Successfully created and tested custom XSS detection logic.

---

## Command Injection

Payload

```
127.0.0.1 && whoami
```

Activities

- Executed operating system commands
- Learned Linux command chaining
- Investigated execution context
- Observed execution as

```
www-data
```

Outcome

Demonstrated command injection and planned custom detection engineering.

---

## File Upload

Activities

- Studied unrestricted file upload
- Investigated web shell concepts
- Explored monitoring strategies
- Reviewed Apache logging

---

## SSH Authentication

Activities

- Configured SSH communication
- Monitored authentication events
- Investigated successful logins
- Investigated failed logins

---

## Brute Force

Studied

- SSH brute force
- Web authentication brute force
- Authentication monitoring
- Detection opportunities

---

# Detection Engineering

This project includes learning and development of custom Wazuh detection rules.

Areas explored

- Rule hierarchy
- Decoders
- Rule levels
- Rule inheritance
- Local rules
- Rule testing
- False positives
- Alert tuning

---

# Threat Hunting

Performed investigations using

- Apache Logs
- Wazuh Dashboard
- alerts.log
- ossec.log
- Linux authentication logs

Investigated

- Source IPs
- Suspicious URLs
- Attack payloads
- Authentication events
- Command execution

---

# File Integrity Monitoring

Explored

- Syscheck
- Rootcheck
- Protected directories
- File monitoring
- Rootkit detection

---

# Linux Administration

Practiced

- SSH
- Service management
- systemctl
- journalctl
- grep
- nano
- networking
- Apache configuration
- Wazuh configuration

---

# Challenges Encountered

Throughout the project, several operational issues were identified and resolved.

Examples include

- Wazuh agent connectivity
- Apache log ingestion
- ossec.conf configuration
- Dashboard visibility
- Network communication
- SSH connectivity
- Custom rule validation
- XSS troubleshooting
- Apache monitoring configuration

---

# Lessons Learned

This project provided practical experience in

- Security Operations Center workflows
- SIEM administration
- Linux administration
- Web application attacks
- Detection engineering
- Threat hunting
- Incident investigation
- Log analysis
- Endpoint monitoring
- Apache monitoring

---

# Future Improvements

- Active Response
- Automated IP blocking
- Custom command injection detection
- Brute force correlation rules
- File upload detection rules
- Threat intelligence integration
- MITRE ATT&CK mapping
- Dashboard improvements
- Detection tuning
- Incident response playbooks

---

# Repository Structure

```
SOC-Home-Lab

├── docs
├── attack-scenarios
├── custom-rules
├── diagrams
├── reports
├── screenshots
└── README.md
```

---

# Author

Cybersecurity Student

Focused Areas

- Security Operations
- SIEM Engineering
- Detection Engineering
- Threat Hunting
- Linux Security
- Identity & Access Management

---

# Disclaimer

This project was developed inside an isolated virtual lab for educational purposes only. All attacks were performed against intentionally vulnerable systems owned and controlled by the author.
