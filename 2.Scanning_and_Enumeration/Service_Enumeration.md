# Service Enumeration
Service enumeration is the process of gathering detailed information about services running on discovered open ports.

## 1. Service & Version Detection
```bash
nmap -sV -p <PORT> <TARGET>
```

## 2. Default Scripts
```bash
nmap -sC -p <PORT> <TARGET>
```

## 3. Service-Specific Scripts
### SSH
```bash
nmap --script ssh-* -p <PORT> <TARGET>
```

### HTTP
```bash
nmap --script http-* -p <PORT> <TARGET>
```

### SMB
```bash
nmap --script smb-* -p <PORT> <TARGET>
```

### FTP
```bash
nmap --script ftp-* -p <PORT> <TARGET>
```

## 4. What to Look For
* Service version
* Service configuration
* Authentication methods
* Accessible resources
* Users or shares
* Anonymous access
* Interesting information

## Record Results
```text
Port:
Service:
Version:
Authentication:
Interesting Findings:
```
