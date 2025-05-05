# 🌐 **WebDAV Enumeration**

WebDAV (Web Distributed Authoring and Versioning) enumeration is the process of discovering accessible resources, capabilities, and potential vulnerabilities on a WebDAV-enabled server. This guide outlines techniques and tools used to interact with and test WebDAV services for security weaknesses.

---

## 🔍 **WebDAV Enumeration Techniques**

### 1️⃣ **Identify WebDAV Support**

Use the `OPTIONS` HTTP method via `curl` to check if WebDAV is enabled on the server:

```bash
curl -X OPTIONS http://192.168.31.61/webdav/
```

📩 **Request Example**

```
OPTIONS /webdav/ HTTP/1.1
Host: 192.168.1.36
Cache-Control: max-age=0
Accept-Language: en-GB,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```

📨 **Response Example**

```
HTTP/1.1 200 OK
Date: Thu, 24 Apr 2025 10:50:01 GMT
Server: Apache/2.4.62 (CentOS Stream) OpenSSL/3.2.2
DAV: 1,2
MS-Author-Via: DAV
Allow: OPTIONS, GET, HEAD, POST, DELETE, TRACE, PROPFIND, PROPPATCH, COPY, MOVE, LOCK, UNLOCK
Content-Length: 0
Keep-Alive: timeout=5, max=100
Connection: Keep-Alive
Content-Type: httpd/unix-directory
```

🔎 Look for WebDAV-related HTTP methods in the `Allow` header:

* PROPFIND
* PROPPATCH
* MKCOL
* COPY
* MOVE
* LOCK
* UNLOCK

Presence of these methods confirms WebDAV support ✅

---

### 2️⃣ **Use Nmap For Deeper Analysis**

🔧 **Upload a test PHP file:**

```bash
curl -v -X PUT -d "<?php phpinfo(); ?>" http://192.168.1.36/webdav/phpinfo.php
```

🔍 **Run Nmap scripts:**

```bash
nmap -p 80 --script=http-methods.nse --script-args http-methods.url-path='/webdav/' target-ip
```

🔬 **Full scan with OS detection, versioning, and scripts:**

```bash
nmap -v -sT -sV -A -O -p 80 --script=http-methods.nse --script-args http-methods.url-path='/webdav/' target-ip
```

---

### 3️⃣ **Test With Davtest**

🛠️ **Install:**

```bash
apt install davtest
```

📊 **Run tests:**

```bash
davtest -url http://192.168.1.36/webdav/
```

With authentication:

```bash
davtest -url http://target-ip/webdav/ -auth username:password
```

Checks for:

* Writable directories
* Upload execution
* File validation bypasses

---

### 4️⃣ **Use a WebDAV Client (Cadaver)**

💻 **Install Cadaver:**

* Debian/Ubuntu:

```bash
apt install cadaver
```

* RHEL/CentOS:

```bash
yum install cadaver
```

🔗 **Connect:**

```bash
cadaver http://target-ip/webdav/
```

🧱 **Basic commands inside cadaver:**

```
ls              # List contents
put file.txt    # Upload file
get file.txt    # Download file
delete file.txt # Delete file
mkdir dir       # Create directory
```

---

### 5️⃣ **Brute Force Authentication (If Protected)**

🔐 **Use `hydra`:**

```bash
hydra -l username -P /path/to/passwords.txt -s 80 -f target-ip http-head "/webdav"
```

Useful for testing HTTP Basic/Digest Auth.

---

### 6️⃣ **Manual Upload And Deletion (Test Writable Access)**

📝 **Test file uploads with `curl`:**

```bash
curl -T test.txt http://target-ip/webdav/test.txt
```

🗑️ **Test deletion:**

```bash
curl -X DELETE http://target-ip/webdav/test.txt
```

🔐 **Authenticated uploads and deletions:**

```bash
curl -u username:password -T test.txt http://target-ip/webdav/
curl -u username:password -X DELETE http://target-ip/webdav/test.txt
```

---

### 7️⃣ **Check for Misconfigured Access Controls**

🚨 **Indicators:**

* Anonymous upload/delete access
* Executable file types (.php, .asp, .aspx)
* No auth prompt
* Directory browsing enabled

⚠️ **Potential impact:** **Remote Code Execution (RCE)**

🔎 **What to check:**

* Writable directories
* Executable file types supported
* Directory listing exposed
* Weak or default login credentials
* Over-permissive file permissions (e.g., `chmod 777`)

---

## 💡 **Basic WebDAV Interaction Using Curl**

### 📄 **Send OPTIONS Requests**

```bash
curl -v -X OPTIONS http://192.168.1.40/webdav/
```

```bash
curl -v -k -X OPTIONS https://192.168.1.40/webdav/
```

### 📤 **Upload Files Using PUT**

```bash
curl -T tesla.com_ips.txt http://192.168.1.30/webdav/tesla.com_ips.txt
```

```bash
curl -X PUT -d "hi" http://192.168.1.40/webdav/1.txt
```

```bash
curl -v -u dev:1234 -d "Test" -X PUT http://192.168.1.35/webdav/test.txt
```

### 🗑️ **Delete Files Using DELETE**

```bash
curl -v -u dev:1234 -X DELETE http://192.168.1.35/webdav/test.txt
```

### 🔐 **Send Authenticated OPTIONS Requests**

```bash
curl -v -u dev:1234 -X OPTIONS http://192.168.1.40/test/
```

---
