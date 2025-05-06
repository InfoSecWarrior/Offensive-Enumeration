# 🌐 **Web Server Scanner**

---

## 🔧 **WhatWeb Usage**

### 📦 **Install Tools**

Install WhatWeb and Nikto packages using apt package manager:

```bash
apt install whatweb nikto
```

---

### 🔍 **Basic Scans**

Scan a simple website for technologies used:

```bash
whatweb http://192.168.1.206
```

Scan a website hosted on a custom port:

```bash
whatweb http://192.168.1.206:2222
```

Scan a specific page of a website:

```bash
whatweb http://192.168.1.44/dvwa/login.php
```

Scan a web application running on port 8080:

```bash
whatweb http://192.168.1.211:8080
```

---

## 🛠️ **Using Nmap HTTP Enum Script**

Enumerate a website for technologies and vulnerabilities using Nmap’s HTTP enumeration script:

```bash
nmap -v -Pn -sT -sV -p 80 --script=http-enum.nse 192.168.1.211
```

---

## 🛡️ **Nikto Usage**

### 📅 **Install Nikto**

Install Nikto Packages using apt package manager:

```bash
apt install nikto
```

---

### ⚙️ **Basic Commands**

View help options:

```bash
nikto -H
```

Display Nikto version:

```bash
nikto -Version
```

Update Nikto to the latest version:

```bash
nikto -update
```

Check the database for inconsistencies or missing entries:

```bash
nikto -dbcheck
```

List available plugins and their status:

```bash
nikto -list-plugins
```

📌 **Quick Reference:**

```bash
nikto -H              # Help
nikto -Version        # Show version
nikto -update         # Update tool
nikto -dbcheck        # Check DB integrity
nikto -list-plugins   # List plugins
```

---

### 🔎 **Basic Scanning**

Perform a basic scan of a web server:

```bash
nikto -h 192.168.1.211
```

Scan a web application with full URL:

```bash
nikto -h http://192.168.1.204/
```

Scan a web server running specifically on port 80:

```bash
nikto -h http://192.168.1.204:80
```

Scan a web server’s CGI-BIN directory:

```bash
nikto -h http://192.168.1.204/cgi-bin/
nikto -h http://192.168.1.204:2222 -C all
```

Specify the port explicitly during a scan:

```bash
nikto -h 192.168.1.204 -port 80
```

Scan a non-standard port (e.g., port 2222):

```bash
nikto -h 192.168.1.211 -port 2222
```

---

## 🌐 **Using Proxies**

Scan a target through a proxy server:

```bash
nikto -host 192.168.1.35 -useproxy http://127.0.0.1:8080
```

Scan a specific URL through a proxy:

```bash
nikto -host http://192.168.1.30/dvwa/ -useproxy http://127.0.0.1:8080
```

Proxy scan example for a standard web server:

```bash
nikto -h http://192.168.1.31/ -useproxy http://127.0.0.1:8080
```

---

## 🧪 **Scanning CGI Directories**

Scan all common CGI directories:

```bash
nikto -C all -h 192.168.1.211
```

Scan CGI directories on a specific port:

```bash
nikto -C all -h 192.168.1.211 -port 80
```

Scan all CGI directories using Cgidir option:

```bash
nikto -Cgidir all -h 192.168.1.211
```

```bash
nikto -Cgidir all -h 192.168.1.211 -port 80
```

---

## 📂 **Scanning Multiple Targets**

Scan a list of targets mentioned in a file:

```bash
nikto -h targets.txt
```

---

## 📣 **Verbose Output**

Perform a scan with verbose output:

```bash
nikto -h http://192.168.1.31 -Display v
```

Verbose CGI scanning:

```bash
nikto -Cgidir all -h 192.168.1.211 -port 80 -Display v
```

```bash
nikto -Cgidir all -h 192.168.1.211 -port 80 -Display V
```

---

## ❌ **Disabling SSL, DNS Lookups, 404 Detection**

Disable DNS lookup and SSL:

```bash
nikto -h 192.168.1.31 -nolookup -nossl
```

Disable handling of HTTP 404 detection:

```bash
nikto -h 192.168.1.31 -no404
```

---

## 🌍 **Scanning Different Ports and HTTPS Sites**

Scan a server running on port 81:

```bash
nikto -h http://192.168.1.31:81
```

Scan an HTTPS site:

```bash
nikto -h https://192.168.1.31/demosite/
```

---

## 🔌 **Using Specific Plugins**

Scan using Apache XSS expectation plugin with verbose and debug mode:

```bash
nikto -Plugins "apache_expect_xss(verbose,debug)" -h 192.168.1.211 -port 80
```

Scan using the Shellshock vulnerability plugin:

```bash
nikto -Plugins "shellshock(verbose)" -h 192.168.1.211 -port 80
```

```bash
nikto -Plugins "shellshock" -h 192.168.1.211 -port 80
```

```bash
nikto -Plugins shellshock -h 192.168.1.211 -port 80
```

---

## 🎯 **Nikto Tuning Options**

Tuning allows targeting specific vulnerabilities during scans.

| **Tuning Code** | **Type**                                              |
| --------------- | ----------------------------------------------------- |
| 1               | Interesting File / Seen In Logs                       |
| 2               | Misconfiguration / Default File                       |
| 3               | Information Disclosure                                |
| 4               | Injection (XSS/Script/HTML)                           |
| 5               | Remote File Retrieval - Inside Web Root               |
| 6               | Denial Of Service                                     |
| 7               | Remote File Retrieval - Server Wide                   |
| 8               | Command Execution / Remote Shell                      |
| 9               | SQL Injection                                         |
| 0               | File Upload                                           |
| a               | Authentication Bypass                                 |
| b               | Software Identification                               |
| c               | Remote Source Inclusion                               |
| x               | Reverse Tuning Options (Include All Except Specified) |

---

### 🧠 **Tuning Examples**

Scan specifically for interesting files:

```bash
nikto -h http://192.168.1.31/ -Tuning 1
```

Scan specifically for misconfigurations:

```bash
nikto -h http://192.168.1.31/ -Tuning 2
```

Scan for information disclosure vulnerabilities:

```bash
nikto -h http://192.168.1.31/ -Tuning 3
```

Scan all vulnerabilities except specific tuning options:

```bash
nikto -C all -h 192.168.1.211 -port 80 -Tuning x
```

---

## 🕵️ **Custom User Agent And Proxy Usage**

Set a custom user-agent during scan:

```bash
nikto -h http://192.168.1.31 -useragent "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:15.0) Gecko/20100101 Firefox/15.0.1"
```

Use a custom user-agent and route traffic through a proxy:

```bash
nikto -h http://192.168.1.236:2222 -useragent "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:15.0) Gecko/20100101 Firefox/15.0.1" -useproxy http://127.0.0.1:8080
```

---

## 💡 **Extra Tips**

* Always run Nikto and WhatWeb with `-ssl` when testing HTTPS endpoints.
* Update Nikto regularly to ensure you have the latest vulnerability checks.
* ⚠️ When scanning sensitive or live environments, avoid using Denial of Service tuning unless you have permission.
