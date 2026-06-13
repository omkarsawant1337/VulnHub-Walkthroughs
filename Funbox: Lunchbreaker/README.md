# Funbox: Lunchbreaker (VulnHub)

## Overview

**Funbox: Lunchbreaker** is an easy-level VulnHub machine that focuses on FTP security assessment, user enumeration, credential attacks, password spraying, SSH access, local enumeration, and privilege escalation through password reuse.

The challenge demonstrates how poor credential management, weak passwords, and exposed backup files can lead to complete system compromise.

## Machine Information

| Attribute   | Value                                               |
| ----------- | --------------------------------------------------- |
| Platform    | VulnHub                                             |
| Machine     | Funbox: Lunchbreaker                                |
| Author      | 0815R2d2                                            |
| Series      | Funbox                                              |
| Difficulty  | Easy                                                |
| Target OS   | Ubuntu Linux                                        |
| Attacker OS | Kali Linux                                          |
| Objective   | Gain Initial Access and Escalate Privileges to Root |

## Skills Demonstrated

* Network Discovery
* Service Enumeration
* Nmap Scanning
* FTP Security Assessment
* Anonymous FTP Enumeration
* User Enumeration
* Password Auditing
* Credential Discovery
* Hydra Password Attacks
* Password Spraying
* SSH Authentication Testing
* Linux Enumeration
* Privilege Escalation
* Security Misconfiguration Assessment
* Post-Exploitation

## Tools Used

* Netdiscover
* Nmap
* Hydra
* FTP Client
* SSH
* Linux Enumeration Commands
* Kali Linux

## Attack Methodology

1. Discover the target host on the network.
2. Enumerate open ports and running services.
3. Assess FTP security configuration.
4. Identify valid usernames through information disclosure.
5. Perform credential security testing.
6. Gain authenticated access to multiple FTP accounts.
7. Discover sensitive backup files and credential information.
8. Conduct password spraying against SSH services.
9. Obtain authenticated SSH access.
10. Perform local system enumeration.
11. Identify password reuse issues.
12. Escalate privileges to root.
13. Validate compromise and retrieve proof.

## Key Learning Outcomes

* Weak passwords significantly increase attack success rates.
* Anonymous FTP services can expose sensitive information.
* Password spraying remains an effective attack technique against reused credentials.
* Backup files frequently contain valuable reconnaissance data.
* Credential reuse creates critical privilege escalation risks.
* Proper access control and credential hygiene are essential security practices.
* Enumeration is often the most important phase of a penetration test.

## Vulnerabilities Identified

* Anonymous FTP Access Enabled
* Weak FTP Passwords
* User Enumeration Exposure
* Sensitive Backup Files Exposed
* Password Spraying Susceptibility
* Password Reuse
* Poor Credential Management
* Privilege Escalation via Shared Credentials

## Security Recommendations

* Disable anonymous FTP access where unnecessary.
* Enforce strong password policies.
* Prevent password reuse across accounts.
* Protect backup files and sensitive information.
* Implement multi-factor authentication (MFA).
* Restrict access to sensitive directories.
* Monitor authentication attempts and account activity.
* Conduct regular security audits and credential reviews.

## Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

**Funbox_Lunchbreaker_Walkthrough.pdf**

## Disclaimer

This walkthrough was completed in a controlled lab environment using an intentionally vulnerable machine provided by VulnHub. The content is intended solely for educational purposes, cybersecurity training, and ethical hacking practice.

---

**Author:** Omkar Babaji Sawant
**Repository:** VulnHub-Walkthroughs
