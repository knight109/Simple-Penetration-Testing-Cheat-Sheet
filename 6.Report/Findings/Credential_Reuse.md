# Credential Reuse (Credential Stuffing)

## 1. Executive Summary
A Credential Reuse (or Credential Stuffing) vulnerability was identified in the application's authentication mechanism. The application does not implement adequate protections against automated login attempts using credentials compromised in third-party data breaches.

An attacker can leverage automated tools and massive lists of leaked username and password pairs to systematically attempt logins, leading to widespread Account Takeover (ATO) of users who reuse their passwords across multiple services.

## 2. Description
Credential Reuse occurs when users employ the same password for multiple online accounts. If one service suffers a data breach, attackers harvest these credentials and test them against other applications—a technique known as credential stuffing.

The application is vulnerable because it lacks sufficient defensive controls such as Multi-Factor Authentication (MFA), aggressive rate limiting, CAPTCHA, or compromised credential checking, allowing attackers to perform high-volume, automated authentication attempts.

**Category:** OWASP Top 10 - A07:2025 Identification and Authentication Failures

**URL:**
```text
[https://example.com/api/v1/login](https://example.com/api/v1/login)
```

**Method:**
```text
POST
```

**Parameter:**
```text
email, password
```

### Example
An attacker configures an automated tool with a list of thousands of compromised credentials and sends rapid login requests:

```http
POST /api/v1/login HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "email": "victim@example.com",
  "password": "Password123!"
}
```

Because the application only relies on a single authentication factor (the password) and lacks robust anti-automation mechanisms, the attacker successfully gains access to any account where the user reused a compromised password.

## 3. Impact
Successful exploitation may allow an attacker to:
- Achieve full Account Takeover (ATO) of affected users.
- Access sensitive personal identifiable information (PII) or financial data.
- Perform unauthorized actions on behalf of the user (e.g., unauthorized purchases, funds transfers, or data deletion).
- Use compromised accounts as a launchpad for phishing or social engineering attacks against other users.
- Cause significant reputational and financial damage to the organization.

## 4. Recommendation
Recommended remediation:
- **Implement Multi-Factor Authentication (MFA):** Require a second form of verification (e.g., TOTP, SMS, push notification) to log in, which neutralizes the threat of compromised passwords.
- **Detect and Prevent Automation:** Implement CAPTCHA, web application firewalls (WAF), and behavioral analytics to detect and block credential stuffing tools.
- **Implement Rate Limiting:** Enforce strict login rate limits based on IP address, device fingerprint, and target account.
- **Check for Breached Passwords:** Integrate with services like the "Have I Been Pwned" API to prevent users from registering or maintaining passwords known to be compromised.
- **Notify Users:** Alert users via email of new logins from unrecognized devices or geographic locations.

## 5. CVSS
**CVSS Version:** 3.1
**Score:** 8.1 — High
**Vector:**
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N
```
