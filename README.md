<div align="center">

# 🛡️ VulnHub Walkthrough

**A professional penetration testing knowledge base documenting real-world attack techniques, vulnerability research, and offensive security methodologies on VulnHub machines.**

[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-VulnHub-orange?style=flat-square)](https://www.vulnhub.com/)
[![Purpose](https://img.shields.io/badge/Purpose-Ethical%20Hacking-red?style=flat-square)](https://github.com/omkarsawant1337/VulnHub-Walkthroughs)
[![Machines](https://img.shields.io/badge/Machines%20Completed-17-blueviolet?style=flat-square)](https://github.com/omkarsawant1337/VulnHub-Walkthroughs)
[![Methodology](https://img.shields.io/badge/Methodology-PTES%20%7C%20OWASP-blue?style=flat-square)](https://github.com/omkarsawant1337/VulnHub-Walkthroughs)

> All walkthroughs are conducted in isolated, authorized lab environments strictly for educational and research purposes.

</div>

---

## 📌 Overview

This repository is a hands-on penetration testing portfolio covering end-to-end attack chains against intentionally vulnerable VulnHub machines. Each walkthrough follows a structured methodology — from initial reconnaissance and enumeration through exploitation, privilege escalation, and professional reporting — mirroring real-world penetration testing engagements.

**Who this is for:** Ethical hackers, OSCP candidates, CTF players, security analysts, bug bounty hunters, red team practitioners, and cybersecurity students looking for practical, documented offensive security techniques.

---

## 🗂️ Repository Structure

```
VulnHub-Walkthroughs/
│
├── Basic Pentesting: 1/
│   ├── README.md                              # Full walkthrough writeup
│   └── Basic_Pentesting_1_Walkthrough...       # Detailed walkthrough document
│
└── Basic Pentesting: 2/
    ├── README.md                              # Full walkthrough writeup
    └── Basic_Pentesting_2_Walkthrough...       # Detailed walkthrough document
```

> More machines will be added progressively as walkthroughs are completed.

---

## 🔍 Methodology Phases

Each machine walkthrough follows the industry-standard penetration testing lifecycle:

### Phase 1 — Reconnaissance & Enumeration

Active and passive information gathering to map the attack surface.

- Network discovery and host identification with **Netdiscover** and **Nmap**
- Full port scanning with service version detection and OS fingerprinting
- Directory and file enumeration using **Gobuster** and **Dirbuster**
- Subdomain enumeration and DNS reconnaissance
- Web application fingerprinting and technology stack identification
- OSINT and metadata analysis

### Phase 2 — Web Application Security Testing

Assessment aligned with the **OWASP Top 10** and beyond.

| Vulnerability Class | Techniques Covered |
|---|---|
| Injection | SQL Injection (SQLi), Command Injection |
| XSS | Reflected, Stored, DOM-based Cross-Site Scripting |
| File Handling | Unrestricted File Upload, Directory Traversal, Path Traversal |
| Access Control | Authentication Bypass, IDOR, Broken Authorization |
| File Inclusion | Local File Inclusion (LFI), Remote File Inclusion (RFI) |
| Configuration | Security Misconfigurations, Default Credentials, Exposed Endpoints |

### Phase 3 — Exploitation & Initial Access

Turning identified vulnerabilities into verified, reproducible access.

- Manual and **Metasploit Framework**-assisted exploitation
- Reverse shell generation and payload deployment (bash, Python, PHP, netcat)
- Credential attacks with **Hydra** and **John the Ripper**
- **SQLMap** for automated SQL injection exploitation
- **Burp Suite** for web application interception and manipulation
- Custom exploit adaptation for version-specific vulnerabilities

### Phase 4 — Privilege Escalation

Systematic escalation from low-privilege shell to root/SYSTEM.

- SUID/SGID binary abuse and GTFOBins exploitation
- Cron job hijacking and writable script injection
- Weak file permissions on sensitive configuration files
- Kernel vulnerability identification and safe exploitation
- Sudo misconfigurations and policy bypass
- Credential harvesting from config files, history, and environment variables
- Lateral movement fundamentals and pivoting concepts

### Phase 5 — Post-Exploitation & Reporting

Structured documentation following professional pentesting standards.

- Proof of Concept (PoC) documentation with step-by-step reproduction
- Screenshot evidence and command output capture
- Vulnerability impact analysis (CIA triad)
- CVSS scoring and risk prioritization
- Remediation recommendations and developer-friendly fixes
- Professional penetration testing report templates

---

## 🛠️ Tools & Technologies

<table>
<tr>
<td valign="top" width="50%">

**Reconnaissance**
- Nmap — Port scanning, service detection
- Netdiscover — Network host discovery
- Gobuster — Directory and DNS brute-forcing
- WhatWeb / Wappalyzer — Web fingerprinting

**Exploitation**
- Metasploit Framework — Exploit automation
- Burp Suite — Web proxy and vulnerability scanner
- SQLMap — SQL injection automation
- Hydra — Online credential brute-forcing

</td>
<td valign="top" width="50%">

**Analysis**
- Wireshark — Packet capture and protocol analysis
- Netcat — Reverse/bind shells, port forwarding
- John the Ripper / Hashcat — Password cracking

**Privilege Escalation**
- LinPEAS / LinEnum — Linux enumeration scripts
- GTFOBins — SUID/sudo binary exploitation
- pspy — Unprivileged process monitoring
- Custom Bash / Python scripts

</td>
</tr>
</table>

---

## 📊 Skills Demonstrated

```
Penetration Testing Lifecycle     ████████████████████  100%
Linux Privilege Escalation        ███████████████████░  95%
Web Application Security (OWASP)  ███████████████████░  95%
Network Enumeration & Scanning    ████████████████████  100%
Exploit Development & Adaptation  ████████████████░░░░  80%
Security Report Writing           ███████████████████░  95%
Packet Analysis (Wireshark)       ████████████████░░░░  80%
```

---

## 📝 Walkthrough Format

Every machine writeup follows a consistent, readable format designed for both learning and professional reference:

```markdown
# Machine Name — VulnHub Walkthrough

## Summary
## Environment Setup
## Phase 1: Reconnaissance
## Phase 2: Enumeration
## Phase 3: Exploitation
## Phase 4: Privilege Escalation
## Phase 5: Post-Exploitation
## Flags
## Vulnerability Analysis & Remediation
## Key Takeaways
```

---

## 🎯 Learning Objectives

This repository is a practical reference for:

- **OSCP / CEH / eJPT candidates** preparing for certification exams
- **CTF players** seeking structured VulnHub methodology
- **Security analysts** building offensive security knowledge
- **Bug bounty hunters** learning vulnerability chaining techniques
- **Red teamers** practicing initial access and lateral movement
- **Developers** understanding attacker perspective for secure code review

---

## ⚠️ Legal Disclaimer

All techniques, tools, and exploits documented in this repository are used **exclusively against intentionally vulnerable machines** in isolated, controlled lab environments. This content is provided for **educational purposes and authorized security research only**.

Unauthorized use of these techniques against systems you do not own or have explicit written permission to test is **illegal and unethical**. The author assumes no responsibility for misuse of this material.

**Always hack ethically. Always get written authorization.**

---

## 🤝 Contributing

Contributions, suggestions, and improvements are welcome.

1. Fork the repository
2. Create a feature branch (`git checkout -b walkthrough/machine-name`)
3. Commit your changes (`git commit -m 'Add walkthrough for MachineName'`)
4. Push to the branch (`git push origin walkthrough/machine-name`)
5. Open a Pull Request

Please follow the existing walkthrough format and ensure all content is original and ethically obtained.

---

## 📬 Connect

**Omkar Sawant** — Cybersecurity Enthusiast | Penetration Tester | Security Researcher

[![GitHub](https://img.shields.io/badge/GitHub-omkarsawant1337-black?style=flat-square&logo=github)](https://github.com/omkarsawant1337)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/omkar-sawant-37bb5228b)

---

<div align="center">

⭐ **If this repository helped you, please consider starring it — it helps others discover this resource.**

`#EthicalHacking` `#PenetrationTesting` `#VulnHub` `#CTF` `#OSCP` `#OffensiveSecurity` `#CyberSecurity` `#BugBounty` `#RedTeam` `#InfoSec`

</div>
