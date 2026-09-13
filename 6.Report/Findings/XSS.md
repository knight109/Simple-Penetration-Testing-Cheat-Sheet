# Cross-Site Scripting (XSS)
## 1. Executive Summary
A Cross-Site Scripting (XSS) vulnerability was identified in the application where user-controlled input is reflected or stored without proper output encoding.
An attacker may be able to execute arbitrary JavaScript in the context of another user's browser.

## 2. Description
Cross-Site Scripting (XSS) occurs when an application includes untrusted user input in a web page without properly validating or encoding the output.
XSS can be classified into:
- Reflected XSS
- Stored XSS
- DOM-based XSS
**Category:** OWASP Top 10 - A05:2025 Injection
**URL:**
```text
https://example.com/search
```
**Method:**
```text
GET
```
**Parameter:**
```text
q
```

### Example
```text
https://example.com/search?q=<script>alert(document.domain)</script>
```
If the payload is executed by the browser instead of being safely encoded, the parameter may be vulnerable to XSS.


## 3. Impact
Successful exploitation may allow an attacker to:
- Execute arbitrary JavaScript in a victim's browser.
- Modify content displayed to the victim.
- Perform actions using the victim's authenticated session.
- Access sensitive information exposed to JavaScript.
- Conduct phishing attacks through the trusted application domain.
- Redirect users to malicious content.
- Abuse functionality available to the victim.
The actual impact depends on the application's functionality and the privileges of the affected user.


## 4. Recommendation
Recommended remediation:
- Properly encode untrusted output according to its HTML, JavaScript, CSS, or URL context.
- Validate user input using an allowlist where practical.
- Avoid dangerous DOM APIs such as `innerHTML` when handling untrusted data.
- Use safe alternatives such as `textContent` where applicable.
- Implement a restrictive Content Security Policy (CSP).
- Use framework-provided output-encoding mechanisms.
- Sanitize HTML input when HTML content is intentionally supported.
- Do not rely solely on client-side validation.
- Review existing stored data for previously injected payloads.


## 5. CVSS
**CVSS Version:** 3.1
**Score:** 6.1 — Medium
**Vector:**
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:C/C:L/I:L/A:N
```
