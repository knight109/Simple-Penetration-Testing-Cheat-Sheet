# Web Enumeration
Web enumeration is the process of gathering detailed information about a web application after identifying an HTTP/HTTPS service.

## 1. Inspect HTTP Response
```bash
curl -i http://<TARGET>:<PORT>
```

Check:
* HTTP status code
* Headers
* Cookies
* Redirects
* Server information

## 2. Inspect Robots.txt
```bash
curl http://<TARGET>:<PORT>/robots.txt
```
Look for paths that may be interesting or restricted.

## 3. Check Common Files
```bash
curl http://<TARGET>:<PORT>/sitemap.xml
```
```bash
curl http://<TARGET>:<PORT>/.well-known/security.txt
```

## 4. Inspect Web Page
```bash
curl -s http://<TARGET>:<PORT>/
```
Look for:
* Links
* Forms
* Comments
* JavaScript files
* API endpoints
* Hidden parameters

## 5. Identify HTTP Methods
```bash
curl -X OPTIONS -i http://<TARGET>:<PORT>/
```
Check which HTTP methods are supported.

## 6. Check Authentication
Identify:
* Login pages
* Registration
* Password reset
* Session handling
* Different user roles

## 7. Record Results
```text
URL:
Status:
Server:
Technology:
Authentication:
HTTP Methods:
Interesting Endpoints:
```
