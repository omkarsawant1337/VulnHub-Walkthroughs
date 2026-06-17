# Funbox: Under Construction! (VulnHub)

## Overview

**Funbox: Under Construction!** is an easy-to-medium VulnHub machine that focuses on web application security, directory enumeration, vulnerability assessment, credential discovery, lateral movement, and Linux privilege escalation.

The challenge demonstrates how exposed installation files, insecure configurations, weak credential management, and poor privilege controls can be chained together to achieve complete system compromise.

## Machine Information

| Attribute          | Value                                               |
| ------------------ | --------------------------------------------------- |
| Platform           | VulnHub                                             |
| Machine            | Funbox: Under Construction!                         |
| Author             | 0815R2d2                                            |
| Series             | Funbox                                              |
| Difficulty         | Easy–Medium                                         |
| Target OS          | Ubuntu Linux                                        |
| Attacker OS        | Kali Linux                                          |
| Primary Technology | Apache, osCommerce, Postfix                         |
| Objective          | Gain Initial Access and Escalate Privileges to Root |

## Skills Demonstrated

* Network Discovery
* Service Enumeration
* Nmap Scanning
* Web Application Enumeration
* Directory Brute Forcing
* Gobuster Enumeration
* osCommerce Security Assessment
* Vulnerability Research
* CVE Analysis
* Remote Code Execution Assessment
* Reverse Shell Handling
* Linux Enumeration
* Credential Discovery
* Lateral Movement
* Process Monitoring
* Cron Job Analysis
* Base64 Decoding
* Linux Privilege Escalation
* Post-Exploitation

## Tools Used

* ARP-Scan
* Nmap
* Gobuster
* SearchSploit
* Netcat
* Python
* pspy64
* Linux Enumeration Commands
* Kali Linux

## Attack Methodology

1. Discover the target host on the local network.
2. Enumerate open ports and services.
3. Perform web application reconnaissance.
4. Discover hidden directories and web resources.
5. Identify vulnerable application components.
6. Research publicly known vulnerabilities.
7. Obtain remote code execution through a vulnerable service.
8. Establish a reverse shell on the target.
9. Enumerate configuration files and sensitive data.
10. Recover valid credentials and perform lateral movement.
11. Monitor system processes for privilege escalation opportunities.
12. Analyze scheduled tasks and exposed secrets.
13. Escalate privileges to root.
14. Validate compromise and capture proof.

## Key Learning Outcomes

* Exposed installation directories can introduce critical security risks.
* Regular vulnerability management is essential for web applications.
* Configuration backup files often contain sensitive credentials.
* Process monitoring tools can reveal hidden privilege escalation paths.
* Poor secret management creates significant security weaknesses.
* Weak access controls increase the likelihood of system compromise.
* Enumeration remains one of the most critical phases of penetration testing.

## Vulnerabilities Identified

* Vulnerable Web Application Deployment
* Exposed Installation Directory
* Outdated Application Components
* Remote Code Execution Exposure
* Sensitive Configuration File Disclosure
* Credential Exposure
* Weak Secret Management
* Privilege Escalation Through Information Disclosure
* Insecure File Permissions

## Security Recommendations

* Remove or secure installation directories after deployment.
* Keep web applications updated with the latest security patches.
* Restrict access to backup and configuration files.
* Store secrets securely using credential vaults or environment variables.
* Implement least-privilege access controls.
* Regularly audit scheduled tasks and automation scripts.
* Restrict file permissions on sensitive directories.
* Deploy centralized logging and monitoring solutions.
* Conduct periodic vulnerability assessments and penetration tests.

## Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

**Funbox_Under_Construction_Walkthrough.pdf**

## Disclaimer

This walkthrough was completed in a controlled lab environment using an intentionally vulnerable machine provided by VulnHub. The content is intended solely for educational purposes, cybersecurity training, and ethical hacking practice.

---

**Author:** Omkar Babaji Sawant
**Repository:** VulnHub-Walkthroughs
