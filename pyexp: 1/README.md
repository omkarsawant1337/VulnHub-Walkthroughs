# Pyexp: 1 (VulnHub)

## Overview

**Pyexp: 1** is an Easy-level VulnHub machine created by **0xatom**. The challenge demonstrates how weak credentials, exposed database services, improper secret management, and insecure Python coding practices can be chained together to achieve full system compromise.

The machine focuses on database enumeration, credential recovery, SSH access, and privilege escalation through unsafe Python code execution.

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | Pyexp: 1 |
| Author | 0xatom |
| Platform | VulnHub |
| Release Date | 11 August 2020 |
| Difficulty | Easy |
| Target OS | Debian Linux |
| Objective | Obtain User and Root Flags |

## Skills Demonstrated

- Network Discovery
- Service Enumeration
- Nmap Scanning
- MySQL Enumeration
- Password Attacks
- Database Analysis
- Fernet Encryption Analysis
- Credential Recovery
- SSH Access
- Linux Enumeration
- Sudo Enumeration
- Python Exploitation
- Privilege Escalation
- Post Exploitation

## Tools Used

- Netdiscover
- Nmap
- Hydra
- MariaDB Client
- SSH
- Python
- Fernet Decoder

## Attack Methodology

1. Discover target host using Netdiscover.
2. Enumerate services with Nmap.
3. Identify exposed MariaDB service.
4. Brute-force MySQL root credentials using Hydra.
5. Access MariaDB remotely.
6. Enumerate databases and tables.
7. Extract encrypted credentials.
8. Decrypt Fernet-encrypted data.
9. Obtain SSH credentials for user lucy.
10. Gain shell access via SSH.
11. Enumerate sudo permissions.
12. Exploit insecure Python exec() functionality.
13. Spawn a root shell.
14. Capture root flag.

## Vulnerabilities Identified

- Weak MySQL Root Password
- Exposed Database Service
- Sensitive Credential Storage
- Reversible Encryption
- Insecure Secret Management
- Unsafe Python exec() Usage
- Misconfigured Sudo Permissions
- Lack of Privilege Separation

## Initial Access

Nmap enumeration revealed:

- SSH running on port 1337
- MariaDB running on port 3306

After brute-forcing the MariaDB root account, access to the database was obtained. Database enumeration revealed Fernet-encrypted credentials and the corresponding encryption key. These credentials were successfully decrypted and used to authenticate via SSH as user **lucy**. :contentReference[oaicite:1]{index=1}

## Privilege Escalation

Running:

```bash
sudo -l
```

revealed:

```bash
(root) NOPASSWD: /usr/bin/python2 /opt/exp.py
```

The vulnerable script contained:

```python
uinput = raw_input('how are you?')
exec(uinput)
```

Because user input was passed directly to `exec()`, arbitrary Python code could be executed with root privileges. A payload spawning `/bin/sh` resulted in a root shell. :contentReference[oaicite:2]{index=2}

## Attack Chain Summary

- Network Discovery
- Service Enumeration
- MySQL Credential Brute Force
- MariaDB Access
- Database Enumeration
- Fernet Credential Recovery
- SSH Login as Lucy
- Sudo Enumeration
- Python exec() Exploitation
- Root Shell
- Root Flag Retrieval

## Security Lessons Learned

- Never expose database services unnecessarily.
- Use strong passwords for administrative accounts.
- Avoid storing sensitive credentials in databases.
- Do not rely on reversible encryption for secrets.
- Never execute unsanitized user input with `exec()`.
- Apply least-privilege principles to sudo permissions.
- Perform regular security audits and code reviews.

## Conclusion

Pyexp: 1 demonstrates how multiple low-to-medium severity weaknesses can be chained together to compromise an entire system. Weak credentials, exposed services, poor secret handling, and insecure coding practices ultimately resulted in arbitrary code execution as root.

---

**Author:** Omkar Babaji Sawant  
**Repository:** VulnHub-Walkthroughs
