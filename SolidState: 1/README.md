# SolidState: 1 (VulnHub)

## Overview

**SolidState: 1** is an Easy-level VulnHub machine created by **Ch33z_plz**. The machine focuses on mail server enumeration, credential harvesting, POP3 mailbox analysis, SSH access, and Linux privilege escalation through a writable scheduled Python script.

The challenge demonstrates how weak administrative credentials, insecure password reset functionality, sensitive information disclosure, and writable privileged scripts can be chained together to achieve complete system compromise.

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | SolidState: 1 |
| Author | Ch33z_plz |
| Platform | VulnHub |
| Release Date | 12 September 2018 |
| Difficulty | Easy |
| Target OS | Debian Linux |
| Category | Mail Server Enumeration, Credential Harvesting, Privilege Escalation |
| Objective | Obtain User and Root Access |

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- Nmap Scanning
- Mail Server Enumeration
- JAMES Administration Enumeration
- POP3 Enumeration
- Credential Harvesting
- Password Reset Abuse
- Email Analysis
- SSH Authentication
- Linux Enumeration
- Scheduled Task Enumeration
- Writable Script Abuse
- Privilege Escalation
- Post Exploitation

## Tools Used

- Netdiscover
- Nmap
- Netcat
- POP3
- SSH
- Linux Enumeration Commands
- Python
- Kali Linux

## Attack Methodology

1. Discover the target machine on the network.
2. Enumerate open ports and services.
3. Identify JAMES Mail Server.
4. Access the JAMES administration interface.
5. Abuse default administrative credentials.
6. Reset mailbox user passwords.
7. Enumerate POP3 mailboxes.
8. Recover SSH credentials from emails.
9. Gain SSH access as user mindy.
10. Enumerate the filesystem.
11. Discover writable scheduled script.
12. Modify script execution flow.
13. Obtain root shell.
14. Capture root flag.

## Open Services Identified

| Port | Service |
|--------|---------|
| 22 | SSH |
| 25 | SMTP |
| 80 | HTTP |
| 110 | POP3 |
| 119 | NNTP |
| 4555 | JAMES Remote Administration |

### Key Findings

- JAMES Mail Server 2.3.2 exposed.
- JAMES Remote Administration accessible.
- Default administrative credentials enabled.
- POP3 mailboxes accessible after password reset.
- Sensitive credentials stored in email messages.
- Writable privileged script present in `/opt`. 

## Vulnerabilities Identified

### 1. Weak Administrative Credentials

JAMES administration service accepted:

```text
Username: root
Password: root
```

allowing unauthorized administrative access. 

### 2. Password Reset Abuse

The administration interface allowed arbitrary password resets:

```text
setpassword james james
setpassword thomas thomas
setpassword john john
setpassword mindy mindy
```

without additional verification. 

### 3. Sensitive Information Disclosure

User mailboxes contained internal credentials.

Recovered from email:

```text
username: mindy
password: P@55W0rd1!2@
```

allowing direct SSH authentication. 

### 4. Writable Scheduled Script

The file:

```text
/opt/tmp.py
```

was writable by a low-privileged user and executed by a privileged process, leading directly to root compromise. 

## Service Enumeration

### JAMES Administration Access

Connect to the administrative service:

```bash
nc <target-ip> 4555
```

Authenticate using default credentials:

```text
root : root
```

Successful access provides administrative control over user accounts. 

### User Enumeration

List available users:

```text
james
thomas
john
mindy
mailadmin
```

Administrative access allows password resets for each account. 

## Initial Access

### POP3 Mailbox Enumeration

Connect to POP3:

```bash
nc -C <target-ip> 110
```

After resetting user passwords, mailbox contents become accessible.

Reviewing Mindy's mailbox revealed SSH credentials. 

### SSH Access

Authenticate using the discovered credentials:

```bash
ssh mindy@<target-ip>
```

Verify access:

```bash
whoami
```

Output:

```text
mindy
```

User-level access successfully obtained. 

## Privilege Escalation

### System Enumeration

Exploring `/opt` revealed:

```text
james-2.3.2
tmp.py
```

The script appeared to be executed automatically and was writable by the current user. 

### Script Review

The script originally contained:

```python
#!/usr/bin/env python
import os
import sys
try:
    os.system('rm -r /tmp/*')
except:
    sys.exit()
```

It periodically cleaned the `/tmp` directory. 

### Exploitation

Because the script was writable and executed with elevated privileges, modifying it allowed arbitrary command execution as root.

After replacing the original logic and waiting for the scheduled execution, a root shell was obtained. 

### Root Verification

```bash
id
```

Output:

```text
uid=0(root) gid=0(root)
```

Root access successfully achieved. 

## Attack Chain Summary

- Network Discovery
- Service Enumeration
- JAMES Mail Server Discovery
- JAMES Administrative Access
- Password Reset Abuse
- POP3 Enumeration
- Mailbox Analysis
- SSH Credential Discovery
- SSH Login as mindy
- Writable Script Discovery
- Scheduled Task Abuse
- Root Shell Access
- Root Flag Retrieval

## Security Recommendations

- Disable default administrative credentials.
- Restrict access to mail administration interfaces.
- Implement strong authentication controls.
- Require authorization checks for password resets.
- Avoid storing sensitive credentials in email.
- Restrict access permissions on scheduled scripts.
- Apply Principle of Least Privilege.
- Monitor administrative account activity.
- Audit scheduled tasks regularly.
- Perform periodic vulnerability assessments.

## Key Learning Outcomes

- Mail services often expose valuable attack paths.
- Administrative interfaces should never use default credentials.
- Password reset functionality must be properly secured.
- Internal emails frequently contain sensitive information.
- Thorough service enumeration is critical during assessments.
- Scheduled tasks should never execute writable files.
- Multiple low-risk findings can combine into full system compromise.

## Flags

### User Flag

```text
914d0a4ebc1777889b5b89a23f556fd75
```

### Root Flag

```text
b4c9723a28899b1c45db281d99cc87c9
```

## Conclusion

SolidState: 1 is an excellent beginner-to-intermediate VulnHub machine that teaches the importance of mail server enumeration, POP3 analysis, credential harvesting, and privilege escalation through scheduled task abuse. The machine demonstrates how several small misconfigurations can ultimately result in complete system compromise. 

---

**Author:** Omkar Babaji Sawant  
**Repository:** VulnHub-Walkthroughs
