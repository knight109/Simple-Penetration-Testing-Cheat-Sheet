# SQL Injection

## 1. Executive Summary
A SQL Injection vulnerability was identified in the application where user-controlled input is directly incorporated into SQL queries without proper parameterization or input handling.

An attacker may be able to manipulate database queries, access unauthorized data, modify database contents, or potentially execute database-level commands depending on the database configuration.

## 2. Description
SQL Injection occurs when untrusted user input is incorporated into an SQL query without proper parameterization or sanitization.

SQL Injection can allow an attacker to alter the intended logic of a database query.

Common types include:
- In-band SQL Injection
- Blind SQL Injection
- Time-based Blind SQL Injection
- Error-based SQL Injection

**Category:** OWASP Top 10 - A05:2025 Injection

**URL:**
```text
https://example.com/products?id=1
```

**Method:**
```text
GET
```

**Parameter:**
```text
id
```

### Example
```text
https://example.com/products?id=1'
```

A more obvious indication may occur when the application returns a database error or behaves differently when SQL syntax is introduced into the parameter.

For example:

```text
https://example.com/products?id=1 OR 1=1
```

If the application processes the input as part of the SQL query instead of treating it as data, the parameter may be vulnerable to SQL Injection.

## 3. Impact
Successful exploitation may allow an attacker to:
- Retrieve sensitive information from the database.
- Bypass application-level access controls.
- Access data belonging to other users.
- Modify or delete database records.
- Extract usernames, password hashes, tokens, or other sensitive information.
- Enumerate database structure, tables, and columns.
- Potentially execute database-level commands.
- Potentially achieve further compromise depending on database privileges and server configuration.

The actual impact depends on the database privileges of the application's account and the application's architecture.

## 4. Recommendation
Recommended remediation:
- Use parameterized queries or prepared statements.
- Use secure ORM/database APIs that separate SQL commands from user input.
- Avoid dynamically constructing SQL queries using string concatenation.
- Apply strict input validation where appropriate.
- Use allowlists for parameters with predictable values.
- Apply the principle of least privilege to database accounts.
- Ensure the application database account has only the permissions it requires.
- Disable unnecessary database features and privileges.
- Avoid displaying detailed database errors to users.
- Implement centralized error handling.
- Conduct security testing against database-related input parameters.
- Review existing database queries for similar injection points.

## 5. CVSS
**CVSS Version:** 3.1
**Score:** 9.8 — Critical
**Vector:**
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```
