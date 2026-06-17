# Funbox: Rookie (VulnHub)

## Overview

**Funbox: Rookie** is an easy-level VulnHub machine focused on FTP enumeration, archive password cracking, SSH key discovery, credential analysis, Linux enumeration, and privilege escalation. The challenge demonstrates how exposed files, weak passwords, and misconfigured permissions can lead to complete system compromise.

This machine provides hands-on experience with password auditing, SSH authentication, local enumeration, and privilege escalation techniques commonly encountered during penetration testing engagements.

## Machine Information

| Attribute   | Value                                               |
| ----------- | --------------------------------------------------- |
| Platform    | VulnHub                                             |
| Machine     | Funbox: Rookie                                      |
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
* File Analysis
* Password Hash Cracking
* ZIP Archive Security Assessment
* John the Ripper
* SSH Key Analysis
* SSH Authentication
* Linux Enumeration
* Credential Discovery
* Privilege Escalation
* Post-Exploitation

## Tools Used

* Netdiscover
* Nmap
* FTP Client
* zip2john
* John the Ripper
* SSH
* Linux Enumeration Commands
* Kali Linux

## Attack Methodology

1. Discover the target machine on the network.
2. Enumerate open ports and running services.
3. Assess FTP security configuration.
4. Identify and download exposed files.
5. Analyze protected archives.
6. Recover archive passwords through password auditing.
7. Extract sensitive authentication material.
8. Obtain authenticated SSH access.
9. Perform local system enumeration.
10. Identify credential exposure and privilege escalation opportunities.
11. Escalate privileges to root.
12. Validate compromise and capture proof.

## Key Learning Outcomes

* Anonymous FTP services can expose sensitive organizational data.
* Weak archive passwords significantly reduce security effectiveness.
* Exposed SSH keys can provide unauthorized system access.
* Sensitive information should never be stored in user history files.
* Proper privilege management is essential for system security.
* Enumeration remains one of the most important phases of penetration testing.
* Multiple low-risk issues can combine into a critical compromise.

## Vulnerabilities Identified

* Anonymous FTP Access Enabled
* Sensitive ZIP Archives Exposed
* Weak Archive Passwords
* SSH Private Key Disclosure
* Credential Exposure
* Insecure Information Storage
* Excessive User Privileges
* Misconfigured Sudo Permissions

## Security Recommendations

* Disable anonymous FTP access where unnecessary.
* Protect sensitive files using strong encryption and access controls.
* Enforce strong password policies.
* Secure SSH private keys and authentication material.
* Avoid storing sensitive information in shell or application history files.
* Apply the principle of least privilege.
* Regularly audit sudo permissions.
* Conduct routine security assessments and hardening reviews.

## Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

**Funbox_Rookie_Walkthrough.pdf**

## Disclaimer

This walkthrough was completed in a controlled lab environment using an intentionally vulnerable machine provided by VulnHub. The content is intended solely for educational purposes, cybersecurity training, and ethical hacking practice.

---

**Author:** Omkar Babaji Sawant
**Repository:** VulnHub-Walkthroughs
