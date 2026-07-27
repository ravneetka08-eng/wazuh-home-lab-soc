# Malicious File Upload

## Objective

The objective of this exercise was to demonstrate the risks associated with insecure file upload functionality in DVWA and investigate how upload activity can be monitored using Apache logs and Wazuh SIEM.

---

# Background

Many web applications allow users to upload files such as images, documents, or profile pictures.

If file uploads are not properly validated, attackers may upload malicious files instead.

Examples include:

- PHP web shells
- Backdoors
- Malware
- Reverse shells
- Ransomware

Improper file validation is one of the most common web application security weaknesses.

---

# Lab Environment

| Component | Purpose |
|-----------|---------|
| Kali Linux | Attacker |
| Ubuntu DVWA | Vulnerable Target |
| Apache2 | Web Server |
| Wazuh Agent | Endpoint Monitoring |
| Wazuh Manager | SIEM |
| Wazuh Dashboard | Investigation |

---

# Attack Workflow

```
Kali Linux

↓

DVWA File Upload Module

↓

Apache Web Server

↓

File Stored

↓

Apache Access Log

↓

Wazuh Agent

↓

Wazuh Manager

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
DVWA → File Upload
```

---

## Step 3

Select the demonstration file.

---

## Step 4

Upload the file.

The application accepted the upload and stored it within the upload directory.

---

# Investigation

After uploading the file, the following activities were investigated:

- Apache access logs
- Upload request
- Timestamp
- Source IP
- HTTP request
- Dashboard events

The upload request was successfully recorded in the Apache logs and collected by the Wazuh Agent.

---

# Apache Log Evidence

Example request:

```
POST /DVWA/vulnerabilities/upload/
```

Apache recorded the upload request, allowing investigators to reconstruct the activity.

---

# Security Risks

If unrestricted uploads are allowed, attackers may upload:

- PHP shells
- Executable scripts
- Malware
- Remote access tools
- Reverse shells

Successful execution of uploaded files may lead to:

- Remote Code Execution
- Data theft
- Persistence
- Privilege escalation
- Full server compromise

---

# Wazuh Investigation

The Wazuh Agent collected the Apache logs generated during the upload.

The investigation included:

- Reviewing upload requests
- Identifying source IP
- Reviewing timestamps
- Confirming successful log collection

Although a dedicated file upload detection rule was not implemented, Apache logging provided sufficient evidence to investigate upload activity.

---

# MITRE ATT&CK Mapping

| Technique | ID |
|-----------|----|
| Exploit Public-Facing Application | T1190 |

---

# Security Recommendations

Secure file upload functionality should include:

- File type validation
- File extension allow-listing
- MIME type verification
- Antivirus scanning
- Upload size restrictions
- Store uploads outside the web root
- Rename uploaded files
- Disable script execution in upload directories
- Continuous monitoring with SIEM

---

# Skills Demonstrated

This exercise demonstrated:

- Web application security testing
- Apache log analysis
- Security monitoring
- Threat hunting
- Wazuh investigation
- Incident analysis

---

# Future Improvements

Future enhancements include:

- Custom Wazuh file upload detection rule
- Detection of suspicious file extensions
- YARA scanning of uploaded files
- Active Response to quarantine malicious uploads
- Integration with antivirus scanning

---

# Lessons Learned

This exercise demonstrated how insecure file upload functionality can expose web servers to serious security risks.

Although only a benign demonstration file was uploaded during the lab, the investigation showed how upload activity can be reconstructed using Apache logs and monitored through Wazuh. Future work will focus on developing custom detection rules and automated responses for malicious file uploads.
