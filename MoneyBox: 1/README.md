# MoneyBox: 1

## Overview

**MoneyBox: 1** is an Easy–Medium difficulty VulnHub machine created by **Kirthik_T**. The box focuses on web enumeration, source code analysis, anonymous FTP abuse, steganography, SSH brute forcing, lateral movement using SSH keys, and Linux privilege escalation through a misconfigured sudo rule. :contentReference[oaicite:0]{index=0}

## Machine Information

| Attribute | Value |
|------------|---------|
| Platform | VulnHub |
| Machine | MoneyBox: 1 |
| Author | Kirthik_T |
| Release Date | 27 February 2021 |
| Difficulty | Easy–Medium |
| Target OS | Debian Linux |
| Attacker OS | Kali Linux |
| Objective | Obtain User Flags and Root Flag |

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- Nmap Scanning
- FTP Enumeration
- Anonymous FTP Access
- Web Enumeration
- Gobuster Directory Bruteforcing
- Source Code Analysis
- Information Disclosure Discovery
- Steganography Analysis
- Steghide Usage
- Password Auditing
- Hydra Brute Force
- SSH Enumeration
- SSH Key Abuse
- Lateral Movement
- Linux Privilege Escalation
- Sudo Enumeration
- GTFOBins Techniques
- Post Exploitation

## Tools Used

- arp-scan
- Nmap
- Gobuster
- FTP
- Steghide
- Hydra
- SSH
- Linux Commands
- GTFOBins
- Kali Linux

## Attack Methodology

1. Discover the target machine on the network.
2. Enumerate open services using Nmap.
3. Enumerate web directories with Gobuster.
4. Inspect page source code for hidden information.
5. Discover secret directories and hidden keys.
6. Access FTP anonymously and download exposed files.
7. Extract hidden information from images using Steghide.
8. Identify valid usernames.
9. Perform SSH password auditing with Hydra.
10. Obtain initial shell access.
11. Enumerate local users and directories.
12. Abuse SSH key trust relationships for lateral movement.
13. Enumerate sudo permissions.
14. Exploit misconfigured sudo privileges.
15. Escalate privileges to root.
16. Capture all flags.

## Key Learning Outcomes

- Hidden information can often be found in source code comments.
- Directory enumeration remains a critical step during reconnaissance.
- Anonymous FTP access can expose sensitive files.
- Steganography may be used to hide credentials and clues.
- Weak passwords significantly increase attack surface.
- SSH key misconfigurations can enable lateral movement.
- Misconfigured sudo permissions frequently lead to full system compromise.
- Proper privilege separation is essential for Linux security.

## Vulnerabilities Identified

- Information Disclosure
- Hidden Sensitive Data in Source Code
- Anonymous FTP Access Enabled
- Weak User Password
- Credential Exposure via Steganography
- Insecure SSH Key Trust Relationship
- Misconfigured Sudo Permissions
- Privilege Escalation via Perl

## Security Recommendations

- Disable anonymous FTP access.
- Avoid storing sensitive information within publicly accessible files.
- Remove sensitive comments from source code.
- Enforce strong password policies.
- Implement account lockout protections.
- Audit SSH key trust relationships.
- Restrict user-to-user access permissions.
- Review sudo configurations regularly.
- Apply the Principle of Least Privilege.

## Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

**MoneyBox_1_Walkthrough.pdf**

## Attack Chain Summary

- Network Discovery using arp-scan
- Service Enumeration using Nmap
- Directory Enumeration using Gobuster
- Hidden Directory Discovery via Source Code Inspection
- Anonymous FTP Access
- Steganography-Based Credential Discovery
- SSH Password Attack with Hydra
- Initial Access as User renu
- Lateral Movement to User lily
- Sudo Enumeration
- Perl Privilege Escalation
- Root Access and Flag Retrieval

## Highlights

### Enumeration Findings

- FTP service with anonymous login enabled
- SSH service exposed
- Apache web server running
- Hidden directories discovered through source code comments
- Secret key disclosure in web content

### Initial Access

- Username obtained from hidden steganographic content
- Password discovered through Hydra brute-force attack
- SSH access achieved as user **renu**

### Lateral Movement

- SSH key trust relationship enabled access to another user account (**lily**) without requiring credentials. :contentReference[oaicite:1]{index=1}

### Privilege Escalation

The sudo configuration allowed execution of:

```bash
/usr/bin/perl
```

without requiring a password:

```bash
sudo perl -e 'exec "/bin/sh";'
```

This resulted in immediate root access. :contentReference[oaicite:2]{index=2}

## Technical Highlights

- Gobuster Directory Discovery
- Hidden Source Code Comments
- FTP Enumeration
- Steghide Extraction
- Hydra SSH Brute Force
- SSH Key Abuse
- Linux Enumeration
- Sudo Misconfiguration Exploitation
- Perl GTFOBins Privilege Escalation

## Disclaimer

This walkthrough was conducted in a controlled laboratory environment using an intentionally vulnerable machine provided by VulnHub. The content is intended solely for educational purposes, cybersecurity research, penetration testing practice, and ethical hacking training.

---

**Author:** Omkar Babaji Sawant  
**Repository:** VulnHub-Walkthroughs
