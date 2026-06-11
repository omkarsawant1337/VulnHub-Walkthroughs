# CyberSploit: 2 (VulnHub)

## Overview

**CyberSploit: 2** is an easy-level VulnHub machine designed to test enumeration, web application analysis, credential discovery, Linux privilege escalation, and Docker security concepts. The challenge demonstrates how weakly protected information and improper privilege assignments can lead to full system compromise.

## Machine Information

| Attribute   | Value                                               |
| ----------- | --------------------------------------------------- |
| Platform    | VulnHub                                             |
| Machine     | CyberSploit: 2                                      |
| Author      | CyberSploit                                         |
| Target OS   | CentOS Linux                                        |
| Difficulty  | Easy                                                |
| Attacker OS | Kali Linux                                          |
| Objective   | Gain Initial Access and Escalate Privileges to Root |

## Skills Demonstrated

* Network Discovery
* Service Enumeration
* Web Application Analysis
* Source Code Review
* Credential Discovery
* Encoding & Decoding Techniques
* SSH Authentication
* Linux Enumeration
* Docker Enumeration
* Privilege Escalation
* GTFOBins Research
* Post-Exploitation

## Tools Used

* Netdiscover
* Nmap
* SSH
* Docker
* GTFOBins
* ROT47 Decoder
* Kali Linux

## Attack Methodology

1. Discover the target system on the network.
2. Enumerate open ports and services.
3. Analyze the web application.
4. Inspect page source code for hidden information.
5. Decode obfuscated credentials.
6. Gain initial access through SSH.
7. Perform local enumeration.
8. Identify Docker-related privilege escalation opportunities.
9. Exploit Docker group permissions.
10. Obtain root access and validate system compromise.

## Key Learning Outcomes

* Weak obfuscation is not a substitute for security.
* Source code comments can expose sensitive information.
* Proper user privilege management is critical.
* Docker group membership can provide root-equivalent access.
* Enumeration remains one of the most important phases of penetration testing.
* Misconfigurations often create easier attack paths than software vulnerabilities.

## Security Recommendations

* Never store credentials within web applications or source code.
* Remove sensitive comments from production environments.
* Apply the principle of least privilege.
* Restrict Docker access to trusted administrators only.
* Regularly audit user groups and permissions.
* Conduct security reviews of web applications before deployment.
* Monitor and log privileged operations.

## Walkthrough

📄 Detailed Proof of Concept (PoC) report available in:

**CyberSploit_2_Walkthrough.pdf**

## Disclaimer

This walkthrough was performed in a legal lab environment using an intentionally vulnerable VulnHub machine. The content is provided solely for educational, research, and ethical hacking purposes.

---

**Author:** Omkar Babaji Sawant
**Repository:** VulnHub-Walkthroughs
