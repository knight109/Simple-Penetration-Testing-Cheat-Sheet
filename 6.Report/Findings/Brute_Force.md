# Brute Force

## 1. Executive Summary
A Brute Force vulnerability was identified in the application's authentication mechanism where repeated login attempts can be performed without sufficient protection against automated credential guessing.

An attacker may be able to repeatedly attempt usernames and passwords until valid credentials are discovered.

## 2. Description
Brute Force is an attack where an attacker systematically attempts multiple password or credential combinations against an authentication mechanism.

The attack may target:
- Login pages
- API authentication endpoints
- Password reset mechanisms
- OTP verification
- PIN authentication
- Other credential-based authentication mechanisms

**Category:** OWASP Top 10 - A07:2025 Authentication Failures

**URL:**
```text
https://example.com/login
```

**Method:**
```text
POST
```

**Parameter:**
```text
username
password
```

### Example
A login request may contain:

```text
POST /login

username=test@example.com
password=Password123
```

If the application accepts repeated authentication attempts without effective rate limiting, account lockout, progressive delays, or other protective controls, the authentication endpoint may be vulnerable to brute-force attacks.

For example, an attacker may repeatedly submit different passwords against the same account:

```text
POST /login
username=admin@example.com
password=Password001
```

```text
POST /login
username=admin@example.com
password=Password002
```

```text
POST /login
username=admin@example.com
password=Password003
```

## 3. Impact
Successful exploitation may allow an attacker to:
- Obtain valid user credentials.
- Gain unauthorized access to user accounts.
- Compromise accounts with weak passwords.
- Access sensitive information available to the compromised account.
- Perform actions using the compromised user's privileges.
- Potentially compromise administrative accounts.
- Use compromised credentials against other services when password reuse exists.

The actual impact depends on the strength of the targeted credentials, authentication controls, account privileges, and whether additional authentication factors are enabled.

## 4. Recommendation
Recommended remediation:
- Implement rate limiting on authentication endpoints.
- Limit the number of failed authentication attempts within a defined period.
- Implement progressive delays after repeated failed attempts.
- Temporarily lock or restrict accounts after excessive failed attempts where appropriate.
- Implement multi-factor authentication (MFA).
- Use CAPTCHA or equivalent controls when suspicious authentication activity is detected.
- Monitor and log repeated authentication failures.
- Alert administrators about abnormal login activity.
- Prevent username enumeration through consistent authentication responses.
- Enforce strong password policies.
- Block commonly used and compromised passwords.
- Implement appropriate protections for password reset and OTP endpoints.
- Consider IP-based and account-based rate limiting together.
- Avoid permanent account lockout mechanisms that can be abused for denial-of-service against legitimate users.

## 5. CVSS
**CVSS Version:** 3.1
**Score:** 9.1 — Critical
**Vector:**
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N
```
