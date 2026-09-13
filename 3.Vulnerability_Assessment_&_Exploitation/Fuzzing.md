# Fuzzing
Fuzzing is the process of automatically sending many different inputs to an application and analyzing the responses to discover hidden resources, parameters, virtual hosts, or unexpected behavior.
A simple workflow:
```text
Generate Inputs
      ↓
Send Requests
      ↓
Analyze Responses
      ↓
Identify Interesting Results
      ↓
Manually Verify
```

## 1. Directory and File Fuzzing
Discover hidden directories and files.
### ffuf
```bash
ffuf -u http://<TARGET>:<PORT>/FUZZ -w <WORDLIST>
```
### Common Extensions
```bash
ffuf -u http://<TARGET>:<PORT>/FUZZ -w <WORDLIST> -e .php,.html,.txt,.bak
```

### Feroxbuster
```bash
feroxbuster -u http://<TARGET>:<PORT> -w <WORDLIST>
```
Look for:

```text
/admin
/login
/backup
/uploads
/config
/api
/dev
/test
```

## 2. Parameter Fuzzing
Fuzz parameter names to discover hidden parameters.
Example:
```bash
ffuf -u "http://<TARGET>:<PORT>/search?FUZZ=test" -w <WORDLIST>
```
Possible discoveries:
```text
debug
admin
file
page
redirect
id
user
```
Tools such as **Arjun** can also be used specifically for HTTP parameter discovery:
```bash
arjun -u http://<TARGET>:<PORT>/search
```

## 3. Parameter Value Fuzzing
Fuzz the value of an existing parameter.
Example:
```bash
ffuf -u "http://<TARGET>:<PORT>/search?id=FUZZ" -w <WORDLIST>
```
This can be useful for testing:
* IDs
* File names
* Paths
* Usernames
* Application values
* Potential injection points

## 4. Virtual Host Fuzzing
Discover virtual hosts configured on the target.
```bash
ffuf -u http://<TARGET>:<PORT>/ \
-H "Host: FUZZ.<TARGET>" \
-w <WORDLIST>
```
Potential results:
```text
admin.<TARGET>
dev.<TARGET>
test.<TARGET>
staging.<TARGET>
```

## 5. HTTP Method Fuzzing
Test whether an endpoint behaves differently with different HTTP methods.
Common methods:
```text
GET
POST
PUT
PATCH
DELETE
OPTIONS
HEAD
```
Example:
```bash
curl -i -X OPTIONS http://<TARGET>:<PORT>/
```
Use this to identify methods that may require further testing.

## 6. Response Filtering
Fuzzing can produce many results. Filter responses to find interesting differences.

### Filter by Status Code
```bash
ffuf -u http://<TARGET>:<PORT>/FUZZ \
-w <WORDLIST> \
-fc 404
```
