# HackathonCTF: 2 (VulnHub)

## Overview

**HackathonCTF: 2** is an easy-level VulnHub machine focused on enumeration, anonymous FTP access, directory brute-forcing, credential discovery, SSH compromise, and Linux privilege escalation through insecure sudo configurations.

The challenge demonstrates how seemingly minor information disclosures can be chained together to achieve complete system compromise, reinforcing the importance of thorough enumeration and security hardening.

## Machine Information

| Attribute   | Value                       |
| ----------- | --------------------------- |
| Platform    | VulnHub                     |
| Machine     | HackathonCTF: 2             |
| Author      | Somu Sen                    |
| Series      | HackathonCTF                |
| Difficulty  | Easy                        |
| Target OS   | Ubuntu Linux                |
| Attacker OS | Kali Linux                  |
| Objective   | Obtain User and Root Access |

## Skills Demonstrated

* Network Discovery
* Service Enumeration
* Nmap Scanning
* FTP Security Assessment
* Anonymous FTP Enumeration
* File Analysis
* Web Application Enumeration
* Directory Brute Forcing
* Gobuster Enumeration
* Source Code Review
* Information Disclosure Analysis
* Credential Discovery
* Password Auditing
* Hydra Password Attacks
* SSH Authentication
* Linux Enumeration
* Sudo Enumeration
* GTFOBins Research
* Linux Privilege Escalation
* Post-Exploitation

## Tools Used

* Netdiscover
* Nmap
* FTP Client
* Gobuster
* Hydra
* SSH
* Vim
* GTFOBins
* Kali Linux

## Attack Methodology

1. Discover the target machine on the network.
2. Enumerate open ports and running services.
3. Assess FTP security configuration.
4. Download exposed files from anonymous FTP access.
5. Analyze discovered files for useful information.
6. Perform directory brute-forcing using a custom wordlist.
7. Discover hidden web resources.
8. Review source code for information disclosure.
9. Identify valid usernames.
10. Conduct credential security testing.
11. Obtain authenticated SSH access.
12. Perform local system enumeration.
13. Analyze sudo permissions.
14. Identify privilege escalation opportunities.
15. Escalate privileges to root.
16. Validate compromise and capture flags.

## Key Learning Outcomes

* Anonymous FTP access can expose sensitive information.
* Custom wordlists discovered during enumeration can become valuable attack resources.
* Source code comments may reveal critical information.
* Weak passwords significantly increase attack success rates.
* Proper sudo configuration is essential for system security.
* Enumeration remains one of the most important phases of penetration testing.
* Multiple low-severity weaknesses can combine into a critical compromise.

## Vulnerabilities Identified

* Anonymous FTP Access Enabled
* Sensitive File Exposure
* Information Disclosure via Source Code
* Weak SSH Credentials
* Insecure Authentication Practices
* Misconfigured Sudo Permissions
* Privilege Escalation via Vim
* Inadequate Access Controls

## Security Recommendations

* Disable anonymous FTP access unless explicitly required.
* Restrict public access to sensitive files and resources.
* Remove sensitive information from source code and comments.
* Enforce strong password policies.
* Implement multi-factor authentication where possible.
* Regularly audit sudo permissions.
* Apply the principle of least privilege.
* Monitor authentication logs for suspicious activity.
* Conduct regular vulnerability assessments and penetration testing.

## Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

**HackathonCTF_2_Walkthrough.pdf**

## Disclaimer

This walkthrough was completed in a controlled lab environment using an intentionally vulnerable machine provided by VulnHub. The content is intended solely for educational purposes, cybersecurity training, and ethical hacking practice.

---

**Author:** Omkar Babaji Sawant
**Repository:** VulnHub-Walkthroughs
