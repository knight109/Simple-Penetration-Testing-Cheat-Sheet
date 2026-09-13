# Active Reconnaissance
Active reconnaissance is the process of gathering information by directly interacting with the target system.
> Only perform active reconnaissance against systems you own or have explicit permission to test.
---

## 1. Check Host Availability
Check whether the target is reachable.
```bash
ping -c 4 example.com
```
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

## 3. Nmap Scanning
Use Nmap to identify open ports, services, versions, OS, and common vulnerabilities.
### Basic Scan
```bash
nmap example.com
```
### All TCP Ports
```bash
nmap -p- example.com
```
### Service & Version Detection
```bash
nmap -sV example.com
```
### OS Detection
```bash
sudo nmap -O example.com
```
### Default Scripts
```bash
nmap -sC example.com
```
### Recommended Scan
```bash
sudo nmap -sC -sV -O example.com 
sudo nmap -sC -sV -O -p- example.com 
```
Example:
```text
22/tcp   open  ssh     OpenSSH
80/tcp   open  http    Apache
3306/tcp open  mysql   MySQL
```
---

## 4. Web Enumeration
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

## 5. Web Directory Enumeration
Look for accessible directories and files on a web server.
### Gobuster
```bash
gobuster dir -u http://example.com -w wordlist.txt
```
### FFUF
```bash
ffuf -u http://example.com/FUZZ -w wordlist.txt
```
### Dirsearch
```bash
dirsearch -u http://example.com
```
Using a specific wordlist:
```bash
dirsearch -u http://example.com -w wordlist.txt
```
### Dirb
```bash
dirb http://example.com
```
Using a specific wordlist:
```bash
dirb http://example.com wordlist.txt
```
### Others
Common targets to look for:
```text
/admin
/login
/uploads
/backup
/config
/api
/dev
/test
```
Common wordlist location:
```text
/usr/share/wordlists/
/usr/share/seclists/
```
Useful things to check:
* Hidden directories
* Backup files
* Configuration files
* Login pages
* Upload directories
* API endpoints
* Development or testing directories
---

## 6. Virtual Host Enumeration
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

## 7. DNS Enumeration
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

## 8. Service-Specific Enumeration
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

## 9. Record the Results
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
