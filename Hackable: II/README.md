# Hackable: II (VulnHub)

## Overview

**Hackable: II** is an easy-level VulnHub machine designed to teach fundamental penetration testing concepts including service enumeration, FTP security assessment, web exploitation, credential discovery, password auditing, SSH access, and Linux privilege escalation.

The challenge demonstrates how anonymous FTP access combined with a web-accessible upload directory can lead to remote code execution and full system compromise.

## Machine Information

| Attribute   | Value                       |
| ----------- | --------------------------- |
| Platform    | VulnHub                     |
| Machine     | Hackable: II                |
| Author      | Elias Sousa                 |
| Series      | Hackable                    |
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
* Web Directory Enumeration
* File Upload Security Testing
* Remote Code Execution Analysis
* Reverse Shell Handling
* Linux Enumeration
* Credential Discovery
* Password Hash Analysis
* Password Cracking
* SSH Authentication
* Sudo Enumeration
* Linux Privilege Escalation
* GTFOBins Research
* Post-Exploitation

## Tools Used

* Netdiscover
* Nmap
* FTP Client
* DIRB
* Netcat
* PHP Reverse Shell
* CrackStation
* SSH
* GTFOBins
* Kali Linux

## Attack Methodology

1. Discover the target machine on the local network.
2. Enumerate open ports and running services.
3. Assess FTP security configuration.
4. Identify anonymously accessible resources.
5. Discover clues through file analysis.
6. Perform web application and directory enumeration.
7. Identify web-accessible upload locations.
8. Upload a controlled payload in a lab environment.
9. Obtain initial system access.
10. Enumerate local files and sensitive information.
11. Recover user credentials.
12. Perform password analysis and recovery.
13. Obtain authenticated SSH access.
14. Enumerate sudo permissions.
15. Identify privilege escalation opportunities.
16. Escalate privileges to root.
17. Validate compromise and capture flags.

## Key Learning Outcomes

* Anonymous FTP access significantly increases attack surface.
* Web-accessible upload directories create serious security risks.
* File upload controls should be strictly enforced.
* Password reuse and weak passwords can lead to compromise.
* Sensitive information should never be exposed through scripts or files.
* Proper sudo configuration is critical for system security.
* Enumeration remains one of the most important penetration testing phases.

## Vulnerabilities Identified

* Anonymous FTP Access Enabled
* Writable FTP Directory
* Web-Accessible File Upload Location
* Remote Code Execution Opportunity
* Credential Disclosure
* Weak Password Security
* Insecure Information Storage
* Misconfigured Sudo Permissions
* Privilege Escalation via GTFOBins

## Security Recommendations

* Disable anonymous FTP access unless absolutely required.
* Restrict upload permissions and validate uploaded files.
* Prevent execution of uploaded content from web directories.
* Implement strong password policies.
* Store credentials securely using proper hashing mechanisms.
* Restrict access to sensitive scripts and files.
* Regularly audit sudo permissions.
* Apply the principle of least privilege.
* Conduct routine vulnerability assessments and penetration tests.

## Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

**Hackable_II_Walkthrough.pdf**

## Disclaimer

This walkthrough was completed in a controlled lab environment using an intentionally vulnerable machine provided by VulnHub. The content is intended solely for educational purposes, cybersecurity training, and ethical hacking practice.

---

**Author:** Omkar Babaji Sawant
**Repository:** VulnHub-Walkthroughs
