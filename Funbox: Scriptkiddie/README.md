# Funbox: Scriptkiddie (VulnHub)

## Overview

**Funbox: Scriptkiddie** is an easy-level VulnHub machine that focuses on network enumeration, service discovery, vulnerability assessment, exploit research, and remote code execution through a known backdoored service.

The challenge demonstrates the importance of software supply chain security and how vulnerable or compromised software versions can lead to immediate system compromise.

## Machine Information

| Attribute   | Value                                         |
| ----------- | --------------------------------------------- |
| Platform    | VulnHub                                       |
| Machine     | Funbox: Scriptkiddie                          |
| Author      | 0815R2d2                                      |
| Series      | Funbox                                        |
| Difficulty  | Easy                                          |
| Target OS   | Ubuntu Linux                                  |
| Attacker OS | Kali Linux                                    |
| Objective   | Gain Remote Access and Obtain Root Privileges |

## Skills Demonstrated

* Network Discovery
* Service Enumeration
* Nmap Scanning
* Vulnerability Assessment
* Exploit Research
* SearchSploit Usage
* Metasploit Framework
* Remote Code Execution Analysis
* Exploit Validation
* Linux Post-Exploitation
* Security Misconfiguration Assessment
* Security Reporting

## Tools Used

* ARP-Scan
* Nmap
* SearchSploit
* Metasploit Framework
* Linux Shell
* Kali Linux

## Attack Methodology

1. Discover the target system on the local network.
2. Enumerate open ports and running services.
3. Identify software versions and exposed attack surfaces.
4. Research publicly known vulnerabilities.
5. Validate the existence of a known service vulnerability.
6. Perform controlled exploitation in a lab environment.
7. Obtain remote command execution.
8. Verify privilege level and system access.
9. Conduct post-exploitation validation.
10. Capture proof of compromise.

## Key Learning Outcomes

* Accurate service enumeration is critical during penetration testing.
* Vulnerability research helps identify known attack vectors.
* Outdated and compromised software versions create significant security risks.
* Supply chain attacks can impact trusted software distributions.
* Proper patch management reduces organizational risk.
* Continuous monitoring assists in detecting unauthorized activity.
* Security hardening minimizes attack surface exposure.

## Vulnerabilities Identified

* Vulnerable FTP Service
* Outdated Software Components
* Remote Code Execution Exposure
* Insufficient Service Hardening
* Excessive Service Exposure
* Weak Security Monitoring Controls

## Security Recommendations

* Upgrade vulnerable services to supported versions.
* Remove deprecated or insecure software.
* Restrict unnecessary network services.
* Implement continuous vulnerability management.
* Monitor for suspicious service activity.
* Enforce network segmentation where appropriate.
* Conduct regular penetration testing and security reviews.
* Apply security updates promptly.

## Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

**Funbox_Scriptkiddie_Walkthrough.pdf**

## Disclaimer

This walkthrough was completed in a controlled lab environment using an intentionally vulnerable machine provided by VulnHub. The content is intended solely for educational purposes, cybersecurity training, and ethical hacking practice.

---

**Author:** Omkar Babaji Sawant
**Repository:** VulnHub-Walkthroughs
