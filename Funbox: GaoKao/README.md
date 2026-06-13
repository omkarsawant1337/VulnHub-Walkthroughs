# Funbox: GaoKao (VulnHub)

## Overview

**Funbox: GaoKao** is an easy-level VulnHub machine that focuses on FTP security assessment, credential attacks, remote code execution, Linux enumeration, and privilege escalation. The challenge demonstrates how multiple weak security controls can be chained together to achieve complete system compromise.

This machine provides practical experience in service enumeration, authentication testing, post-exploitation techniques, and privilege escalation through misconfigured Linux permissions.

## Machine Information

| Attribute   | Value                                               |
| ----------- | --------------------------------------------------- |
| Platform    | VulnHub                                             |
| Machine     | Funbox: GaoKao                                      |
| Author      | 0815R2d2                                            |
| Series      | Funbox                                              |
| Difficulty  | Easy                                                |
| Target OS   | Ubuntu Linux                                        |
| Attacker OS | Kali Linux                                          |
| Objective   | Gain Initial Access and Escalate Privileges to Root |

## Skills Demonstrated

* Network Discovery
* Service Enumeration
* Nmap Scanning
* FTP Security Assessment
* Anonymous FTP Enumeration
* Credential Discovery
* Password Auditing
* Authentication Testing
* Hydra Password Attacks
* Remote Code Execution Analysis
* Reverse Shell Handling
* Linux Enumeration
* SUID Analysis
* Privilege Escalation
* Post-Exploitation

## Tools Used

* Netdiscover
* Nmap
* FTP Client
* Hydra
* Netcat
* Python PTY
* Linux Enumeration Utilities
* Kali Linux

## Attack Methodology

1. Discover the target host on the network.
2. Enumerate open services and technologies.
3. Assess FTP security configuration.
4. Identify exposed usernames and sensitive information.
5. Perform credential security testing.
6. Gain authenticated access.
7. Analyze accessible files and permissions.
8. Obtain remote code execution.
9. Establish and stabilize a shell.
10. Enumerate privilege escalation opportunities.
11. Identify insecure SUID configurations.
12. Escalate privileges to root.
13. Validate compromise and capture proof.

## Key Learning Outcomes

* Anonymous services can expose valuable reconnaissance information.
* User enumeration often assists authentication attacks.
* Weak passwords remain a major security risk.
* Improper file permissions can lead to remote code execution.
* SUID binaries require strict security auditing.
* Linux privilege escalation frequently results from permission misconfigurations.
* Multiple low-severity issues can combine into a critical compromise.

## Vulnerabilities Identified

* Anonymous FTP Access Enabled
* Username Disclosure
* Weak Authentication Controls
* Credential Security Weaknesses
* Writable Executable Files
* Remote Code Execution Opportunity
* Dangerous SUID Configuration
* Privilege Escalation Misconfiguration

## Security Recommendations

* Disable anonymous FTP access unless absolutely necessary.
* Prevent unnecessary information disclosure in service banners.
* Enforce strong password policies and account lockout controls.
* Restrict write permissions on executable files.
* Regularly audit SUID binaries and privileged executables.
* Implement centralized logging and monitoring.
* Apply the principle of least privilege.
* Conduct periodic security reviews and vulnerability assessments.

## Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

**Funbox_GaoKao_Proof_of_Concept.pdf**

## Disclaimer

This walkthrough was completed in a controlled lab environment using an intentionally vulnerable machine provided by VulnHub. The content is intended for educational purposes, cybersecurity training, and ethical hacking practice only.

---

**Author:** Omkar Babaji Sawant
**Repository:** VulnHub-Walkthroughs
