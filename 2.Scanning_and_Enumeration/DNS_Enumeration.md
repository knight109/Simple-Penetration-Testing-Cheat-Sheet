# DNS Enumeration
DNS enumeration is the process of gathering detailed DNS records and information about a target domain.

## Query DNS Records
```bash
dig <TARGET> A
dig <TARGET> MX
dig <TARGET> NS
dig <TARGET> TXT
```

## Query All Records
```bash
dig <TARGET> ANY
```

## Reverse DNS Lookup
```bash
dig -x <TARGET-IP>
```

## DNS Zone Transfer
```bash
dig axfr <TARGET>
```

## What to Look For
* IP addresses
* Name servers
* Mail servers
* Subdomains
* TXT records
* Potentially exposed information
* Misconfigured DNS zone transfers

## Record Results
```text
Domain:
A:
MX:
NS:
TXT:
Subdomains:
Other Findings:
```
