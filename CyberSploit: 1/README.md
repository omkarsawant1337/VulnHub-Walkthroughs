# CyberSploit: 1 (VulnHub)

## Overview

**CyberSploit: 1** is a beginner-friendly Capture The Flag (CTF) machine from VulnHub that focuses on web enumeration, information disclosure, credential discovery, SSH access, Linux privilege escalation, and post-exploitation techniques.

The objective is to identify hidden attack vectors, obtain user access, escalate privileges, and retrieve all challenge flags.

## Machine Information

| Attribute   | Value                                  |
| ----------- | -------------------------------------- |
| Platform    | VulnHub                                |
| Machine     | CyberSploit: 1                         |
| Difficulty  | Beginner                               |
| Attacker OS | Kali Linux                             |
| Target OS   | Ubuntu Linux                           |
| Objective   | Gain Root Access and Capture All Flags |

## Skills Demonstrated

* Network Discovery
* Nmap Enumeration
* Web Application Enumeration
* Directory Brute Forcing
* Information Disclosure Analysis
* Source Code Review
* Base64 Decoding
* SSH Enumeration
* Linux Enumeration
* Local Privilege Escalation
* Kernel Exploitation
* Post-Exploitation
* Capture The Flag (CTF) Methodology

## Tools Used

* Nmap
* ARP-Scan
* DIRB
* SSH
* Exploit-DB
* GCC
* Kali Linux

## Attack Methodology

1. Discover the target system on the network.
2. Enumerate services and identify attack surfaces.
3. Perform web application reconnaissance.
4. Discover hidden files and directories.
5. Analyze exposed information and credentials.
6. Gain initial access via SSH.
7. Enumerate the Linux environment.
8. Identify privilege escalation opportunities.
9. Exploit a vulnerable kernel configuration.
10. Obtain root access and complete the challenge.

## Key Learning Outcomes

* Hidden information in web applications can lead to compromise.
* Proper enumeration is critical during penetration testing.
* Exposed credentials create significant security risks.
* Outdated systems are vulnerable to privilege escalation attacks.
* Defense-in-depth is essential for securing Linux environments.
* Regular patch management reduces exploitation opportunities.

## Security Recommendations

* Remove sensitive information from source code and web files.
* Restrict access to unnecessary resources and directories.
* Enforce secure authentication practices.
* Regularly patch operating systems and applications.
* Harden SSH configurations.
* Implement system monitoring and intrusion detection.
* Apply the principle of least privilege.

## Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

**CyberSploit_1_Walkthrough.pdf**

## Disclaimer

This walkthrough was completed in a controlled lab environment using an intentionally vulnerable machine provided by VulnHub. The content is intended for educational and ethical cybersecurity learning purposes only.

---

**Author:** Omkar Babaji Sawant
**Repository:** VulnHub-Walkthroughs
