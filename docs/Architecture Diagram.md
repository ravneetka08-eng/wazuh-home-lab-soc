
                                        Internet
                                            │
                                            │
                                   HTTP / HTTPS Requests
                                            │
                                            ▼
                               ┌────────────────────────┐
                               │      Kali Linux VM     │
                               │------------------------│
                               │ • Firefox             │
                               │ • Attack Simulation   │
                               │ • SQL Injection       │
                               │ • XSS                │
                               │ • Command Injection  │
                               │ • Brute Force        │
                               └──────────┬────────────┘
                                          │
                                          │ HTTP
                                          ▼
                          ┌────────────────────────────────┐
                          │        SafeLine WAF            │
                          │--------------------------------│
                          │ • Reverse Proxy               │
                          │ • Web Filtering               │
                          │ • Request Inspection          │
                          │ • Attack Detection            │
                          └──────────┬─────────────────────┘
                                     │
                                     │
                                     ▼
                    ┌─────────────────────────────────────┐
                    │         Ubuntu DVWA Server          │
                    │-------------------------------------│
                    │ Apache2                            │
                    │ PHP                                │
                    │ MariaDB                            │
                    │ DVWA                               │
                    │                                    │
                    │ Generates:                         │
                    │ • Apache Access Logs              │
                    │ • Apache Error Logs               │
                    │ • Authentication Logs             │
                    └───────────────┬────────────────────┘
                                    │
                     Log Collection │
                                    ▼
                    ┌─────────────────────────────────────┐
                    │         Wazuh Agent                 │
                    │-------------------------------------│
                    │ Logcollector                       │
                    │ Syscheck                           │
                    │ Rootcheck                          │
                    │ Syscollector                       │
                    │ Active Response                    │
                    └───────────────┬────────────────────┘
                                    │
                                    │ Secure TCP 1514
                                    ▼
          ┌───────────────────────────────────────────────────────────┐
          │                  Wazuh Manager VM                         │
          │-----------------------------------------------------------│
          │                                                           │
          │ Receives Endpoint Logs                                    │
          │                                                           │
          │ Decoders                                                  │
          │      │                                                    │
          │      ▼                                                    │
          │ Rules Engine                                              │
          │      │                                                    │
          │      ▼                                                    │
          │ Alert Generation                                          │
          │      │                                                    │
          │      ▼                                                    │
          │ File Integrity Monitoring                                 │
          │ Rootcheck                                                 │
          │ Vulnerability Detection                                   │
          │ XDR Functions                                             │
          └───────────────┬───────────────────────────────────────────┘
                          │
                          │
                          ▼
             ┌────────────────────────────────┐
             │      Wazuh Indexer             │
             │--------------------------------│
             │ OpenSearch Storage             │
             │ Event Indexing                 │
             │ Search                         │
             │ Analytics                      │
             └──────────────┬─────────────────┘
                            │
                            ▼
             ┌────────────────────────────────┐
             │      Wazuh Dashboard           │
             │--------------------------------│
             │ Security Events               │
             │ Agent Monitoring              │
             │ Rule Monitoring               │
             │ Threat Hunting                │
             │ Visualisations                │
             │ Alert Investigation           │
             └────────────────────────────────┘



             Virtual Machine Topology
Virtual Machine	IP Address (example)	Purpose
Kali Linux	192.168.128.108	Attack simulation
SafeLine WAF	192.168.128.106	Web Application Firewall / Reverse Proxy
Ubuntu DVWA	192.168.128.106 (Apache behind WAF)	Vulnerable web application
Ubuntu Wazuh	192.168.128.109	Wazuh Manager, Indexer, Dashboard
Attack Scenarios Performed
Kali Linux
     │
     ├── SQL Injection
     │
     ├── Cross Site Scripting (XSS)
     │
     ├── Command Injection
     │
     ├── File Upload
     │
     └── SSH Authentication Testing
Logs Monitored
Apache access.log
Apache error.log
Apache other_vhosts_access.log

↓

Wazuh Agent

↓

Wazuh Manager

↓

Rules

↓

Dashboard
Detection Techniques Demonstrated
Attack	Status	Detection
SQL Injection	✅ Completed	Built-in Wazuh Rule 31164
Cross-Site Scripting (XSS)	✅ Completed	Custom detection validated with wazuh-logtest
Command Injection	✅ Completed	Apache log analysis and detection workflow
File Upload	✅ Completed	Apache log monitoring and investigation
SSH Monitoring	✅ Completed	PAM and sudo events
File Integrity Monitoring	✅ Completed	Syscheck
Rootcheck	✅ Completed	Rule 510
Threat Hunting	✅ Completed	Wazuh Dashboard investigations
