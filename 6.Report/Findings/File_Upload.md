# Insecure File Upload

## 1. Executive Summary
An Insecure File Upload vulnerability was identified in the application where user-submitted files are accepted and stored without adequate validation of file type, extension, size, or content.

An attacker may be able to upload malicious files, such as web shells or executable scripts, leading to remote code execution, system compromise, or unauthorized access to sensitive application data.

## 2. Description
Insecure File Upload occurs when an application fails to properly validate, sanitize, or restrict uploaded files. If the application stores these files within the web root or executes them improperly, it can allow attackers to interact directly with the server.

The vulnerability typically arises due to:
- Missing or insufficient file type validation (relying solely on client-side checks or easily bypassed Content-Type headers).
- Allowing dangerous extensions (e.g., `.php`, `.jsp`, `.asp`, `.exe`).
- Storing uploaded files in a publicly accessible web root without execution restrictions.
- Failing to rename uploaded files, leading to potential path traversal or overwriting critical system files.
- Lacking proper file size and rate-limiting controls, which can lead to Denial of Service (DoS).

**Category:** OWASP Top 10 - A03:2025 Injection / Broken Access Control

**URL:**
```text
[https://example.com/profile/upload-avatar](https://example.com/profile/upload-avatar)
```

**Method:**
```text
POST
```

**Parameter:**
```text
avatar
```

### Example
A legitimate request uploads an image file:

```http
POST /profile/upload-avatar HTTP/1.1
Host: example.com
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary

------WebKitFormBoundary
Content-Disposition: form-data; name="avatar"; filename="photo.jpg"
Content-Type: image/jpeg

[binary image data]
------WebKitFormBoundary--
```

If the application does not validate the file extension or content, an attacker can substitute the image with a malicious script:

```http
POST /profile/upload-avatar HTTP/1.1
Host: example.com
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary

------WebKitFormBoundary
Content-Disposition: form-data; name="avatar"; filename="shell.php"
Content-Type: application/x-php

<?php echo system($_GET['cmd']); ?>
------WebKitFormBoundary--
```

If the uploaded script is saved directly to the web root, the attacker can access and execute it via `https://example.com/uploads/shell.php?cmd=whoami`.

## 3. Impact
Successful exploitation may allow an attacker to:
- Execute arbitrary operating system commands via web shells (Remote Code Execution).
- Read, modify, or delete sensitive application and system files.
- Access internal network resources and configuration secrets.
- Perform Cross-Site Scripting (XSS) by uploading malicious HTML or SVG files containing JavaScript.
- Exhaust server disk space or resources, leading to Denial of Service (DoS).
- Facilitate further lateral movement within the infrastructure.

The actual impact depends on the execution permissions of the web server directory and the privileges associated with the application user.

## 4. Recommendation
Recommended remediation:
- Implement strict allowlist validation for file extensions (e.g., permit only `.jpg`, `.png`, etc.) and reject any unexpected formats.
- Validate file contents (magic bytes/file signatures) rather than relying solely on file extensions or `Content-Type` headers provided by the client.
- Store uploaded files outside of the web root directory or configure the web server to disable script execution within upload directories.
- Generate unpredictable, randomized filenames for all uploaded files to prevent direct referencing, overwriting, and path traversal attacks.
- Enforce strict file size limits and implement rate limiting on upload endpoints to mitigate Denial of Service risks.
- Utilize a dedicated storage service or cloud bucket (e.g., AWS S3) with restricted public permissions where appropriate.
- Scan uploaded files using updated antivirus or malware detection solutions.

## 5. CVSS
**CVSS Version:** 3.1
**Score:** 9.8 — Critical
**Vector:**
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```
