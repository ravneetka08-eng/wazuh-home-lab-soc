# Custom Detection Rules

This folder contains custom Wazuh detection rules developed during the SOC Home Lab project.

## Completed

### XSS Detection

Rule ID

100200

Description

Possible XSS attack detected

Detection Method

Apache access logs

Validation

✔ wazuh-logtest

✔ Apache logs

✔ DVWA Reflected XSS

Payload Tested

```html
<script>alert(1)</script>
```

Status

Successfully validated.
