# Privilege Escalation

## 1. Executive Summary
A Privilege Escalation vulnerability was identified in the system where a low-privileged user can obtain higher privileges than those originally assigned.

An attacker who has already obtained limited access to the system may be able to exploit insecure configurations, excessive permissions, vulnerable services, or other weaknesses to obtain administrative or root-level privileges.

## 2. Description
Privilege Escalation occurs when an attacker with limited privileges is able to access functionality, files, processes, or system resources that should only be available to a higher-privileged user.

Privilege Escalation can be classified into:

- Vertical Privilege Escalation
- Horizontal Privilege Escalation

Common causes include:

- Misconfigured `sudo` permissions
- SUID binaries
- Linux capabilities
- Writable scripts executed by privileged users
- Misconfigured services
- Insecure scheduled tasks
- Excessive file permissions
- Exposed credentials
- Vulnerable software or operating system components

**Category:** OWASP Top 10 - A01:2025 Broken Access Control

**URL:**
```text
N/A - System-level vulnerability
```

**Method:**
```text
N/A
```

**Parameter:**
```text
N/A
```

### Example
An attacker initially obtains access as a low-privileged user:

```text
$ whoami
www-data
```

During enumeration, a misconfigured SUID binary or privileged service is identified.

For example:

```text
$ find / -perm -4000 -type f 2>/dev/null
/usr/bin/example
```

If the binary can be abused to execute commands with elevated privileges, the attacker may be able to obtain root access.

Successful exploitation may result in:

```text
$ whoami
root
```

The exact exploitation method depends on the underlying misconfiguration or vulnerable component.

## 3. Impact
Successful exploitation may allow an attacker to:

- Obtain administrative or root-level privileges.
- Access restricted files and directories.
- Read sensitive system and application data.
- Access credentials and secrets belonging to other users.
- Modify system configurations.
- Modify or delete files owned by privileged users.
- Disable security controls.
- Install or execute unauthorized software.
- Access other services running on the system.
- Establish persistent access to the compromised system.
- Fully compromise the affected host.

The actual impact depends on the privileges obtained and the resources accessible to the elevated account.

## 4. Recommendation
Recommended remediation:

- Apply the principle of least privilege.
- Review and restrict `sudo` permissions.
- Remove unnecessary SUID and SGID permissions.
- Review Linux capabilities and remove unnecessary capabilities.
- Ensure privileged scripts and configuration files are not writable by unprivileged users.
- Secure scheduled tasks and cron jobs.
- Review services running with root or administrative privileges.
- Apply appropriate filesystem permissions.
- Remove unnecessary administrative services.
- Keep operating systems and installed software patched.
- Protect credentials and secrets from unauthorized users.
- Run application services using dedicated low-privileged accounts.
- Regularly audit privileged accounts and permissions.
- Monitor suspicious privilege escalation activity.
- Perform periodic vulnerability and configuration assessments.

## 5. CVSS
**CVSS Version:** 3.1
**Score:** 8.8 — High
**Vector:**
```text
CVSS:3.1/AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H
```
