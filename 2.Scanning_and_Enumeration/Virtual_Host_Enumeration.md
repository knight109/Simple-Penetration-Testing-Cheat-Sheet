# Virtual Host Enumeration
Virtual host enumeration identifies virtual hosts configured on the same web server.

## FFUF
```bash
ffuf -u http://<TARGET>:<PORT> \
-H "Host: FUZZ.<TARGET>" \
-w <WORDLIST>
```

## Gobuster
```bash
gobuster vhost -u http://<TARGET>:<PORT> \
-w <WORDLIST>
```

## What to Look For
```text
dev.<TARGET>
test.<TARGET>
admin.<TARGET>
staging.<TARGET>
```
Interesting virtual hosts may expose:
* Development environments
* Test environments
* Admin panels
* Internal applications
* Additional functionality

## Record Results
```text
Virtual Host:
IP:
Status:
Size:
Notes:
```
