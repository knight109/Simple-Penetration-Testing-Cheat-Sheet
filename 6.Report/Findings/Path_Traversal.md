# Path Traversal

## 1. Executive Summary
A Path Traversal vulnerability was identified in the application where user-controlled input can be manipulated to access files or directories outside the intended application directory.

An attacker may be able to access sensitive files on the server by manipulating file or path parameters.

## 2. Description
Path Traversal occurs when an application uses user-controlled input to construct a file path without properly restricting access to the intended directory.

The vulnerability commonly involves path traversal sequences such as:

```text
../
```

It may affect functionality such as:
- File download
- File viewing
- Document retrieval
- Image loading
- Static file access
- File management
- Log viewing

**Category:** OWASP Top 10 - A01:2025 Broken Access Control

**URL:**
```text
https://example.com/download?file=report.pdf
```

**Method:**
```text
GET
```

**Parameter:**
```text
file
```

### Example
A legitimate request may look like:

```text
https://example.com/download?file=report.pdf
```

An attacker may attempt to manipulate the parameter:

```text
https://example.com/download?file=../../../../etc/passwd
```

If the application returns a file outside the intended directory, the parameter may be vulnerable to Path Traversal.

The exact number of traversal sequences required depends on the application's directory structure.

## 3. Impact
Successful exploitation may allow an attacker to:
- Read sensitive files from the server.
- Access application configuration files.
- Disclose credentials and secrets stored in configuration files.
- Access source code or application files.
- Read system files.
- Access logs containing sensitive information.
- Obtain information useful for further exploitation.
- Potentially access private keys or other sensitive cryptographic material.

The actual impact depends on the permissions of the application process and the files accessible from the vulnerable functionality.

## 4. Recommendation
Recommended remediation:
- Avoid using user-controlled input directly when constructing filesystem paths.
- Use an allowlist of permitted files or resources.
- Validate and normalize file paths before accessing them.
- Ensure the resolved path remains inside the intended directory.
- Use secure file-handling APIs provided by the application framework.
- Avoid accepting arbitrary filesystem paths from users.
- Store user-accessible files separately from sensitive system files.
- Apply appropriate filesystem permissions.
- Run the application with the minimum privileges required.
- Prevent access to sensitive application and system directories.
- Return generic errors instead of exposing filesystem paths.
- Log and monitor suspicious path traversal attempts.

## 5. CVSS
**CVSS Version:** 3.1
**Score:** 7.5 — High
**Vector:**
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N
```
