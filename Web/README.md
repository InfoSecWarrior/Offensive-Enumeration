# 🔍 Offensive Enumeration

A comprehensive collection of offensive enumeration techniques, tools, and exploits used in penetration testing and red teaming. This repository is organized by specific services and includes detailed enumeration methods, tools, and exploitation techniques.

---

## 📂 Repository Structure

This repository is structured into service-specific folders, each containing Markdown files that cover specific enumeration techniques and exploitation methods.

### 🕸️ Web Enumeration

Web enumeration focuses on identifying open ports, services, and potential vulnerabilities in web servers. The following topics are covered:

* **Ports:** Identifying open ports using Nmap and other tools.
* **Nmap Scanning:** Basic to advanced Nmap scans for HTTP services.
* **Service Version Detection:** Identifying running service versions.
* **Nmap Scripts:** Utilizing NSE scripts for web enumeration.
* **Directory Searching:** Discovering hidden directories using tools like DirSearch and Gobuster.

### 🌐 HTTP Methods

Identifying and exploiting HTTP methods to uncover potential attack vectors. Topics covered include:

* Available Methods
* File Upload Techniques
* Tools for Testing:

  * netcat
  * curl
  * nikto
  * davtest

### 📦 FTP Enumeration

Identifying and exploiting FTP services, including:

* Anonymous Login Testing
* Brute Forcing FTP Credentials
* Enumerating FTP Directories
* Tools:

  * ftp
  * Hydra
  * Nmap FTP Scripts

### 🛢️ MySQL Enumeration

MySQL database enumeration techniques, including:

* Identifying Open MySQL Ports
* Brute Forcing MySQL Credentials
* Database Structure Analysis
* Tools:

  * mysql
  * Nmap
  * Metasploit
  * sqlmap

### 📚 LDAP Enumeration

LDAP enumeration for identifying user accounts and other sensitive data:

* LDAP Service Discovery
* Extracting User Information
* Tools:

  * ldapsearch
  * Nmap LDAP Scripts

### 🖥️ RDP Enumeration

Identifying and enumerating RDP services to uncover potential vulnerabilities:

* Discovering RDP Services
* Checking Weak Credentials
* Exploiting RDP Misconfigurations
* Tools:

  * Nmap RDP Scripts
  * rdesktop
  * xfreerdp

### 🛠️ SSH Enumeration

Enumerating SSH services to identify potential weaknesses:

* Enumerating SSH Banner and Version
* Brute Forcing SSH Credentials
* Analyzing SSH Configurations
* Tools:

  * Nmap SSH Scripts
  * Hydra
  * ssh-audit

### 📡 Telnet Enumeration

Identifying and exploiting Telnet services:

* Checking for Open Telnet Ports
* Brute Forcing Telnet Logins
* Banner Grabbing and Analysis
* Tools:

  * telnet
  * Hydra
  * Nmap Telnet Scripts

### 🖥️ VNC Enumeration

Identifying and exploiting VNC services:

* Detecting Open VNC Ports
* Brute Forcing VNC Passwords
* Analyzing VNC Configuration
* Tools:

  * Nmap VNC Scripts
  * vncviewer
  * vncsnapshot

---

## 📄 Modules and Detailed Techniques

| File                                                     | Description                                                        |
| -------------------------------------------------------- | ------------------------------------------------------------------ |
| `Enumeration.md`                                         | Comprehensive overview of general web enumeration techniques.      |
| `HTTP-Methods.md`                                        | Detailed exploration of HTTP methods and potential attack vectors. |
| `Hydra-HTTP-Basic-Authentication-Brute-Force.md`         | Techniques for brute-forcing HTTP Basic Auth using Hydra.          |
| `Nmap-HTTP-NSE-Scripts.md`                               | A guide to using Nmap NSE scripts for HTTP services.               |
| `PHP-Version-Detection-and-Vulnerabilities.md`           | Detecting PHP versions and associated vulnerabilities.             |
| `WebDAV-Enumeration.md`                                  | Discovering and exploiting WebDAV vulnerabilities.                 |
| `Web-Server-Scanner.md`                                  | Scanning web servers with Nikto and DavTest.                       |
| `Shellshock-Remote-Command-Injection-(CVE-2014-6271).md` | Exploiting the Shellshock vulnerability.                           |
| `Nostromo-1.9.6-exploit.md`                              | Detailed exploitation of Nostromo web server.                      |
| `OpenLuck.md`                                            | Write-up on exploiting OpenLuck.                                   |
| `Upgrading to a Full Interactive Shell.md`               | Techniques for upgrading to a fully interactive shell.             |
| `FTP-Enumeration.md`                                     | Techniques for enumerating FTP services and directories.           |
| `MySQL-Enumeration.md`                                   | Identifying MySQL services and enumerating databases.              |
| `LDAP-Enumeration.md`                                    | Extracting user data through LDAP enumeration.                     |
| `RDP-Enumeration.md`                                     | Techniques for identifying and exploiting RDP services.            |
| `SSH-Enumeration.md`                                     | Methods for enumerating SSH services and configurations.           |
| `Telnet-Enumeration.md`                                  | Techniques for enumerating Telnet services.                        |
| `VNC-Enumeration.md`                                     | Identifying and exploiting VNC services.                           |

---

## 🛠 Tools Covered

* `nmap` - Network scanning and enumeration
* `Hydra` - Brute-forcing HTTP, FTP, SSH, Telnet, and VNC authentication
* `Nikto` - Web server vulnerability scanning
* `Gobuster` - Directory and file brute-forcing
* `DirSearch` - Web directory enumeration
* `DavTest` - Testing WebDAV vulnerabilities
* `netcat` - Network utility for reading/writing data
* `curl` - Command-line tool for transferring data
* `ftp` - FTP client for file transfer and enumeration
* `mysql` - MySQL client for database enumeration
* `ldapsearch` - LDAP querying tool
* `rdesktop` - Remote Desktop Protocol client
* `xfreerdp` - Free RDP client
* `ssh-audit` - SSH server auditing tool
* `telnet` - Telnet client for testing and enumeration
* `vncviewer` - VNC client for remote access
* `vncsnapshot` - Capture screenshots of VNC sessions

---

## 👥  Contributing

💪 **Got New Techniques or Tools?**
Your contributions can make this repository even better! If you have additional techniques, tools, or improvements, fork the repository and submit a pull request.

🔥 **Let’s Collaborate!**
Check out the open issues, suggest new ideas, or refine existing modules. Your input is invaluable!

[![Contribute](https://contrib.rocks/image?repo=InfoSecWarrior/Offensive-Enumeration)](https://github.com/InfoSecWarrior/Offensive-Enumeration)

---

##


