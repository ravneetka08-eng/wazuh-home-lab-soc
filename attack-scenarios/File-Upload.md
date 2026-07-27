# Malicious File Upload

## Objective

To demonstrate insecure file upload functionality within DVWA and investigate related events using Wazuh.

---

# Attack Description

Applications that fail to validate uploaded files may allow attackers to upload malicious scripts.

Potential risks include:

- Remote Code Execution
- Web Shell deployment
- Malware hosting

---

# Lab Steps

1. Open:

DVWA → File Upload

2. Upload the demonstration file.

3. Verify upload success.

---

# Investigation

Verified:

- Apache logs
- Uploaded file location
- Wazuh monitoring

Observed the upload request within Apache access logs.

---

# MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Exploit Public-Facing Application | T1190 |

---

# Skills Demonstrated

- File Upload Testing
- Web Server Monitoring
- Apache Log Analysis
