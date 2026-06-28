# Toppo: 1 (VulnHub)

## Overview

**Toppo: 1** is an Easy-level VulnHub machine created by **Hadi Mene**. The machine focuses on web enumeration, directory brute forcing, information disclosure, credential discovery, SSH access, Linux enumeration, and privilege escalation through a misconfigured SUID-enabled Python binary. The objective is to obtain root access by exploiting exposed credentials and abusing an insecure SUID configuration. 

---

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | Toppo: 1 |
| Author | Hadi Mene |
| Series | Toppo |
| Platform | VulnHub |
| Release Date | 12 July 2018 |
| Difficulty | Easy |
| Target OS | Linux |
| Category | Web Enumeration, Credential Discovery, SUID Privilege Escalation |

---

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- Web Enumeration
- Directory Brute Forcing
- Information Disclosure
- Credential Discovery
- SSH Authentication
- Linux Enumeration
- SUID Enumeration
- Python Privilege Escalation
- GTFOBins Exploitation
- Post Exploitation

---

## Tools Used

- Netdiscover
- Nmap
- Gobuster
- SSH
- Linux Enumeration Commands
- GTFOBins

---

## Attack Methodology

1. Network Discovery
2. Port Enumeration
3. Website Enumeration
4. Directory Enumeration
5. Information Disclosure
6. SSH Access
7. User Enumeration
8. SUID Enumeration
9. Privilege Escalation
10. Root Access
11. Flag Retrieval

---

## Network Discovery

Identify active hosts on the local network.

```bash
sudo netdiscover -i eth0
```

### Result

```text
192.168.10.12
```

Target successfully identified. 

---

## Port Scanning

Enumerate open ports and running services.

```bash
sudo nmap -sC -sV 192.168.10.12 --min-rate 10000
```

### Open Ports

| Port | Service |
|--------|---------|
| 22 | SSH |
| 80 | HTTP |
| 111 | RPCBind |

### Interesting Findings

```text
SSH service available
Apache web server running
RPC service exposed
```

The web application appears to be the primary attack surface. 

---

## Website Enumeration

Browse to the web server.

```text
http://192.168.10.12
```

The website hosts a Bootstrap-based blog page with no useful information exposed in the source code. 

---

## Directory Enumeration

Perform directory brute forcing.

```bash
gobuster dir -u http://192.168.10.12/ -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -x php,html,txt,old,bak
```

### Interesting Findings

```text
/admin
/mail
/manual
/LICENSE
```

The `/admin` directory contains valuable information. 

---

## Information Disclosure

Browse to:

```text
http://192.168.10.12/admin
```

A file named:

```text
notes.txt
```

contains sensitive information.

### Password Discovered

```text
12345ted123
```

The note also strongly suggests the username:

```text
ted
```

This exposed credential enables SSH authentication. 

---

## SSH Access

Authenticate using the discovered credentials.

```bash
ssh ted@192.168.10.12
```

### Credentials

```text
Username: ted
Password: 12345ted123
```

Verify access.

```bash
whoami
```

### Output

```text
ted
```

Initial foothold successfully obtained. 

---

## User Enumeration

Inspect the user's home directory.

```bash
ls -la
```

Interesting files:

```text
.bash_history
.bashrc
.profile
```

Review the command history.

```bash
cat .bash_history
```

No useful information is discovered. 

---

## SUID Enumeration

Search for SUID binaries.

```bash
find / -perm -4000 2>/dev/null
```

### Interesting Finding

```text
/usr/bin/python2.7
```

Python should not normally possess the SUID permission bit, making it an ideal privilege escalation vector. 

---

## Privilege Escalation

Abuse the SUID-enabled Python binary to obtain a root shell.

Verify privileges.

```text
uid=1000(ted)
gid=1000(ted)
euid=0(root)
```

Confirm root access.

```bash
whoami
```

### Output

```text
root
```

Root privileges successfully obtained. 

---

## Capture the Flag

Navigate to the root directory.

```bash
cd /root
ls
```

### Flag File

```text
flag.txt
```

### Final Flag

```text
0wnedlab{p4ssi0n_c0me_with_pract1ce}
```

---

## Vulnerabilities Identified

### Information Disclosure

A sensitive note containing credentials was exposed through the web server.

### Weak Credential Management

User credentials were stored in plaintext and publicly accessible.

### Directory Enumeration

Hidden administrative directories exposed sensitive information.

### Dangerous SUID Configuration

A SUID-enabled Python binary allowed privilege escalation to root.

### GTFOBins Abuse

The Python binary could be abused to execute commands with elevated privileges. 

---

## Attack Chain Summary

```text
Network Discovery
        ↓
Port Enumeration
        ↓
Website Enumeration
        ↓
Directory Enumeration
        ↓
Information Disclosure
        ↓
Credential Discovery
        ↓
SSH Access
        ↓
User Enumeration
        ↓
SUID Enumeration
        ↓
Python Privilege Escalation
        ↓
Root Access
        ↓
Capture the Flag
```

---

## Security Recommendations

- Disable directory listing on web servers.
- Avoid storing credentials in plaintext.
- Restrict access to administrative directories.
- Remove unnecessary SUID permissions.
- Audit privileged binaries regularly.
- Implement strong password policies.
- Conduct regular security assessments.
- Apply the principle of least privilege.
- Monitor authentication attempts.
- Harden Linux system configurations.

---

## Flags Retrieved

### Final Flag

```text
0wnedlab{p4ssi0n_c0me_with_pract1ce}
```

---

## Key Learning Outcomes

- Web Enumeration Techniques
- Directory Brute Forcing
- Information Disclosure Exploitation
- Credential Discovery
- SSH Authentication
- Linux Enumeration
- SUID Enumeration
- Python Privilege Escalation
- GTFOBins Methodology
- Linux Privilege Escalation Fundamentals

---

## Conclusion

Toppo: 1 is an excellent beginner-friendly VulnHub machine that demonstrates how exposed credentials and insecure SUID configurations can lead to complete system compromise. The challenge provides hands-on experience with web enumeration, directory brute forcing, SSH access, Linux privilege escalation, and GTFOBins techniques, making it an ideal lab for aspiring penetration testers. 

---

**Author:** Omkar Babaji Sawant  
**Repository:** VulnHub-Walkthroughs
