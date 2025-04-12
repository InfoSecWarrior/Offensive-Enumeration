# Gauplus

## 📦 GitHub Repository
🔗 [bp0lr/gauplus (GitHub)](github.com/bp0lr/gauplus)

## 🔍 Overview
gauplus is an enhanced version of **gau (GetAllUrls)** that fetches URLs from multiple sources, including:

- 📚 Wayback Machine  
- 🌐 Common Crawl  
- 🧪 VirusTotal  
- 🔍 URLScan.io  
- 📂 Other public archives

✅ It is useful for reconnaissance, discovering hidden endpoints, and extracting subdomains.

---

## ⚙️ Installation
Ensure that you have Go properly installed and configured, then run:

```bash
go install github.com/bp0lr/gauplus@latest
```

---

## 🛠️ Usage

### 🌐 Fetching URLs with gauplus
To retrieve archived URLs for a domain (e.g., tesla.com):

```bash
gauplus -t 5 -random-agent -subs tesla.com
```

### 🧾 Explanation of Flags:
- `-t 5` → 🧵 Sets the number of concurrent threads (default is 1; more threads = faster)
- `-random-agent` → 🎭 Uses a random user-agent to avoid blocks/rate limiting
- `-subs` → 🌍 Includes subdomains in the results

---

## 🔎 Extracting Only Subdomains
Since gauplus returns full URLs, we use **unfurl** to extract only the domain names:

```bash
cat tesla.com-gauplus.txt | unfurl -u domains
```

📁 Or to overwrite the file:

```bash
cat tesla.com-gauplus.txt | unfurl -u domains > tesla.com-gauplus.txt
```

📡 Or directly from gauplus:

```bash
gauplus -t 5 -random-agent -subs tesla.com | unfurl -u domains
```

---

## 💾 Saving the Output to a File
To save the extracted subdomains:

```bash
gauplus -t 5 -random-agent -subs tesla.com | unfurl -u domains > tesla.com-gauplus-output.txt
```

---

## 📋 Example Output
Running:

```bash
gauplus -t 5 -random-agent -subs tesla.com | unfurl -u domains
```

Might return:
```
www.tesla.com
shop.tesla.com
blog.tesla.com
api.tesla.com
energy.tesla.com
```

---

## ✅ Conclusion
🚀 gauplus is an effective tool for extracting URLs from multiple archives.  
🔐 It helps security researchers discover hidden subdomains and endpoints.  
⚡ When combined with **unfurl**, it allows quick and efficient subdomain enumeration.
