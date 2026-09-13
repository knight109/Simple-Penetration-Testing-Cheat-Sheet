# Active Reconnaissance

Active reconnaissance is the process of gathering information by directly interacting with the target system.

> Only perform active reconnaissance against systems you own or have explicit permission to test.

---

## 1. Check Host Availability

Check whether the target is reachable.

```bash
ping -c 4 example.com
```

If ICMP is blocked, this does not necessarily mean the host is down.

---

## 2. Identify IP Address

Resolve the target domain to an IP address.

```bash
host example.com
```

or:

```bash
dig example.com
```

---

## 3. Port Scanning

Use Nmap to identify open ports.

```bash
nmap example.com
```

Scan all TCP ports:

```bash
nmap -p- example.com
```

---

## 4. Service Enumeration

Identify services and their versions.

```bash
nmap -sV example.com
```

Example:

```text
22/tcp   open  ssh     OpenSSH
80/tcp   open  http    Apache
3306/tcp open  mysql   MySQL
```

---

## 5. OS Detection

Attempt to identify the target operating system.

```bash
sudo nmap -O example.com
```

Combine OS and service detection:

```bash
sudo nmap -sV -O example.com
```

---

## 6. Default Nmap Scripts

Run Nmap's default NSE scripts.

```bash
nmap -sC example.com
```

Combine with version detection:

```bash
nmap -sC -sV example.com
```

---

## 7. Web Enumeration

If HTTP/HTTPS is available, inspect the web service.

```bash
curl -I http://example.com
```

Check the response headers:

```bash
curl -i http://example.com
```

Look for:

* Server
* Technologies
* Cookies
* Redirects
* Security headers

---

## 8. Directory Enumeration

Look for accessible directories and files.

Using Gobuster:

```bash
gobuster dir -u http://example.com -w wordlist.txt
```

Using FFUF:

```bash
ffuf -u http://example.com/FUZZ -w wordlist.txt
```

Common targets:

```text
/admin
/login
/uploads
/backup
/config
```

---

## 9. Virtual Host Enumeration

Look for virtual hosts hosted on the same server.

Using FFUF:

```bash
ffuf -u http://example.com -H "Host: FUZZ.example.com" -w wordlist.txt
```

Possible results:

```text
dev.example.com
test.example.com
admin.example.com
```

---

## 10. DNS Enumeration

Query DNS records directly from the target's DNS infrastructure.

```bash
dig example.com ANY
```

Query specific records:

```bash
dig example.com A
dig example.com MX
dig example.com NS
dig example.com TXT
```

---

## 11. Service-Specific Enumeration

Once open ports are identified, enumerate the corresponding services.

### SSH

```bash
nmap -p 22 --script ssh-* example.com
```

### HTTP

```bash
nmap -p 80,443 --script http-* example.com
```

### SMB

```bash
nmap -p 139,445 --script smb-* example.com
```

### FTP

```bash
nmap -p 21 --script ftp-* example.com
```

---

## 12. Record the Results

Organize the discovered information.

```text
Target       : example.com
IP           : x.x.x.x

Open Ports:
22/tcp       : SSH
80/tcp       : HTTP
443/tcp      : HTTPS

Web Server   : Apache
OS           : Linux

Directories:
 /admin
 /uploads
 /backup
```

Use the results from active reconnaissance to determine which services and applications should be investigated during the next phase.
