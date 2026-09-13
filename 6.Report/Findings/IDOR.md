# Insecure Direct Object Reference (IDOR)

## 1. Executive Summary
An Insecure Direct Object Reference (IDOR) vulnerability was identified in the application where an attacker can manipulate a direct object identifier to access resources belonging to another user without proper authorization checks.

An attacker may be able to access, modify, or delete unauthorized resources by changing identifiers in requests.

## 2. Description
IDOR occurs when an application uses user-controlled identifiers to directly access internal objects or resources without verifying whether the requesting user is authorized to access the requested object.

Common identifiers that may be vulnerable include:
- User IDs
- Account IDs
- Order IDs
- Invoice IDs
- Document IDs
- File IDs
- Message IDs

**Category:** OWASP Top 10 - A01:2025 Broken Access Control

**URL:**
```text
https://example.com/api/invoices/1001
```

**Method:**
```text
GET
```

**Parameter:**
```text
invoice_id
```

### Example
An authenticated user may normally access:

```text
https://example.com/api/invoices/1001
```

After changing the identifier:

```text
https://example.com/api/invoices/1002
```

If the application returns invoice `1002` even though it belongs to another user, the endpoint may be vulnerable to IDOR.

The same issue may occur with other HTTP methods. For example:

```text
PUT /api/users/1002
DELETE /api/documents/1002
```

If the application does not verify authorization for the referenced object, an attacker may be able to modify or delete resources belonging to another user.

## 3. Impact
Successful exploitation may allow an attacker to:
- Access other users' personal information.
- Read unauthorized documents or files.
- Access invoices, orders, or transaction information.
- Modify another user's information.
- Modify unauthorized application resources.
- Delete resources belonging to other users.
- Access sensitive business information.
- Perform unauthorized actions on behalf of other users.

The actual impact depends on the type of object exposed and the operations permitted by the affected endpoint.

## 4. Recommendation
Recommended remediation:
- Implement server-side authorization checks for every object access.
- Verify that the authenticated user is authorized to access the requested resource.
- Do not rely on object IDs or other client-controlled identifiers as authorization controls.
- Apply object-level access control to GET, POST, PUT, PATCH, and DELETE operations.
- Use role-based or attribute-based access control where appropriate.
- Ensure authorization checks are performed consistently across all API endpoints.
- Avoid exposing sensitive sequential identifiers where possible.
- Consider using unpredictable identifiers such as UUIDs as an additional security measure.
- Do not rely on UUIDs alone as a replacement for authorization checks.
- Test horizontal privilege escalation between users.
- Test vertical privilege escalation between users with different roles.
- Log and monitor unauthorized access attempts.

## 5. CVSS
**CVSS Version:** 3.1
**Score:** 6.5 — Medium
**Vector:**
```text
CVSS:3.1/AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:N/A:N
```
