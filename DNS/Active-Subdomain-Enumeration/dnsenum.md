
---

# **dnsenum – DNS Enumeration Tool**  
**dnsenum** is a Perl-based DNS enumeration tool for gathering DNS records (subdomains, mail servers, nameservers, etc.) and testing zone transfers. Useful for **penetration testers** and **red teamers** during reconnaissance.

---

## **Basic Usage**  
### **Display Help Menu**  
```sh
dnsenum --help
```
Lists all available options and syntax.

### **Verbose Scan on a Domain**  
```sh
dnsenum -v tesla.com
```
Performs **detailed** DNS enumeration with progress updates.

### **Verbose Scan on a Known Vulnerable Domain (for training)**  
```sh
dnsenum -v zonetransfer.me
```
Tests enumeration on `zonetransfer.me`, a domain configured for demo purposes.

### **Quick Scan (Non-Verbose)**  
```sh
dnsenum zonetransfer.me
```
Runs a standard scan without verbose output.

---

## **Default Wordlist**  
The default wordlist is usually located at:  
```sh
cat /usr/share/dnsenum/dns.txt
```
Check the number of entries:  
```sh
cat /usr/share/dnsenum/dns.txt | wc -l
```

---

## **Using a Custom DNS Server**  
```sh
dnsenum tesla.com --dnsserver edns69.ultradns.com
```
Queries `edns69.ultradns.com` instead of the system default.

---

## **Advanced Usage**  
### **Custom Wordlist + Multi-threading + Output Saving**  
```sh
dnsenum --threads 50 \
  -f /usr/share/seclists/Discovery/DNS/subdomains-topmillion-5000.txt \
  -r -o tesla_domain.txt tesla.com \
  --dnsserver edns69.ultradns.com
```
- `--threads 50`: Faster brute-forcing with concurrency.  
- `-f`: Specifies a custom wordlist.  
- `-r`: Enables reverse DNS lookups.  
- `-o`: Saves results to a file.  

### **Extended Enumeration (Larger Wordlist)**  
```sh
dnsenum --threads 50 \
  -f /usr/share/seclists/Discovery/DNS/all.txt \
  -r -o tesla_domain.txt tesla.com \
  --dnsserver edns69.ultradns.com
```

### **Internal Network Enumeration**  
```sh
dnsenum --threads 64 \
  --dnsserver 10.10.10.224 \
  -f /usr/share/seclists/Discovery/DNS/subdomains-topmillion-110000.txt \
  htbhost.htb
```
For **internal domains** (e.g., HackTheBox, corporate networks).

---

## **Option Breakdown**  
| Option          | Description |
|-----------------|-------------|
| `-f <file>`     | Custom subdomain brute-force wordlist |
| `-r`            | Reverse DNS lookups on found IPs |
| `-o <file>`     | Save results to a file/folder |
| `--threads <N>` | Concurrent threads (faster scans) |
| `--dnsserver`   | Use a custom DNS resolver |

---

## **Installation**  
On Debian/Ubuntu:  
```sh
sudo apt install dnsenum
```

---

## **Pro Tips**  
✔ Test on **zonetransfer.me** before real targets.  
✔ Combine with **Amass, MassDNS, Subfinder** for better coverage.  
✔ Always ensure **legal authorization** before scanning.  

---

