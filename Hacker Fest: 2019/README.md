# Hacker Fest: 2019 (VulnHub)

## Overview

**Hacker Fest: 2019** is a medium-difficulty VulnHub machine that focuses on WordPress security assessment, anonymous FTP enumeration, credential disclosure, SQL Injection, password cracking, SSH access, and Linux privilege escalation.

The challenge demonstrates how exposed configuration files, outdated web applications, vulnerable plugins, and excessive sudo permissions can be chained together to achieve complete system compromise.

## Machine Information

| Attribute | Value |
|------------|---------|
| Platform | VulnHub |
| Machine | Hacker Fest: 2019 |
| Author | Martin Haller |
| Series | Hacker Fest |
| Difficulty | Medium |
| Target OS | Debian Linux |
| Attacker OS | Kali Linux |
| Objective | Gain Initial Access and Escalate Privileges to Root |

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- Nmap Scanning
- FTP Security Assessment
- Anonymous FTP Enumeration
- WordPress Security Assessment
- WPScan Enumeration
- Configuration File Analysis
- Credential Discovery
- SQL Injection Assessment
- Vulnerability Research
- Metasploit Framework
- Password Hash Extraction
- Password Cracking
- John the Ripper
- SSH Authentication
- Linux Enumeration
- Sudo Enumeration
- Linux Privilege Escalation
- Post-Exploitation

## Tools Used

- ARP-Scan
- Nmap
- FTP Client
- WPScan
- Metasploit Framework
- John the Ripper
- SSH
- Linux Enumeration Commands
- Kali Linux

## Attack Methodology

1. Discover the target machine on the network.
2. Enumerate open ports and running services.
3. Assess FTP security configuration.
4. Access the FTP service anonymously.
5. Download exposed WordPress configuration files.
6. Identify credential disclosure vulnerabilities.
7. Perform WordPress enumeration.
8. Discover vulnerable plugins and attack surfaces.
9. Exploit SQL Injection vulnerabilities.
10. Extract password hashes from the application database.
11. Crack recovered password hashes.
12. Obtain authenticated SSH access.
13. Perform local system enumeration.
14. Review sudo permissions.
15. Escalate privileges to root.
16. Validate compromise and capture proof.

## Key Learning Outcomes

- Anonymous FTP access can expose highly sensitive application files.
- WordPress configuration files should never be publicly accessible.
- Outdated plugins significantly increase security risk.
- SQL Injection remains one of the most critical web application vulnerabilities.
- Password hashing alone is insufficient if weak passwords are used.
- Excessive sudo privileges can lead directly to full system compromise.
- Proper vulnerability management is essential for securing web applications.

## Vulnerabilities Identified

- Anonymous FTP Access Enabled
- WordPress Configuration File Disclosure
- Credential Exposure
- Outdated WordPress Installation
- Vulnerable WordPress Plugin
- SQL Injection Vulnerability
- Weak Password Security
- Excessive Sudo Permissions
- Privilege Escalation via Misconfigured Access Controls

## Security Recommendations

- Disable anonymous FTP access unless absolutely required.
- Restrict access to WordPress configuration files.
- Keep WordPress core, themes, and plugins updated.
- Remove vulnerable or unsupported plugins.
- Perform regular vulnerability assessments.
- Enforce strong password policies.
- Implement multi-factor authentication where possible.
- Apply the principle of least privilege.
- Regularly audit sudo permissions and privileged accounts.
- Monitor for exposed credentials and sensitive information.

## Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

**Hacker_Fest_2019_Walkthrough.pdf**

## Disclaimer

This walkthrough was completed in a controlled lab environment using an intentionally vulnerable machine provided by VulnHub. The content is intended solely for educational purposes, cybersecurity training, and ethical hacking practice.

---

**Author:** Omkar Babaji Sawant  
**Repository:** VulnHub-Walkthroughs
