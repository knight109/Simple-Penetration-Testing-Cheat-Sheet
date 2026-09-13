# Local File Inclusion (LFI)

## 1. Executive Summary
A Local File Inclusion (LFI) vulnerability was identified in the application where user-controlled input is used to include or load local files from the server without sufficient validation or access restrictions.

An attacker may be able to read sensitive local files and, depending on the application configuration and available attack paths, potentially achieve further compromise of the server.

## 2. Description
Local File Inclusion (LFI) occurs when an application allows user-controlled input to determine which local file is loaded or included by the application.

LFI commonly occurs in functionality such as:
- Page templates
- Language or localization files
- File viewers
- Document previews
- Dynamic content loading
- Template selection

**Category:** OWASP Top 10 - A01:2025 Broken Access Control

**URL:**
```text
https://example.com/index.php?page=home
```

**Method:**
```text
GET
```

**Parameter:**
```text
page
```

### Example
A legitimate request may look like:

```text
https://example.com/index.php?page=home
```

An attacker may attempt to reference a local file:

```text
https://example.com/index.php?page=/etc/passwd
```

Another common test involves traversal sequences:

```text
https://example.com/index.php?page=../../../../etc/passwd
```

If the application includes or returns the contents of a local file outside the intended application directory, the parameter may be vulnerable to LFI.

The exact behavior depends on the application's implementation, operating system, permissions, and file inclusion mechanism.

## 3. Impact
Successful exploitation may allow an attacker to:
- Read sensitive files from the server.
- Disclose application configuration files.
- Obtain credentials and secrets stored in local files.
- Read source code or application files.
- Disclose private keys and other sensitive cryptographic material.
- Access logs and other locally stored information.
- Obtain information useful for further exploitation.
- Potentially achieve Remote Code Execution when combined with another suitable vulnerability or server configuration.

The actual impact depends on the files accessible to the application process and whether the inclusion mechanism can be combined with other attack techniques.

## 4. Recommendation
Recommended remediation:
- Avoid using user-controlled input directly in file inclusion functions.
- Use an allowlist of permitted files or templates.
- Map user-supplied identifiers to predefined files instead of accepting filesystem paths.
- Validate and normalize file paths before processing them.
- Ensure resolved paths remain within the intended application directory.
- Disable unnecessary local file inclusion functionality.
- Apply appropriate filesystem permissions.
- Run the application with the minimum privileges required.
- Prevent access to sensitive system and application files.
- Keep sensitive credentials and private keys outside web-accessible directories.
- Avoid exposing detailed filesystem errors and paths.
- Log and monitor suspicious file inclusion attempts.
- Review the application for other parameters that dynamically load local files.

## 5. CVSS
**CVSS Version:** 3.1
**Score:** 7.5 — High
**Vector:**
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N
```
