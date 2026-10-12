# 🛡️ SOC/Blue Team Home Lab – Active Directory & Troubleshooting

[![PL](https://img.shields.io/badge/Język-Polski-red.svg)](README_PL.md)
[![EN](https://img.shields.io/badge/Language-English-blue.svg)](README.md)

Module 2: Active Directory, GPO & DNS Troubleshooting (Break-Fix)

In this phase of building my SOC/Blue Team Home Lab, I moved from initial deployment to hands-on "Break-Fix" troubleshooting scenarios. Instead of just setting things up, I deliberately introduced configuration errors and diagnosed them from the client endpoint to master real-world administrative problem-solving.

1. GPO Hardening & Troubleshooting
Deployed a Group Policy Object (GPO) restricting access to Command Prompt (CMD) and Control Panel for standard users.

Break-Fix (Mislinked GPO): Simulated an administrative misconfiguration by linking the policy to an incorrect OU. Performed live client-side diagnostics using native CLI tools.
Security Filtering & Delegation: Configured advanced security filtering. Applied an Explicit Deny rule on the Apply Group Policy permission for the Domain Admins group, successfully exempting administrators from restrictions while keeping standard users locked down.
2. DNS Management & Interface Metrics (Routing)
Verified and maintained Forward and Reverse Lookup Zones on the Domain Controller (managing A, CNAME, and PTR records).

Break-Fix (DNS Blindness): Injected a malformed DNS server address on the client network interface to simulate name-resolution failure, diagnosed using ipconfig /flushdns and nslookup dc01.cyberlab.local.
Virtualization Routing Conflict (Dual-Homed VM): The client VM ran two active adapters (NAT for Internet, Internal Network for AD). Windows prioritized the NAT adapter, forwarding internal AD queries to the home router.
Resolution (Interface Metrics): Manually tuned IPv4 Interface Metrics. Assigned a high-priority metric (10) to the internal lab adapter and a lower priority (100) to the NAT adapter. This successfully synchronized domain name resolution alongside uninterrupted Internet access.ction.

## 📸 Screenshots
<img width="1710" height="1387" alt="Stan Wazuh" src="<img width="941" height="633" alt="1" src="https://github.com/user-attachments/assets/b73f77bf-7f12-4da6-b391-c7c56f542eda" />

<img width="1024" height="830" alt="Logi Wazuh" src="<img width="659" height="587" alt="2" src="https://github.com/user-attachments/assets/cce36dec-8ef2-4326-a93b-5eec7001c29c" />

<img width="1715" height="1386" alt="Logi WS" src="<img width="779" height="563" alt="3" src="https://github.com/user-attachments/assets/cbe9bdf0-b76d-4795-87be-407f76de6424" />


