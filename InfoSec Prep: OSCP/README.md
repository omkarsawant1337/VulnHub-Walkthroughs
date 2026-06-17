# InfoSec Prep: OSCP (VulnHub)

## Overview

**InfoSec Prep: OSCP** is a beginner-friendly VulnHub machine that focuses on web enumeration, WordPress reconnaissance, information disclosure, encoded data analysis, SSH key authentication, and Linux privilege escalation through SUID misconfiguration.

The challenge demonstrates how exposed sensitive data, weak operational security practices, and improper privilege configurations can be chained together to achieve full system compromise. :contentReference[oaicite:0]{index=0}

## Machine Information

| Attribute | Value |
|------------|---------|
| Platform | VulnHub |
| Machine | InfoSec Prep: OSCP |
| Author | FalconSpy |
| Series | InfoSec Prep |
| Difficulty | Easy |
| Target OS | Ubuntu Linux |
| Attacker OS | Kali Linux |
| Objective | Gain Initial Access and Escalate Privileges to Root |

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- Nmap Scanning
- Web Application Enumeration
- WordPress Reconnaissance
- Robots.txt Analysis
- Directory Enumeration
- Gobuster Usage
- Information Disclosure Analysis
- Base64 Decoding
- SSH Private Key Analysis
- SSH Authentication
- Linux Enumeration
- SUID Enumeration
- GTFOBins Research
- Linux Privilege Escalation
- Post-Exploitation

## Tools Used

- Netdiscover
- Nmap
- Gobuster
- CyberChef
- SSH
- GTFOBins
- Linux Enumeration Commands
- Kali Linux

## Attack Methodology

1. Discover the target machine on the local network.
2. Enumerate open ports and running services.
3. Identify the WordPress application.
4. Analyze robots.txt for hidden resources.
5. Discover sensitive files through directory enumeration.
6. Identify encoded information disclosure.
7. Decode exposed Base64 content.
8. Recover an SSH private key.
9. Authenticate via SSH using the recovered key.
10. Perform local Linux enumeration.
11. Enumerate SUID binaries.
12. Identify a misconfigured privileged executable.
13. Escalate privileges to root.
14. Validate compromise and retrieve proof.

## Key Learning Outcomes

- Robots.txt files can unintentionally expose sensitive resources.
- Information disclosure vulnerabilities often provide critical attack paths.
- Base64 encoding should never be considered a security control.
- Exposed SSH private keys can result in immediate system compromise.
- Enumeration is one of the most important phases of penetration testing.
- Misconfigured SUID binaries present serious privilege escalation risks.
- Proper privilege separation is essential for Linux system security.

## Vulnerabilities Identified

- Sensitive Information Disclosure
- Exposed Hidden Resources
- SSH Private Key Exposure
- Weak Operational Security Practices
- Improper Access Controls
- Misconfigured SUID Permissions
- Privilege Escalation via SUID Bash
- Inadequate Security Hardening

## Security Recommendations

- Avoid exposing sensitive files through web directories.
- Regularly review robots.txt for unintended disclosures.
- Store SSH private keys securely and never expose them publicly.
- Implement proper file permission management.
- Conduct regular security audits of SUID binaries.
- Apply the principle of least privilege.
- Monitor systems for unauthorized privilege escalation attempts.
- Perform routine vulnerability assessments and penetration testing.

## Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

**InfoSec_Prep_OSCP_Walkthrough.pdf**

## Disclaimer

This walkthrough was completed in a controlled lab environment using an intentionally vulnerable machine provided by VulnHub. The content is intended solely for educational purposes, cybersecurity training, and ethical hacking practice.

---

**Author:** Omkar Babaji Sawant  
**Repository:** VulnHub-Walkthroughs
