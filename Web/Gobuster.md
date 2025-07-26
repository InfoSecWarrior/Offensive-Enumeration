# 📌 **Gobuster**

Gobuster is a powerful and fast brute-forcing tool written in Go, designed for discovering hidden files, directories, DNS subdomains, and virtual hosts on a web server.

It is extremely useful during web penetration testing, red teaming, and bug bounty hunting.

🔗 **For more information, visit the official repository:**
👉 [Gobuster Repository](https://github.com/OJ/gobuster)

---

## ⚡ **Installation**

Install gobuster using the package manager:

```
apt install gobuster
```

---

## 🔍 **Checking Version**

Check the installed version:

```
gobuster version
```

---

## 🆘 **Displaying Help Menu**

View the general help menu:

Display help for specific modules:

```
gobuster dir --help
gobuster dns --help
```

---

## 📂 **Basic Directory Scan**

Perform a basic directory brute-force:

```
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://192.168.1.51
```

---

## 🗣 **Printing Verbose Output**

Enable verbose mode to display all requests:

```
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3.medium.txt -u http://192.168.1.51 -v
```

---

## 📏 **Identifying Content Length**

Display content length of each response:

```
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3.medium.txt -u http://192.168.1.51:81 -l
```

---

## ⚙️ **Using Multiple Concurrent Threads**

Set the number of concurrent threads:

```
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3.medium.txt -u http://192.168.1.51 -t 50
```

---

## 🚦 **Filtering Specific HTTP Status Codes**

```
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3.medium.txt -u http://192.168.1.51 -t 50 -s 403
```

```
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://192.168.1.51 -t 50 -s 200
```

```
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://192.168.1.51:81 -t 50 -s 200,302,403
```

---

## 🗂 **Searching For Specific File Extensions**

Search for specific file types like `.php`:

```
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://192.168.1.51 -s 200 -x php
```

Search multiple extensions:

```
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://192.168.1.51 -s 200 -x php,html
```

Using more extensions:

```
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://192.168.1.51 -t 10 -x php,html,sql
```

Massive extension search:

```
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://192.168.1.51 -s 200 -x php,inc.php,jsp,jsf,asp,aspx,do,action,cgi,pl,html,htm,js,css,json,txt,tar.gz,tgz -t 100
```

---

## 🔒 **Skipping SSL Certificate Verification**

```
gobuster dir -t 50 -x html,php,asp,aspx -k -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://192.168.1.51
```

```
gobuster dir -k -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u https://192.168.1.51 -s 200 -x php
```

---

## 💾 **Saving Output To A File**

```
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://192.168.1.51 -s 200 -x php,html -o results.txt
```

---

## 🌐 **Using Proxy**

Route requests through a proxy server:

```
gobuster dir -k -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://192.168.1.51 -x php -t 10 --proxy http://127.0.0.1:8080
```

Use proxy along with a custom User-Agent:

```
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://192.168.1.51 -a "Mozilla/5.0 (iPhone; CPU iPhone OS 11_4_1 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) FxiOS/12.1b10941 Mobile/15G77 Safari/605.1.15" -s 200 -x php,html -p http://127.0.0.1:8080
```

---

## 🌎 **DNS Subdomain Bruteforcing**

Perform DNS subdomain enumeration:

```
gobuster dns -d example.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```

* `-d` specifies the domain.
* `-w` specifies the wordlist.

---

## 🏠 **Virtual Host Bruteforcing**

Create a wordlist file:

```
vim /opt/virtual-Host.txt
```

Add the following hosts inside the file:

```
nicolas.local
phpadmin.local
www.subscribe.local
prototype.local
experts.local
mgk.local
newforum.local
result.local
www.prueba.local
cbf2.local
s114.local
spp.local
trident.local
mirror2.local
s112.local
sonia.local
nnov.local
www.china.local
alabama.local
photogallery.local
blackjack.local
lex.local
hathor.local
inc.local
xmas.local
tulip.local
and.local
common-sw1.local
betty.local
vo.local
armour.local
ai.local
infosec.local
www.armour.local
www.ai.local
www.infosec.local
```

Discover virtual hosts:

```
gobuster vhost -u http://192.168.1.51 -w /opt/virtual-Host.txt
```

* `-u` → Target URL.
* `-w` → Wordlist for hostnames.

---

## ⏳ **Setting Timeout For Requests**

```
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://192.168.1.51 --timeout 10s
```

---

## 📝 **Using Custom HTTP Headers**

```
gobuster dir -u http://192.168.1.51 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -H "Authorization: Basic dXNlcm5jpwYXNzd29yZA=="
```

---

## 🚀 **Full Example Command**

```
gobuster dir -u http://192.168.1.51 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 100 -s 200,204,301,302,307,403 -x php,html,txt -k -o /tmp/gobuster-results.txt
```

---

## 🛠 **Troubleshooting Tips**

* ✅ Always verify if the target is using HTTP or HTTPS.
* ✅ Use `-k` when dealing with invalid SSL certificates.
* ✅ Increase timeout with `--timeout` if encountering slow responses.
* ✅ Use `--proxy` when routing through Burp Suite or ZAP.

---

## 📑 **Gobuster Cheatsheet**

| **Option** | **Description**                      |
| ---------- | ------------------------------------ |
| `-u`       | Target URL                           |
| `-w`       | Wordlist                             |
| `-t`       | Threads (Concurrency)                |
| `-s`       | Filter status codes (e.g., 200, 403) |
| `-x`       | File extensions                      |
| `-k`       | Skip SSL verification                |
| `-o`       | Save output to file                  |
| `-a`       | Set custom User-Agent header         |
| `--proxy`  | Proxy server                         |
| `-l`       | Show content length                  |
| `-H`       | Add custom HTTP header               |
