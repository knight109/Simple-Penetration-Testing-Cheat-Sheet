# Command Injection

## 1. Executive Summary
A Command Injection vulnerability was identified in the application where user-controlled input is passed to an operating system command without proper validation or safe handling.

An attacker may be able to execute arbitrary operating system commands with the privileges of the application or service processing the input.

## 2. Description
Command Injection occurs when an application passes untrusted user input to an operating system command or shell without properly separating application data from executable commands.

The vulnerability may occur in functionality such as:
- Network diagnostic tools
- File processing
- System utilities
- Ping or traceroute functionality
- Hostname or IP address lookup
- Backup operations
- Application administration features

**Category:** OWASP Top 10 - A05:2025 Injection

**URL:**
```text
https://example.com/tools/ping
```

**Method:**
```text
GET
```

**Parameter:**
```text
host
```

### Example
A legitimate request may look like:

```text
https://example.com/tools/ping?host=example.com
```

If the application directly passes the parameter to an operating system command, special command syntax may alter the intended command execution.

For example:

```text
https://example.com/tools/ping?host=example.com;whoami
```

If the application executes the injected command and returns its output, the parameter may be vulnerable to Command Injection.

## 3. Impact
Successful exploitation may allow an attacker to:
- Execute arbitrary operating system commands.
- Read sensitive files accessible to the application user.
- Modify or delete files.
- Access application configuration and secrets.
- Enumerate the underlying operating system.
- Access internal network resources.
- Execute additional malicious programs or scripts.
- Establish further access to the affected system.
- Potentially escalate privileges if additional vulnerabilities or misconfigurations exist.

The actual impact depends on the privileges of the affected application and the security controls implemented on the underlying system.

## 4. Recommendation
Recommended remediation:
- Avoid passing user-controlled input directly to operating system commands.
- Use dedicated application or library APIs instead of shell commands where possible.
- Use parameterized APIs that separate command arguments from executable commands.
- Apply strict allowlist validation to expected input values.
- Reject unexpected characters and command syntax where appropriate.
- Avoid invoking commands through a shell when a direct process execution API is available.
- Run application services with the minimum privileges required.
- Apply the principle of least privilege to service accounts.
- Restrict access to administrative functionality.
- Implement appropriate authentication and authorization controls.
- Log and monitor suspicious command execution attempts.
- Review application code for other locations where user input reaches system commands.

## 5. CVSS
**CVSS Version:** 3.1
**Score:** 9.8 — Critical
**Vector:**
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```
