# HackathonCTF: 1 (VulnHub)

## Overview

**HackathonCTF: 1** is a beginner-friendly VulnHub machine created by **Somu Sen** that focuses on web enumeration, information disclosure, credential discovery, SSH brute forcing, password recovery, and Linux privilege escalation through a vulnerable sudo configuration.

The challenge demonstrates how seemingly harmless files such as **robots.txt**, hidden web pages, Bash history files, and improperly stored credentials can be chained together to achieve complete system compromise. :contentReference[oaicite:0]{index=0}

## Machine Information

| Attribute | Value |
|------------|---------|
| Platform | VulnHub |
| Machine | HackathonCTF: 1 |
| Author | Somu Sen |
| Series | HackathonCTF |
| Release Date | 27 October 2020 |
| Difficulty | Easy |
| Target OS | Ubuntu Linux |
| Attacker OS | Kali Linux |
| Objective | Gain Initial Access and Escalate Privileges to Root |

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- Nmap Scanning
- Web Enumeration
- Directory Brute Forcing
- Gobuster Enumeration
- robots.txt Analysis
- Source Code Inspection
- Information Disclosure Analysis
- Base64 Decoding
- Credential Discovery
- Password Recovery
- SSH Enumeration
- Hydra Password Attacks
- SSH Authentication
- Linux Enumeration
- Bash History Analysis
- Sudo Enumeration
- CVE Research
- Linux Privilege Escalation
- Post-Exploitation

## Tools Used

- Netdiscover
- Nmap
- Gobuster
- Hydra
- SSH
- Base64
- Linux Enumeration Commands
- Kali Linux

## Attack Methodology

1. Discover the target machine on the network.
2. Enumerate open ports and running services.
3. Analyze robots.txt for hidden content.
4. Perform directory brute forcing using Gobuster.
5. Discover hidden web pages.
6. Inspect source code for information disclosure.
7. Identify valid usernames.
8. Perform SSH password auditing with Hydra.
9. Obtain initial SSH access.
10. Enumerate Bash history files.
11. Discover hidden credentials.
12. Decode Base64-encoded passwords.
13. Enumerate sudo permissions.
14. Identify vulnerable sudo configuration.
15. Exploit CVE-2019-14287.
16. Escalate privileges to root.
17. Validate compromise and capture proof.

## Key Learning Outcomes

- robots.txt files can unintentionally expose sensitive information.
- Source code comments frequently reveal useful attack vectors.
- Weak passwords significantly increase attack success rates.
- Bash history files often contain sensitive operational data.
- Base64 encoding is not a security control.
- Information disclosure vulnerabilities frequently lead to credential compromise.
- Misconfigured sudo rules can provide direct privilege escalation paths.
- Thorough enumeration remains the most important penetration testing skill.

## Vulnerabilities Identified

- Information Disclosure via robots.txt
- Hidden Web Content Exposure
- Username Disclosure
- Weak SSH Credentials
- Sensitive Data Exposure
- Insecure Credential Storage
- Bash History Information Leakage
- Vulnerable Sudo Configuration
- CVE-2019-14287 Privilege Escalation

## Security Recommendations

- Avoid storing sensitive information in robots.txt.
- Remove sensitive comments from source code.
- Enforce strong password policies.
- Restrict access to sensitive files and directories.
- Avoid storing credentials in plaintext or Base64 format.
- Regularly review Bash history and user artifacts.
- Update vulnerable sudo versions immediately.
- Apply the Principle of Least Privilege.
- Conduct periodic vulnerability assessments and penetration tests.

## Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

**HackathonCTF_1_Walkthrough.pdf**

## Attack Chain Summary

- Network Discovery using Netdiscover
- Service Enumeration with Nmap
- robots.txt Analysis
- Directory Enumeration using Gobuster
- Hidden Page Discovery
- Username Disclosure via Source Code
- SSH Brute Force using Hydra
- Initial SSH Access
- Bash History Enumeration
- Base64 Password Recovery
- Sudo Enumeration
- CVE-2019-14287 Exploitation
- Root Access and Flag Retrieval

## Highlights

### Enumeration Findings

- FTP service exposed
- Telnet service available
- HTTP web application accessible
- SSH running on port 7223
- Hidden directories referenced in robots.txt
- Base64-encoded hint discovered

### Initial Access

- Username recovered from page source code.
- Password discovered through Hydra brute-force attack.
- SSH access obtained as user **test**. :contentReference[oaicite:1]{index=1}

### Credential Discovery

Bash history analysis revealed references to:

```bash
/media/floppy/media/imp
```

A Base64-encoded credential was recovered and decoded, providing additional information useful during the attack chain. :contentReference[oaicite:2]{index=2}

### Privilege Escalation

The sudo configuration allowed:

```bash
(ALL, !root) ALL
```

This vulnerable configuration was exploitable via **CVE-2019-14287**, allowing privilege escalation to root using:

```bash
sudo -u#-1 /bin/bash
```

which bypasses the intended sudo restriction. :contentReference[oaicite:3]{index=3}

## Technical Highlights

- robots.txt Enumeration
- Gobuster Directory Discovery
- Source Code Analysis
- Base64 Decoding
- Hydra SSH Password Auditing
- Bash History Enumeration
- Credential Recovery
- CVE-2019-14287 Exploitation
- Linux Privilege Escalation

## Disclaimer

This walkthrough was conducted in a controlled laboratory environment using an intentionally vulnerable machine provided by VulnHub. The content is intended solely for educational purposes, cybersecurity research, penetration testing practice, and ethical hacking training.

---

**Author:** Omkar Babaji Sawant  
**Repository:** VulnHub-Walkthroughs
