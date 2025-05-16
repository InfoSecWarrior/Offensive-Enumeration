# 🧰 Feroxbuster 

**Feroxbuster** is a fast, simple, recursive content discovery tool written in Rust. It helps in discovering hidden files and directories on web servers by sending HTTP requests to various paths.

---

## 🔗 Official Repository

[https://github.com/epi052/feroxbuster](https://github.com/epi052/feroxbuster)

---

## ✅ Installation

Install Feroxbuster using the package manager:

```bash
apt install feroxbuster
```

---

## 🖥️ Basic Usage

To display the help menu and see available options:

```bash
feroxbuster -h
```

This will list all flags, arguments, and usage examples.

---

## 🌐 Scanning a Target URL

To perform a basic scan of a target URL:

```bash
feroxbuster --url=http://192.168.1.21
```

This will recursively search for directories and files on the specified server.

---

## 🧾 Filtering HTTP Status Codes

### 🔹 To scan and ignore 403 Forbidden responses:

```bash
feroxbuster --url=http://192.168.1.211 --filter-status 403
```

### 🔹 To scan and ignore multiple status codes like 403, 404, and 500:

```bash
feroxbuster --url=http://192.168.1.211 --filter-status 403,404,500
```

> 💡 Filtering helps you focus only on meaningful results.

---

## 🛠️ Using Custom Wordlist and Threads

### 🔹 To use a custom wordlist and set the number of concurrent threads:

```bash
feroxbuster --url=http://192.168.1.211 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 10
```

* `-w`: Specifies the wordlist
* `-t`: Sets the number of concurrent threads

---

## 🕵️‍♂️ Scanning a Public Website

To scan a public website:

```bash
feroxbuster --url https://lacity.gov/
```

🔍 This will attempt to discover hidden content on the target site.

---

## 🚫 Filtering Status Codes on Public Sites

To scan and ignore 403 Forbidden responses:

```bash
feroxbuster --url https://lacity.gov/ --filter-status 403
```

---

## 📂 Using Wordlists with Output Files

To perform a scan using a custom wordlist and save the output to a file:

```bash
feroxbuster -u http://192.168.1.185/ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3.medium.txt -t 10 -o 192.168.31.74-feroxbuster.txt
```

* `-u`: Target URL
* `-w`: Wordlist
* `-t`: Threads
* `-o`: Output file path

---

## 🔁 Controlling Recursive Depth

Limit recursion depth:

```bash
feroxbuster --url=http://192.168.1.211 --depth 2
```

* Controls how deep the scan goes into nested directories

---

## ⏱️ Setting Timeout

Set request timeout:

```bash
feroxbuster --url=http://192.168.1.211 --timeout 10
```

* Prevents hanging on slow servers

---

## 🕵️ Using a Proxy

Route traffic through a proxy:

```bash
feroxbuster --url=http://192.168.1.211 --proxy http://127.0.0.1:8080
```

---

## 🛠️ Custom User-Agent

Set a custom User-Agent header:

```bash
feroxbuster --url=http://192.168.1.211 --user-agent "Mozilla/5.0 (Pentest Scanner)"
```

---

## 🚀 Advanced Targeting

### 📃 Using Multiple Targets

Specify multiple targets at once using a file:

```bash
feroxbuster --stdin < targets.txt
```

**Example `targets.txt`:**

```
http://192.168.1.1
http://192.168.1.2
http://192.168.1.3
```

---

## 🔁 Resuming a Scan

Resume an interrupted scan using the saved output:

```bash
feroxbuster --resume-from resume-state.json
```

* Resume the scan instead of starting over

---

## 🔗 Extracting Links from Responses

Enable link extraction from responses:

```bash
feroxbuster --url=http://192.168.1.211 --extract-links
```

---

## 📉 Handling Rate Limits

Limit the number of requests per second to avoid server bans:

```bash
feroxbuster --url=http://192.168.1.211 --rate-limit 50
```

* Helps when scanning production environments without causing disruption

---

## 🧩 Using File Extensions

Target specific file extensions like `.php`, `.html`, or `.txt`:

```bash
feroxbuster --url=http://192.168.1.211 --extensions php,html,txt
```

* Bruteforces with custom extensions appended to each wordlist entry

---

## 🧪 Full Example Command

A full command combining several options:

```bash
feroxbuster --url=http://192.168.1.211 -w /usr/share/seclists/Discovery/Web-Content/common.txt -x php,html,txt -t 30 --filter-status 403,404,500 --depth 3 --timeout 15 --rate-limit 100 --proxy http://127.0.0.1:8080 -o /tmp/feroxbuster-results.txt
```

* High-speed, controlled scan with file extension targeting and proxy routing

---

## ❗ Troubleshooting Tips

* Use `-vvv` for detailed debugging output
* Always verify wordlist paths and proxy settings
* Try `--no-recursion` if facing huge directories without meaningful results
* Check firewall and WAF protections which may block scans silently
* Respect scope boundaries and ethical hacking rules
* Use smaller wordlists first to avoid unnecessary load
* Consider scheduling scans during maintenance windows
* Be careful scanning login-protected areas (session tokens might expire)
* Monitor proxy tools like Burp Suite to analyze real-time traffic

---

## 📋 Feroxbuster Quick Cheatsheet

| Option            | Description                           |
| ----------------- | ------------------------------------- |
| `-u`              | Set target URL                        |
| `-w`              | Set wordlist                          |
| `-t`              | Number of threads                     |
| `-o`              | Output to file                        |
| `--depth`         | Recursion depth                       |
| `--timeout`       | Request timeout in seconds            |
| `--proxy`         | Use a proxy server                    |
| `--extensions`    | Add file extensions (e.g., php, html) |
| `--filter-status` | Filter unwanted HTTP status codes     |
| `--user-agent`    | Set custom User-Agent                 |
| `--rate-limit`    | Requests per second                   |
| `--extract-links` | Extract links from response bodies    |
| `--resume-from`   | Resume from saved state               |

---


