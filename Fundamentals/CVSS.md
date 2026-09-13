# CVSS
**CVSS (Common Vulnerability Scoring System)** is a standardized system for measuring the severity of security vulnerabilities.
CVSS produces a score from **0.0 to 10.0**. A higher score indicates a more severe vulnerability.

## CVSS Severity
|    Score | Severity |
| -------: | -------- |
|      0.0 | None     |
|  0.1–3.9 | Low      |
|  4.0–6.9 | Medium   |
|  7.0–8.9 | High     |
| 9.0–10.0 | Critical |

## What CVSS Measures
CVSS considers factors such as:
* **Attack Vector** — How the vulnerability can be exploited
* **Attack Complexity** — How difficult exploitation is
* **Privileges Required** — Whether authentication or privileges are required
* **User Interaction** — Whether another user must perform an action
* **Scope** — Whether exploitation affects resources beyond the vulnerable component
* **Confidentiality** — Impact on data confidentiality
* **Integrity** — Impact on data integrity
* **Availability** — Impact on system availability

## CVSS Versions
Common versions include:
* **CVSS v3.1** — Widely used for vulnerability scoring
* **CVSS v4.0** — Newer version with additional metrics and improved scoring

## Example
A vulnerability that:
* Can be exploited remotely
* Requires no authentication
* Requires no user interaction
* Allows arbitrary code execution
* Gives complete control over the affected system
would generally receive a **high or critical CVSS score**, depending on the exact metrics.

## Important Note
CVSS measures **severity**, not the complete **risk** of a vulnerability.
A vulnerability with a high CVSS score may have low practical risk in one environment, while a medium-severity vulnerability could be highly important if the affected system is critical to the organization.
Use CVSS together with factors such as:
* Asset importance
* Exposure
* Exploit availability
* Business impact
* Existing security controls
* Environmental conditions
