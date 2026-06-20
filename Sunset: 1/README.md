# Sunset: 1 (VulnHub)

## Overview

**Sunset: 1** is an Easy-level VulnHub machine that focuses on FTP enumeration, password hash extraction, offline password cracking, SSH access, Linux privilege escalation, and sudo misconfiguration abuse.

The challenge demonstrates how anonymous FTP access combined with exposed credential backups and insecure sudo permissions can lead to complete system compromise.

## Machine Information

| Attribute   | Value                       |
| ----------- | --------------------------- |
| Platform    | VulnHub                     |
| Machine     | Sunset: 1                   |
| Author      | Whitecr0wz                  |
| Difficulty  | Easy                        |
| Target OS   | Debian Linux                |
| Attacker OS | Kali Linux                  |
| Objective   | Obtain User and Root Access |

## Skills Demonstrated

* Network Discovery
* Service Enumeration
* Nmap Scanning
* FTP Enumeration
* Anonymous FTP Assessment
* Credential Discovery
* Password Hash Analysis
* Offline Password Cracking
* John the Ripper
* SSH Authentication
* Linux Enumeration
* Sudo Enumeration
* GTFOBins Research
* Linux Privilege Escalation
* Post-Exploitation

## Tools Used

* ARP-Scan
* Nmap
* FTP Client
* John the Ripper
* SSH
* GTFOBins
* Linux Enumeration Commands
* Kali Linux

## Attack Methodology

1. Discover the target machine on the network.
2. Enumerate open ports and running services.
3. Identify anonymous FTP access.
4. Download exposed backup files.
5. Extract password hashes from the backup.
6. Crack password hashes offline using John the Ripper.
7. Obtain valid user credentials.
8. Gain authenticated SSH access.
9. Enumerate local system permissions.
10. Review sudo privileges.
11. Identify privilege escalation opportunities.
12. Abuse a vulnerable sudo configuration.
13. Escalate privileges to root.
14. Validate compromise and retrieve flags.

## Key Learning Outcomes

* Anonymous FTP access can expose sensitive information.
* Backup files frequently contain valuable credentials.
* Password hashes should be protected as sensitive data.
* Weak passwords significantly increase security risk.
* Offline password cracking remains highly effective against weak credentials.
* Misconfigured sudo permissions can directly lead to root compromise.
* Enumeration is one of the most important phases of penetration testing.

## Vulnerabilities Identified

* Anonymous FTP Access Enabled
* Sensitive Backup File Exposure
* Password Hash Disclosure
* Weak Password Security
* Credential Exposure
* Insecure Access Controls
* Excessive Sudo Permissions
* Privilege Escalation via GTFOBins

## Security Recommendations

* Disable anonymous FTP access unless absolutely necessary.
* Restrict access to backup files and sensitive data.
* Enforce strong password policies.
* Store password backups securely.
* Implement multi-factor authentication for SSH.
* Apply the Principle of Least Privilege.
* Regularly audit sudo permissions.
* Monitor FTP, SSH, and sudo activity for suspicious behavior.
* Conduct routine vulnerability assessments and security reviews.

## Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

**Sunset_1_Walkthrough.pdf**

## Attack Chain Summary

* Network Discovery using ARP-Scan
* Service Enumeration with Nmap
* Anonymous FTP Access
* Backup File Discovery
* Password Hash Extraction
* John the Ripper Password Cracking
* SSH Login as sunset
* Sudo Enumeration
* GTFOBins Exploitation using ed
* Root Privilege Escalation
* Flag Retrieval

## Highlights

### Enumeration Findings

* FTP service exposed
* Anonymous FTP login enabled
* SSH service available
* Backup file accessible through FTP
* Multiple SHA-512 password hashes disclosed

### Initial Access

* Backup file downloaded from FTP.
* Password hash extracted and cracked using John the Ripper.
* SSH access obtained as user **sunset**.

### Privilege Escalation

The following sudo permission was discovered:

```bash
(root) NOPASSWD: /usr/bin/ed
```

Using the GTFOBins technique:

```bash
sudo ed
!/bin/sh
```

resulted in a root shell.

## Disclaimer

This walkthrough was performed in a controlled lab environment using an intentionally vulnerable machine provided by VulnHub. The content is intended solely for educational purposes, cybersecurity training, and ethical hacking practice.

---

**Author:** Omkar Babaji Sawant
**Repository:** VulnHub-Walkthroughs
