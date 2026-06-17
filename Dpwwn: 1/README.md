# Dpwwn: 1 (VulnHub)

## Overview

**Dpwwn: 1** is an easy-level VulnHub machine that demonstrates how multiple security misconfigurations can be chained together to achieve full system compromise. The challenge covers network enumeration, database assessment, credential harvesting, SSH access, Linux privilege escalation, and cron job security weaknesses.

## Machine Information

| Attribute   | Value                                               |
| ----------- | --------------------------------------------------- |
| Platform    | VulnHub                                             |
| Machine     | Dpwwn: 1                                            |
| Author      | Debashis Pal                                        |
| Difficulty  | Easy                                                |
| Target OS   | CentOS Linux                                        |
| Attacker OS | Kali Linux                                          |
| Objective   | Gain Initial Access and Escalate Privileges to Root |

## Skills Demonstrated

* Network Discovery
* Service Enumeration
* Nmap Scanning
* MySQL/MariaDB Enumeration
* Database Security Assessment
* Credential Discovery
* SSH Authentication
* Linux Enumeration
* Cron Job Analysis
* Privilege Escalation
* Post-Exploitation
* Security Misconfiguration Assessment

## Tools Used

* Netdiscover
* Nmap
* MariaDB Client
* SSH
* Netcat
* Msfvenom
* Kali Linux

## Attack Methodology

1. Discover the target host on the local network.
2. Enumerate open ports and running services.
3. Identify exposed database services.
4. Assess database security configuration.
5. Discover valid user credentials.
6. Obtain initial SSH access.
7. Perform local system enumeration.
8. Analyze scheduled tasks and cron jobs.
9. Identify privilege escalation opportunities.
10. Escalate privileges to root.
11. Validate system compromise and capture the flag.

## Key Learning Outcomes

* Exposed database services can significantly increase attack surface.
* Weak authentication mechanisms create critical security risks.
* Plaintext credential storage should never be used.
* Scheduled tasks require strict permission controls.
* Enumeration is the foundation of successful penetration testing.
* Small misconfigurations can lead to complete system compromise.

## Vulnerabilities Identified

* Insecure Database Configuration
* Weak Authentication Controls
* Plaintext Credential Storage
* Misconfigured Cron Jobs
* Excessive User Permissions
* Privilege Escalation Opportunities

## Security Recommendations

* Disable unnecessary external database access.
* Enforce strong authentication policies.
* Store passwords using secure hashing algorithms.
* Restrict user permissions following the principle of least privilege.
* Regularly audit cron jobs and scheduled tasks.
* Implement file integrity monitoring.
* Conduct periodic security assessments and hardening reviews.

## Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

**Dpwwn_1_Walkthrough.pdf**

## Disclaimer

This walkthrough was completed in a legal lab environment using an intentionally vulnerable machine provided by VulnHub. The content is intended for educational purposes, cybersecurity training, and ethical hacking practice only.

---

**Author:** Omkar Babaji Sawant
**Repository:** VulnHub-Walkthroughs
