# Directory Enumeration
Directory enumeration is the process of discovering hidden or unlinked directories and files on a web server.

## 1. Gobuster
```bash
gobuster dir -u http://<TARGET>:<PORT> -w <WORDLIST>
```

## 2. FFUF
```bash
ffuf -u http://<TARGET>:<PORT>/FUZZ -w <WORDLIST>
```

## 3. Dirsearch
```bash
dirsearch -u http://<TARGET>:<PORT> -w <WORDLIST>
```

## 4. Dirb
```bash
dirb http://<TARGET>:<PORT> <WORDLIST>
```

## 5. Feroxbuster
```bash
feroxbuster -u http://<TARGET>:<PORT> -w <WORDLIST>
```

## Common wordlist locations:
```bash
/usr/share/wordlists/
/usr/share/seclists/
```

## Common Targets
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

## What to Look For
* Hidden directories
* Backup files
* Configuration files
* Login pages
* Upload directories
* API endpoints
* Development or testing directories

## Record Results
```text
URL:
Status:
Size:
Interesting Files:
Interesting Directories:
```
