🔸🔹🔸🔹🔸🔹🔸🔹🔸🔹🔸🔹🔸🔹🔸🔹

🧰 **🔥 Dnsenum – DNS Enumeration Tool 🔥**

🔸🔹🔸🔹🔸🔹🔸🔹🔸🔹🔸🔹🔸🔹🔸🔹

dnsenum is a Perl-based DNS enumeration tool designed to automate the process of gathering various DNS records, including subdomains, mail servers, nameservers, and zone transfer testing. It's useful for penetration testers and red teamers during the reconnaissance phase.

---

🧪 **Basic Usage**

Use the following commands to get started with dnsenum.

### 🔹 Display Help Menu
```bash
dnsenum --help
```
> This command lists all available options and usage syntax for dnsenum.

### 🔹 Verbose Scan on a Domain
```bash
dnsenum -v tesla.com
```
> Performs verbose DNS enumeration on tesla.com, displaying detailed progress and results.

### 🔹 Verbose Scan on a Known Vulnerable Domain
```bash
dnsenum -v zonetransfer.me
dnsenum -v facebook.com
```
> Tests the enumeration process on zonetransfer.me, which is known for training and demo purposes.

### 🔹 Quick Scan
```bash
dnsenum zonetransfer.me
```

---

📂 **Default Wordlist**

The default DNS wordlist used by dnsenum is typically located at:
```bash
cat /usr/share/dnsenum/dns.txt | wc -l
```
> This shows how many entries exist in the default wordlist.

To view the content:
```bash
cat /usr/share/dnsenum/dns.txt
```

---

🌐 **Using a Custom DNS Server**

To perform enumeration using a specific DNS server:
```bash
dnsenum tesla.com --dnsserver edns69.ultradns.com
```
> This queries `edns69.ultradns.com` as the resolver instead of the system default.

---

🚀 **Advanced Usage Examples**

### 🔹 Using a Custom Wordlist with Multi-threading and Output Saving
```bash
dnsenum --threads 50 \
  -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt \
  -r -o tesla_domain tesla.com \
  --dnsserver edns69.ultradns.com
```
- `--threads` : Sets concurrency for faster brute-forcing.
- `-f` : Specifies a wordlist.
- `-r` : Enables reverse DNS lookups.
- `-o` : Saves results to the specified output file or directory.
- `--dnsserver` : Uses a custom DNS resolver.

### 🔹 Using a Larger Wordlist for Extended Enumeration
```bash
dnsenum --threads 50 \
  -f /usr/share/seclists/Discovery/DNS/all.txt \
  -R -o tesla_domain tesla.com \
  --dnsserver edns69.ultradns.com
```
> Use this with a more comprehensive list for thorough enumeration.

### 🔹 Internal Network Target with Custom Resolver
```bash
dnsenum --threads 64 \
  --dnsserver 10.10.10.224 \
  -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt \
  htbhost.htb
```
> Targeting an internal domain with a specified DNS server in a lab or corporate environment.

---

📌 **Option Breakdown**

| Option         | Description                                                       |
|----------------|-------------------------------------------------------------------|
| `-f`           | File path to the subdomain brute-force wordlist                  |
| `-r`           | Enables reverse lookups on IP addresses found                    |
| `-o`           | Output file or folder for saving results                         |
| `--threads`    | Sets number of concurrent threads (improves speed)               |
| `--dnsserver`  | Specify custom DNS server to resolve queries                     |

---

🧷 **Installation Tip**

If dnsenum is not installed:
```bash
sudo apt install dnsenum
```
> This will install it from the system’s package repository..

---

🧠 **Pro Tips**

- Test dnsenum first on training domains like `zonetransfer.me` before using on production targets.
- Combine with tools like `massdns`, `amass`, and `subfinder` for wider coverage.
- Always use legal and authorized scopes for DNS enumeration.

