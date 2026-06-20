# Masashi: 1 (VulnHub)

## Overview

**Masashi: 1** is an easy-level VulnHub machine created by **Sv5 Donald** that focuses on enumeration, hidden clues, alternative protocols, password discovery using CeWL, SSH access, and Linux privilege escalation through a misconfigured sudo rule. The challenge emphasizes the importance of manual enumeration, inspecting robots.txt, discovering UDP services, and leveraging GTFOBins during privilege escalation. 

## Machine Information

| Attribute | Value |
|------------|---------|
| Platform | VulnHub |
| Machine | Masashi: 1 |
| Author | Sv5 Donald |
| Series | Masashi |
| Difficulty | Easy |
| Release Date | 13 November 2020 |
| Target OS | Debian Linux |
| Attacker OS | Kali Linux |
| Objective | Gain Initial Access and Escalate Privileges to Root |

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- TCP Enumeration
- UDP Enumeration
- Nmap Scanning
- Directory Enumeration
- DIRB Enumeration
- Robots.txt Analysis
- Information Disclosure Assessment
- TFTP Enumeration
- Password Intelligence Gathering
- CeWL Wordlist Generation
- Hydra Password Attacks
- SSH Authentication
- Linux Enumeration
- Sudo Enumeration
- GTFOBins Exploitation
- Linux Privilege Escalation
- Post-Exploitation

## Tools Used

- Netdiscover
- Nmap
- DIRB
- TFTP Client
- CeWL
- Hydra
- SSH
- GTFOBins
- Kali Linux

## Attack Methodology

1. Discover the target machine on the local network.
2. Enumerate open services using Nmap.
3. Perform web directory enumeration.
4. Analyze robots.txt for hidden resources.
5. Identify exposed text files containing sensitive information.
6. Discover the TFTP service running on UDP port 1337.
7. Download files exposed through TFTP.
8. Analyze retrieved files and identify hidden hints.
9. Generate a custom password list using CeWL.
10. Perform SSH password auditing using Hydra.
11. Obtain valid SSH credentials.
12. Gain initial access through SSH.
13. Enumerate sudo permissions.
14. Abuse insecure sudo permissions using GTFOBins.
15. Escalate privileges to root.
16. Capture the root flag.

## Key Learning Outcomes

- Manual inspection is often more valuable than automated scanning.
- robots.txt files may expose sensitive resources.
- UDP services should never be ignored during enumeration.
- Publicly accessible information can lead to full compromise.
- Custom wordlists can be highly effective against weak passwords.
- GTFOBins provides valuable privilege escalation techniques.
- Misconfigured sudo permissions frequently result in root compromise.
- Thorough enumeration is critical during penetration testing engagements.

## Vulnerabilities Identified

- Information Disclosure via robots.txt
- Exposure of Sensitive Files
- TFTP Misconfiguration
- Anonymous File Access
- Weak Password Security
- Predictable Password Generation
- Insecure Service Configuration
- Dangerous Sudo Permissions
- Privilege Escalation via GTFOBins

## Security Recommendations

- Avoid exposing sensitive information through robots.txt.
- Restrict access to internal documentation and configuration files.
- Disable unnecessary services such as publicly accessible TFTP.
- Implement proper authentication controls.
- Enforce strong password policies.
- Monitor authentication attempts and brute-force attacks.
- Apply the Principle of Least Privilege.
- Regularly audit sudo permissions.
- Conduct periodic security assessments and penetration tests.

## Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

**Masashi_1_Walkthrough.pdf**

## Attack Chain Summary

- Network Discovery using Netdiscover
- Service Enumeration with Nmap
- Directory Enumeration using DIRB
- Hidden Resource Discovery through robots.txt
- TFTP Service Identification
- Retrieval of Exposed Files
- CeWL Wordlist Generation
- SSH Password Attack with Hydra
- Initial Access through SSH
- Sudo Enumeration
- GTFOBins Exploitation using Vi
- Root Privilege Escalation
- Flag Retrieval

## Highlights

### Enumeration Findings

- SSH service exposed
- Apache web server running
- Hidden resources discovered in robots.txt
- TFTP service identified on UDP port 1337
- Username disclosure through exposed files

### Initial Access

- Username discovered through exposed files
- Custom wordlist generated using CeWL
- SSH credentials obtained through Hydra password attack

### Privilege Escalation

A misconfigured sudo rule allowed execution of:

```bash
/usr/bin/vi /tmp/*
```

as root without requiring a password, resulting in immediate privilege escalation through a known GTFOBins technique.

## Disclaimer

This walkthrough was performed in a controlled lab environment using an intentionally vulnerable machine provided by VulnHub. The content is intended solely for educational purposes, cybersecurity training, and ethical hacking practice.

---

**Author:** Omkar Babaji Sawant  
**Repository:** VulnHub-Walkthroughs
