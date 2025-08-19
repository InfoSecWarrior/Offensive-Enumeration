# 🌐 Sublist3r – Subdomain Enumeration Tool

**Sublist3r** is a Python-based tool designed to enumerate subdomains of websites using OSINT (Open Source Intelligence). It gathers subdomains using search engines like Google, Yahoo, Bing, Baidu, and more.

---

## 🔧 Installation

Clone the Sublist3r GitHub repository and install the dependencies:
```bash
git clone https://github.com/aboul3la/Sublist3r.git
```

Navigate into the tool’s directory:
```bash
cd Sublist3r/
```

Install required Python packages:
```bash
pip install -r requirements.txt
```

---

##  Help Menu

To view the help/usage instructions:
```bash
python sublist3r.py -h
```

---

## 🧪 Basic Usage

### 1. Enumerate Subdomains for a Target
```bash
python sublist3r.py -d tesla.com
```
This command runs subdomain enumeration on the target domain `tesla.com`.

### 2. Enable Bruteforce Mode
```bash
python sublist3r.py -d tesla.com -b
```
This enables bruteforce mode in addition to using search engines. It can be more thorough but slower.

---

## 🛠️ Additional Useful Options

| Option         | Description                                       |
|----------------|---------------------------------------------------|
| `-d`           | Target domain to enumerate                        |
| `-b`           | Enable bruteforce mode                            |
| `-t`           | Number of threads to use (default is 10)          |
| `-v`           | Enable verbose output                             |
| `-o`           | Output file to save the discovered subdomains     |
| `-p`           | Scan discovered subdomains for open ports         |
| `--enable-dns` | Enable DNS resolution of subdomains              |

---

## 💻 Example Command: Save output and Enable DNS Resolution
```bash
python sublist3r.py -d tesla.com -o tesla_subs.txt --enable-dns
```

---

## 🔧 Tips
- Sublist3r is ideal for quick, passive recon.
- Combine it with other tools like Amass, Findomain, or massdns for deeper enumeration.
- Some engines may limit API usage or block aggressive scanning; use with care.

