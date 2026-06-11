# EVM (Extremely Vulnerable Machine) - VulnHub

## Overview

**EVM (Extremely Vulnerable Machine)** is a beginner-to-intermediate VulnHub challenge designed to simulate a real-world web application compromise. The machine focuses on WordPress enumeration, vulnerability assessment, credential attacks, authenticated exploitation, post-exploitation activities, and Linux privilege escalation.

This assessment demonstrates the importance of secure web application configuration, strong authentication practices, and proper credential management.

## Machine Information

| Attribute      | Value                                                 |
| -------------- | ----------------------------------------------------- |
| Platform       | VulnHub                                               |
| Machine        | EVM (Extremely Vulnerable Machine)                    |
| Difficulty     | Easy–Medium                                           |
| Target OS      | Ubuntu Linux                                          |
| Attacker OS    | Kali Linux                                            |
| Primary Vector | Vulnerable WordPress Installation                     |
| Objective      | Obtain Initial Access and Escalate Privileges to Root |

## Skills Demonstrated

* Network Discovery
* Service Enumeration
* Nmap Scanning
* Web Application Enumeration
* Directory Enumeration
* WordPress Security Assessment
* WPScan Enumeration
* User Enumeration
* Credential Auditing
* Authentication Testing
* Remote Code Execution Analysis
* Post-Exploitation
* Linux Enumeration
* Privilege Escalation
* Security Assessment Reporting

## Tools Used

* ARP-Scan
* Nmap
* DIRB
* WPScan
* Metasploit Framework
* Meterpreter
* Linux Shell
* Kali Linux

## Attack Methodology

1. Discover the target system on the network.
2. Enumerate open ports and services.
3. Identify web application attack surfaces.
4. Discover and assess the WordPress installation.
5. Perform WordPress user enumeration.
6. Conduct authentication and credential security assessment.
7. Gain authenticated access to the application.
8. Perform post-exploitation enumeration.
9. Identify privilege escalation opportunities.
10. Obtain root-level access.
11. Validate compromise and collect proof.

## Key Learning Outcomes

* Outdated web applications significantly increase risk exposure.
* Weak passwords remain one of the most common attack vectors.
* Directory listing can expose sensitive application resources.
* Proper access controls are critical for administrative interfaces.
* Sensitive credentials should never be stored in plaintext.
* Post-exploitation enumeration is essential for identifying escalation paths.
* Defense-in-depth reduces the impact of individual security failures.

## Vulnerabilities Identified

* Outdated WordPress Installation
* Weak Authentication Controls
* User Enumeration Exposure
* Directory Listing Enabled
* Insecure Credential Storage
* Excessive Privileges
* Security Misconfigurations

## Security Recommendations

* Keep WordPress core, themes, and plugins fully updated.
* Enforce strong password policies and account lockout mechanisms.
* Restrict access to administrative interfaces.
* Disable unnecessary directory listings.
* Remove plaintext credentials from systems.
* Implement centralized logging and monitoring.
* Conduct regular vulnerability assessments and security audits.
* Apply the principle of least privilege across all services.

## Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

**EVM_VulnHub_Machine_Exploitation_Walkthrough.pdf**

## Disclaimer

This walkthrough was completed in a controlled lab environment using an intentionally vulnerable machine provided by VulnHub. The content is intended solely for educational purposes, cybersecurity training, and ethical hacking practice.

---

**Author:** Omkar Babaji Sawant
**Repository:** VulnHub-Walkthroughs
