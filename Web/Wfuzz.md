# 🐞  Wfuzz - Web Application Fuzzing Tool

**Wfuzz** is a powerful **web application security tool** mainly used for brute forcing web applications. It's a go-to during **penetration testing** for discovering:

* 🔍 **Hidden directories and files** on a web server
* 🔐 **Login credentials** (usernames/passwords) via brute-force
* 📌 **Parameters or injection points** (for testing SQLi, XSS, etc.)
* 🍪 **Custom header or cookie vulnerabilities**

At its core, **Wfuzz** sends a high number of HTTP requests using **payloads or wordlists**, and then filters and analyzes the responses to detect interesting behavior such as:

✅ **Status codes** (e.g., 200, 403, 404)
📏 **Content size or word count**
🧵 **Line or character differences**

---

# 🎯 Main Features

* 📂 **Directory/file fuzzing** (finding hidden files)
* 🔐 **Login brute-forcing** (Basic/Digest/NTLM authentication)
* 📬 **GET/POST parameter fuzzing** (for injection testing)
* 🎭 **Header fuzzing** (like User-Agent, Referer, etc.)
* 🌐 **Proxy support** (e.g., Burp Suite, OWASP ZAP)
* 🧠 **Filtering options** by status code, size, lines, words, etc.

---

# **🚀 Simple Usage Example**

```bash
wfuzz -w /usr/share/wordlists/dirb/common.txt -u http://target.com/FUZZ
```

🔹 This command tries all words in `common.txt` at the `FUZZ` placeholder on the server.

---

# ⚙️ Installation

```bash
apt install wfuzz
```

---

# 📖 Help & Version

```bash
wfuzz --help
wfuzz --version
```

---

# 📁 Common Directory Fuzzing Examples

## ⬜️ **Example 1**

```bash
wfuzz -w /usr/share/secLists/.../directory-list-2.3-medium.txt http://192.168.1.31/FUZZ
```

## ⬜️ **Example 2**

```bash
wfuzz -w /usr/share/secLists/.../directory-list-2.3-medium.txt http://192.168.1.31/FUZZ/FUZZ
```

## ⬜️ **Example 3**

```bash
wfuzz -t 100 -mc 404 -hh 10701 -w /usr/share/secLists/... http://192.168.1.20/FUZZ
```

## ⬜️ **Example 4**

```bash
wfuzz -t 100 -mc 200 -w /usr/share/secLists/... http://192.168.1.30/dvwa/FUZZ/FUZZ
```

## ⬜️ **Example 5**

```bash
wfuzz -z list,index.php-login.php-admin.php -p 127.0.0.1:8080 -t 1 http://192.168.0.185/FUZZ
```

## ⬜️ **Example 6**

```bash
wfuzz -z list,index.php-login.php-admin.php -p 127.0.0.1:8080 http://192.168.0.200/FUZZ/FUZZ
```

## ⬜️ **Example 7**

```bash
wfuzz -z list,index.php-login.php-admin.php -p 127.0.0.1:8080 http://192.168.3.0/dvwa/FUZZ/FUZZ
```

## ⬜️ **Example 8**

```bash
wfuzz -z list,index.php-login.php-admin.php -p 127.0.0.1:8080 http://192.168.3.0/dvwa/FUZZ/FUZZ/FUZZ
```

## ⬜️ **Example 9**

```bash
wfuzz -w /usr/share/secLists/... -p 127.0.0.1:8080 -t 1 http://192.168.1.30/FUZZ/index.php
```

## ⬜️ **Example 10**

```bash
wfuzz --sc 200 -w /usr/share/secLists/... -p 127.0.0.1:8080 -t 1 http://192.168.1.30/FUZZ/index.php
```

## ⬜️ **Example 11**

```bash
wfuzz -t 100 -mc 404 -p 127.0.0.1:8080/HTTP -w /usr/share/secLists/... http://192.168.1.31/FUZZ/index.php
```

## ⬜️ **Example 12**

```bash
wfuzz -t 100 -hc 404 -p 127.0.0.1:8080:HTTP -z file,... http://192.168.1.31/FUZZ/
```

## ⬜️ **Example 13**

```bash
wfuzz -t 100 -hc 404 -p 127.0.0.1:8080:HTTP -z file,... -z list,index.php-admin.php-login.php http://192.168.1.31/FUZZ/FUZZ
```

## ⬜️ **Example 14**

```bash
wfuzz -p 127.0.0.1:8080 -z file,... -z list,index.php-index.html-admin.php http://192.168.1.31/FUZZ/FUZZ2
```

⬜️ **Example 15**

```bash
wfuzz -p 127.0.0.1:8080 -z list,phpmyadmin-db-admin -z list,index.php-index.html-admin.php http://192.168.1.31/FUZZ/FUZZ2
```

## ⬜️ **Example 16**

```bash
wfuzz -t 100 -mc 404 -z list,admin-upload-backup -z file,... http://192.168.1.31/FUZZ/FUZZ2
```

⬜️ **Example 17**

```bash
wfuzz -t 100 -hc 404 -p 127.0.0.1:8080:HTTP -z file,... http://192.168.1.31/FUZZ/FUZZ2
```

## ⬜️ **Example 18**

```bash
wfuzz --hc 404 -p 127.0.0.1:8080 -z file,/tmp/w1l.txt -z file,... http://192.168.1.31/FUZZ/FUZZ2
```

## ⬜️ **Example 19**

```bash
wfuzz --hc 404 -p 127.0.0.1:8080 -z file,/tmp/dir-list -z file,... -z list,php-php5-php4 http://192.168.1.31/FUZZ/FUZZ2.FUZZ3
```

---

# 🧠 Filtering Options

| Option | Description                            |
| ------ | -------------------------------------- |
| `-t`   | Threads for faster fuzzing             |
| `-mc`  | Match response codes (e.g., 200)       |
| `-hc`  | Hide response codes (e.g., 404)        |
| `-hh`  | Hide by content length                 |
| `-p`   | Proxy support (e.g., Burp Suite)       |
| `-z`   | Payloads: list, file, range, hex, etc. |
| `--sc` | Show only specific status codes        |

---

# **⚠️ Tips**

* 🔐 Combine `-z` list and file payloads for deep brute-force
* 🎯 Always monitor filters for accurate results
* 🧪 Test on allowed/authorized targets only!

---
