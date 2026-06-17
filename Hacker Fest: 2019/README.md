Hacker Fest: 2019 (VulnHub)
Overview

Hacker Fest: 2019 is a medium-difficulty VulnHub machine that focuses on WordPress security assessment, anonymous FTP exposure, credential disclosure, SQL Injection exploitation, password cracking, SSH access, and Linux privilege escalation.

The challenge demonstrates how multiple security weaknesses—including exposed configuration files, vulnerable WordPress plugins, and excessive sudo permissions—can be chained together to achieve complete system compromise.

Machine Information
Attribute	Value
Platform	VulnHub
Machine	Hacker Fest: 2019
Author	Martin Haller
Series	Hacker Fest
Difficulty	Medium
Target OS	Debian Linux
Attacker OS	Kali Linux
Primary Technology	WordPress
Objective	Gain Initial Access and Escalate Privileges to Root
Skills Demonstrated
Network Discovery
Service Enumeration
Nmap Scanning
FTP Security Assessment
Anonymous FTP Enumeration
WordPress Security Assessment
WPScan Enumeration
Configuration File Analysis
Credential Discovery
SQL Injection Assessment
Vulnerability Research
Metasploit Framework
Password Hash Extraction
Password Cracking
John the Ripper
SSH Authentication
Linux Enumeration
Sudo Enumeration
Privilege Escalation
Post-Exploitation
Tools Used
ARP-Scan
Nmap
FTP Client
WPScan
Metasploit Framework
John the Ripper
SSH
Linux Enumeration Commands
Kali Linux
Attack Methodology
Discover the target machine on the local network.
Enumerate open ports and running services.
Identify anonymous FTP access.
Download exposed WordPress configuration files.
Extract sensitive credentials from configuration files.
Enumerate the WordPress installation.
Identify vulnerable plugins and attack surfaces.
Exploit a vulnerable WordPress plugin.
Extract authentication hashes.
Crack password hashes using offline password auditing.
Obtain authenticated SSH access.
Perform local privilege escalation enumeration.
Identify excessive sudo permissions.
Escalate privileges to root.
Validate compromise and retrieve proof.
Key Learning Outcomes
Configuration files frequently contain highly sensitive information.
Anonymous FTP access significantly increases attack surface exposure.
Outdated WordPress installations create exploitable security risks.
Vulnerable plugins remain one of the most common WordPress attack vectors.
Password hashes should be protected and monitored carefully.
Excessive sudo permissions can immediately lead to full compromise.
Security hardening requires a defense-in-depth approach.
Vulnerabilities Identified
Anonymous FTP Access Enabled
WordPress Configuration File Disclosure
Database Credential Exposure
Outdated WordPress Installation
Vulnerable WordPress Plugin
SQL Injection Exposure
Weak Password Security
Excessive Sudo Permissions
Privilege Escalation Misconfiguration
Security Recommendations
Disable anonymous FTP access unless absolutely necessary.
Restrict access to WordPress configuration files.
Store credentials securely and rotate exposed secrets.
Keep WordPress core, themes, and plugins updated.
Remove vulnerable or unsupported plugins.
Restrict Webmin access and administrative interfaces.
Enforce least-privilege sudo configurations.
Monitor systems for exposed credentials and suspicious activity.
Conduct regular vulnerability assessments and penetration testing.
Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

Hacker_Fest_2019_Walkthrough.pdf

Disclaimer

This walkthrough was completed in a controlled lab environment using an intentionally vulnerable machine provided by VulnHub. The content is intended solely for educational purposes, cybersecurity training, and ethical hacking practice.

Author

Omkar Babaji Sawant

Repository

VulnHub-Walkthroughs
