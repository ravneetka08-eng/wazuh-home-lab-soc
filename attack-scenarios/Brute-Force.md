# Brute Force Attack

## Objective

To demonstrate password guessing attacks against DVWA and investigate authentication events using Wazuh.

---

# Attack Description

A brute force attack repeatedly attempts different username and password combinations until authentication succeeds.

---

# Attack Steps

1. Navigate to:

DVWA → Brute Force

2. Submit multiple incorrect passwords.

3. Observe application responses.

---

# Investigation

Reviewed:

- Apache logs
- Authentication logs
- Wazuh Dashboard

Observed authentication attempts and related events.

---

# MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Brute Force | T1110 |

---

# Possible Defences

- MFA
- Account Lockout
- Rate Limiting
- CAPTCHA
- Password Policies

---

# Skills Demonstrated

- Authentication monitoring
- Threat hunting
- Log analysis
