# Passive Reconnaissance

Passive reconnaissance is the process of gathering information about a target without directly interacting with its systems.

> Only perform reconnaissance against systems you own or have explicit permission to test.

---

## 1. Identify the Target

Start by identifying the main domain, organization, IP range, or application.

```text
example.com
```

Record:

* Domain
* Organization
* Known subdomains
* Public IP addresses
* Technologies
* Publicly available information

---

## 2. WHOIS

Check domain registration information.

```bash
whois example.com
```

Look for:

* Registrar
* Registration dates
* Name servers
* Organization information
* Contact information

---

## 3. DNS Information

Query publicly available DNS records.

```bash
dig example.com
```

Check common record types:

```bash
dig example.com A
dig example.com MX
dig example.com NS
dig example.com TXT
```

Useful information may include:

* IP addresses
* Mail servers
* Name servers
* SPF records
* Other TXT records

---

## 4. Search Engine Reconnaissance

Use search engines to find publicly indexed information.

Example queries:

```text
site:example.com
site:example.com filetype:pdf
site:example.com filetype:xls
site:example.com login
site:example.com admin
```

Look for:

* Public documents
* Login pages
* Exposed directories
* Technology information
* Publicly indexed files

---

## 5. Find Subdomains

Use passive sources to identify possible subdomains.

Example with `crt.sh`:

```text
https://crt.sh/?q=%25.example.com
```

You can also use:

```bash
subfinder -d example.com
```

Example output:

```text
www.example.com
mail.example.com
dev.example.com
api.example.com
```

> Subdomain discovery tools may perform some direct DNS queries. Treat them as enumeration rather than strictly passive reconnaissance when documenting your methodology.

---

## 6. Certificate Transparency

Search Certificate Transparency logs for certificates associated with the target.

```text
https://crt.sh/?q=%25.example.com
```

Certificate records can reveal:

* Subdomains
* Alternative domain names
* Previously used hostnames

---

## 7. Technology Identification

Identify technologies used by publicly accessible websites.

Useful tools:

```bash
whatweb https://example.com
```

Browser extensions/tools such as Wappalyzer can also help identify:

* Web servers
* Frameworks
* CMS
* JavaScript libraries
* Analytics platforms

---

## 8. Public Code Repositories

Search public repositories for information related to the target.

Examples:

```text
GitHub
GitLab
Bitbucket
```

Search for:

```text
example.com
company-name
api.example.com
```

Look for accidentally exposed:

* Configuration files
* API endpoints
* Internal hostnames
* Documentation
* Test environments

Do not use or disclose credentials or secrets found during reconnaissance.

---

## 9. Document Metadata

Public documents may contain metadata that reveals useful information.

Download an authorized/public document and inspect it:

```bash
exiftool document.pdf
```

Possible information:

* Author
* Software
* Username
* Creation date
* Organization name

---

## 10. Collect and Organize Information

Create a simple reconnaissance note.

```text
Target       : example.com
IP           : x.x.x.x
Web Server   : Apache
Technology   : PHP
Subdomains   :
               www.example.com
               mail.example.com
               api.example.com

Mail Server  : mail.example.com
Nameservers  : ns1.example.com
```

The goal of passive reconnaissance is to build an initial picture of the target before moving to active enumeration.
