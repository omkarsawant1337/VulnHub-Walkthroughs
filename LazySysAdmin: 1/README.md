# Lazy SysAdmin: 1 (VulnHub)

## Overview

**Lazy SysAdmin: 1** is a beginner-friendly VulnHub machine that focuses on network enumeration, SMB share assessment, WordPress configuration analysis, credential harvesting, SSH access, and Linux privilege escalation through excessive sudo permissions.

The challenge demonstrates how exposed SMB shares, improperly protected application configuration files, weak credentials, and overly permissive sudo privileges can be chained together to achieve complete system compromise. :contentReference[oaicite:0]{index=0}

## Machine Information

| Attribute | Value |
|------------|---------|
| Platform | VulnHub |
| Machine | Lazy SysAdmin: 1 |
| Author | Togie Mcdogie |
| Series | Lazy SysAdmin |
| Difficulty | Easy |
| Target OS | Ubuntu Linux |
| Attacker OS | Kali Linux |
| Objective | Gain Initial Access and Escalate Privileges to Root |

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- Nmap Scanning
- SMB Enumeration
- SMB Share Assessment
- WordPress Security Assessment
- Directory Enumeration
- Gobuster Usage
- Configuration File Analysis
- Credential Harvesting
- Password Auditing
- Hydra Password Attacks
- SSH Authentication
- Linux Enumeration
- Sudo Enumeration
- Linux Privilege Escalation
- Post-Exploitation

## Tools Used

- ARP-Scan
- Nmap
- Gobuster
- SMBClient
- Hydra
- SSH
- Linux Enumeration Commands
- Kali Linux

## Attack Methodology

1. Discover the target machine on the network.
2. Enumerate open ports and running services.
3. Identify web technologies and hidden resources.
4. Perform directory enumeration against the web application.
5. Enumerate accessible SMB shares.
6. Retrieve sensitive WordPress configuration files.
7. Extract exposed credentials from application files.
8. Perform authentication testing against SSH.
9. Obtain authenticated SSH access.
10. Perform local Linux enumeration.
11. Review sudo permissions.
12. Identify privilege escalation opportunities.
13. Escalate privileges to root.
14. Validate compromise and retrieve proof.

## Key Learning Outcomes

- SMB shares can expose highly sensitive application data.
- WordPress configuration files often contain valuable credentials.
- Weak passwords significantly increase organizational risk.
- Credential reuse can facilitate lateral movement and compromise.
- Excessive sudo privileges can directly lead to root access.
- Enumeration remains one of the most important penetration testing phases.
- Proper access controls and least-privilege principles are critical for system security.

## Vulnerabilities Identified

- Exposed SMB Shares
- Sensitive Configuration File Disclosure
- Credential Exposure
- Weak Password Security
- Insecure Access Controls
- Excessive Sudo Permissions
- Privilege Escalation via Misconfigured Sudo
- Inadequate Security Hardening

## Security Recommendations

- Restrict SMB share access using proper authentication controls.
- Protect application configuration files from unauthorized access.
- Avoid storing sensitive credentials in publicly accessible locations.
- Enforce strong password policies.
- Implement multi-factor authentication for privileged accounts.
- Apply the principle of least privilege.
- Regularly audit sudo permissions and privileged accounts.
- Monitor authentication logs for brute-force attempts.
- Conduct routine vulnerability assessments and security reviews.

## Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

**Lazy_SysAdmin_1_Walkthrough.pdf**

## Disclaimer

This walkthrough was completed in a controlled lab environment using an intentionally vulnerable machine provided by VulnHub. The content is intended solely for educational purposes, cybersecurity training, and ethical hacking practice.

---

**Author:** Omkar Babaji Sawant  
**Repository:** VulnHub-Walkthroughs
