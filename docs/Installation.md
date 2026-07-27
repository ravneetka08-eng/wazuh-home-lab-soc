# Installation Guide

## Project Overview

This document explains how the SOC Home Lab was built from scratch using VirtualBox, Ubuntu Linux, Kali Linux, DVWA, SafeLine WAF, and Wazuh SIEM.

---

# Lab Requirements

## Hardware

- Windows 11 Host
- Minimum 16 GB RAM (recommended)
- 100 GB free disk space
- Internet connection

---

# Software

- Oracle VirtualBox
- Ubuntu Server/Desktop ISO
- Kali Linux ISO
- Wazuh
- DVWA
- Apache2
- PHP
- MariaDB
- Git

---

# Virtual Machines

## VM 1

Name

Ubuntu Wazuh

Purpose

Central SIEM

Installed Components

- Wazuh Manager
- Wazuh Dashboard
- Wazuh Indexer

---

## VM 2

Name

Ubuntu DVWA

Purpose

Target Server

Installed Components

- Apache2
- PHP
- MariaDB
- DVWA
- Wazuh Agent

---

## VM 3

Name

Kali Linux

Purpose

Attacker Machine

Installed Components

- Firefox
- Linux tools

---

# Network Configuration

All virtual machines were configured using a bridged network adapter so each VM received its own IP address and could communicate directly.

Connectivity was verified using:

- ping
- ssh
- nc (netcat)

---

# Wazuh Installation

Installed the following:

- Wazuh Manager
- Wazuh Dashboard
- Wazuh Indexer

Verified services were running correctly.

Confirmed dashboard accessibility through a web browser.

---

# Wazuh Agent Installation

Installed the Wazuh Agent on the Ubuntu DVWA server.

Configured:

- Manager IP
- Agent registration
- Secure communication

Verified:

- Agent status
- Connection to manager
- Event forwarding

---

# Apache Configuration

Installed:

- Apache2

Configured Wazuh to monitor:

- /var/log/apache2/access.log
- /var/log/apache2/error.log
- /var/log/apache2/other_vhosts_access.log

Restarted the Wazuh Agent after configuration changes.

---

# DVWA Installation

Installed:

- PHP
- MariaDB
- DVWA

Configured:

- Database
- Apache
- Application setup

Verified that DVWA was accessible through the browser.

---

# SafeLine WAF

Configured SafeLine as a reverse proxy in front of DVWA.

Verified traffic flow between:

Kali Linux

↓

SafeLine

↓

DVWA

---

# SSH Configuration

Enabled SSH communication between virtual machines.

Used SSH for:

- Remote administration
- Log investigation
- Configuration management

---

# Verification

Verified:

✅ Agent online

✅ Dashboard connected

✅ Apache logs collected

✅ Security events visible

✅ Alerts generated

---

# Attacks Successfully Tested

- SQL Injection
- Reflected XSS
- Command Injection
- File Upload
- SSH authentication monitoring
- File Integrity Monitoring
- Rootcheck

---

# Troubleshooting Performed

During development the following issues were resolved:

- Agent offline
- Incorrect manager IP
- Apache log ingestion
- Dashboard alerts missing
- ossec.conf configuration
- Network communication
- SSH connectivity
- Wazuh rule validation
- Custom rule testing

---

# Final Environment

Kali Linux

↓

SafeLine WAF

↓

Ubuntu DVWA

↓

Apache Logs

↓

Wazuh Agent

↓

Wazuh Manager

↓

Wazuh Dashboard

The environment successfully detected and investigated multiple attack scenarios while providing centralized log collection and security monitoring.
