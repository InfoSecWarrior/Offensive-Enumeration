# 🛠️ Dirsearch

**A powerful, fast, and easy-to-use command-line tool designed to brute force directories and files on web servers efficiently.**

**Dirsearch - Directory Brute Forcing**

---

## 📦 Installation

### Install using APT package manager:

```bash
apt install dirsearch
```

### Or clone the repository from GitHub:

```bash
cd /opt/
```

```bash
git clone https://github.com/maurosoria/dirsearch.git
```

```bash
cd /opt/dirsearch/
```

```bash
pip3 install -r requirements.txt
```

```bash
python3 dirsearch.py --version
```

```bash
ln -s /opt/dirsearch/dirsearch.py /usr/local/bin/dirsearch
```

---

## ⚙️ Configuration

Edit main configuration file if necessary:

```bash
vim /etc/dirsearch/config.ini
```

```ini
[general]
threads = 25
recursive = False
deep-recursive = False
force-recursive = False
recursion-status = 200-399,401,403
max-recursion-depth = 0
exclude-subdirs = %%ff/,.;/,..;/,;/,./,../,%%2e/,%%2e%%2e/
random-user-agents = False
max-time = 0
exit-on-error = False

[dictionary]
default-extensions = php,aspx,jsp,html,js
force-extensions = False
overwrite-extensions = False
lowercase = False
uppercase = False
capitalization = False
# wordlists = /path/to/wordlist1.txt,/path/to/wordlist2.txt


[request]
http-method = get
follow-redirects = False

[connection]
timeout = 7.5
delay = 0
max-rate = 0
max-retries = 1

[advanced]
crawl = False

[view]
full-url = False
quiet-mode = False
color = True
show-redirects-history = False

[output]
report-format = plain
autosave-report = True
autosave-report-folder = reports/
```

---

## 📂 View Default Wordlist

```bash
cat /usr/lib/python3/dist-packages/dirsearch/db/dicc.txt
```

```bash
cat /opt/dirsearch/db/dicc.txt
```

---

## 🚀 Basic Usage

### Display help menu:

```bash
dirsearch --help
```

### Scan a target URL:

```bash
dirsearch -u http://192.168.1.211
```

### Set number of threads:

```bash
dirsearch -u http://192.168.1.31 -t 100
```

### Use a custom wordlist:

```bash
dirsearch -u http://192.168.1.31 -t 100 -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files.txt
```

```bash
dirsearch -u http://192.168.1.31 -t 100 -w /usr/share/seclists/Discovery/Web-Content/raft-large-files.txt
```

---

## 🔁 Recursive Scanning

### Recursive brute-forcing:

```bash
dirsearch -u http://192.168.1.211 -r -t 100
```

### Control recursion depth (e.g., 3 levels):

```bash
dirsearch -u http://192.168.1.211 -r -R 3 -t 100 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt
```

### Limit recursion depth:

```bash
dirsearch -u http://192.168.1.211 -R 2 -r -t 300
```

---

## 🧹 Extension Based Scanning

### Scan for all file types:

```bash
dirsearch -u http://192.168.1.211 -t 100 -e "*"
```

### Scan for specific file extensions:

```bash
dirsearch -u http://192.168.1.211 -t 100 -e "php"
```

### Scan for multiple extensions:

```bash
dirsearch -u http://192.168.1.211 -t 100 -e "php,sql"
```

---

## 🌐 Proxy Support

### Use a proxy:

```bash
dirsearch -u http://192.168.1.30/dvwa/ --proxy=http://127.0.0.1:8080
```

### Use a proxy list:

```bash
--proxy-list=proxies.txt
```

### Example with proxy, forced extension, and wordlist:

```bash
dirsearch -u http://192.168.1.30/dvwa -w /opt/files-name.txt -t 100 --proxy=http://127.0.0.1:8080 -f -e "php"
```

---

## 📜 Example Wordlist Entries

```bash
vim /opt/wordlist.txt
```

### Common Entries:

```
1. index
2. app
3. styles
4. login
5. dashboard
6. profile
7. api
8. main
9. config
10. database
11. userController
12. .env
13. README
14. webpack.config
15. package
```

```bash
dirsearch -u http://192.168.1.211 -w /opt/wordlist.txt -t 1 --proxy=http://127.0.0.1:8080 -f -e '*'
```

---

## 📁 Wordlist Management

### Use a specific wordlist:

```bash
dirsearch -u http://192.168.1.211 -t 100 -w /opt/files-name.txt
```

### Combine multiple wordlists:

```bash
dirsearch -u http://192.168.1.211 -t 100 -w /path/to/list1.txt,/path/to/list2.txt
```

### Use predefined large lists:

```bash
dirsearch -u http://192.168.1.211 -t 100 -w /usr/share/seclists/Discovery/Web-Content/raft-large-files.txt
```

---

## 🗞 HTTP Methods

### Change HTTP method (e.g., POST):

```bash
dirsearch -u http://192.168.1.211 --http-method=POST
```

### With proxy and custom method:

```bash
dirsearch -u http://192.168.1.211 --proxy=http://127.0.0.1:8080 --http-method=POST
```

---

## 🕵️‍♂️ User-Agent Customization

### View available user agents:

```bash
cat /usr/share/seclists/Fuzzing/User-Agents/user-agents-whatismybrowserdotcom-small.txt
```

### Use a custom user agent:

```bash
dirsearch -u http://192.168.1.211 --user-agent="Mozilla/5.0 (iPhone; CPU iPhone OS 12_0 like Mac OS X)"
```

### Enable random user-agents in config:

```ini
[general]
random-user-agents = True
```

---

## 🗒 Output Management

### Save results to file:

```bash
dirsearch -u http://192.168.1.211 -o result.txt
```

### Redirect output manually:

```bash
dirsearch -u http://192.168.1.211 > result1.txt
```

### Configure output format:

```ini
[reports]
report-format = plain
autosave-report = True
```

### Supported formats:

```
plain, simple, json, xml, md, csv, html
```

### Remove banner (useful for parsing or clean logs):

```bash
dirsearch -u http://192.168.1.211 -b
```

---

## ❌ Exclude HTTP Status Codes

### Exclude 403:

```bash
dirsearch -u http://192.168.1.211 -x 403 -t 300
```

### Exclude multiple codes:

```bash
dirsearch -u http://192.168.1.211 -x 403,301,500-599 -t 300
```

### Include only specific codes:

```bash
dirsearch -u http://192.168.1.211 -i 200 -w /opt/files-name.txt
```

---

## 🔥 Advanced Examples

### Full scan with proxy, forced extensions:

```bash
dirsearch -u http://192.168.1.30/dvwa/ -w /opt/files-name.txt -t 100 --proxy=http://127.0.0.1:8080 -f -e "php,jsp,asp"
```

### Recursive scan with large wordlist:

```bash
dirsearch -u http://192.168.1.211 -r -R 3 -t 100 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt
```

### Forced extensions with multiple types:

```bash
dirsearch -u http://192.168.1.30/dvwa/ -f -e "php,asp,jsp" -t 100
```

---
