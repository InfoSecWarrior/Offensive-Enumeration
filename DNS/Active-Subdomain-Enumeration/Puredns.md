# 🔧 **PUREDNS**

🔗 [PureDNS GitHub Repository](https://github.com/d3mondev/puredns)

**PureDNS** is a fast and powerful domain resolver and subdomain brute-forcing tool. It supports filtering wildcard domains and DNS poisoning protection, and works best with tools like **massdns** and **dnsvalidator**.

---

## 📋 **Prerequisites**

### ⚡ **Step 1: Install MassDNS**
**MassDNS** is a high-performance DNS stub resolver required by PureDNS.

```bash
cd /opt
```
```bash
git clone https://github.com/blechschmidt/massdns.git
```
```bash
cd massdns
```
```bash
make
```
```bash
make install
```

---

### ⚙️ **Step 2: Install PureDNS**
**PureDNS** is written in Go. Install it with:

```bash
go install github.com/d3mondev/puredns@v2@latest
```
```bash
cp -v /root/go/bin/puredns /usr/local/bin
```

---

### 🛠️ **Step 3: Install dnsvalidator**
**DNSValidator** is used to prepare a list of valid public resolvers.

```bash
wget https://public-dns.info/nameservers-all.txt -O /opt/nameservers-all.txt
```
```bash
cd /opt
```
```bash
git clone https://github.com/vortexau/dnsvalidator.git
```
```bash
cd dnsvalidator
```
```bash
pip install -r requirements.txt
```
```bash
python3 setup.py install
```
```bash
dnsvalidator
```

➡️ **Help Command:**
```bash
dnsvalidator -h
```

---

### 🧹 **Step 4: Additional Resolver Sources**

```bash
git clone https://github.com/trickest/resolvers.git
```
```bash
wget https://public-dns.info/nameservers.txt
```
```bash
wget https://raw.githubusercontent.com/danielmiessler/SecLists/master/Miscellaneous/dns-resolvers.txt
```
```bash
cat /usr/share/seclists/Miscellaneous/dns-resolvers.txt | wc -l
```

✅ **Validate & output resolver list:**
```bash
dnsvalidator -tL /opt/nameservers-all.txt -threads 50 -o /opt/resolvers.txt
```

---

## 📌 **Usage Basics**

### 🔎 **Check Version**
```bash
puredns -v
```

### 📌 **Help Menus**
```bash
puredns -h
```
```bash
puredns bruteforce -h
```

---

## 💥 **Bruteforce Mode Examples**

🔹 **Basic bruteforce:**
```bash
puredns bruteforce /opt/subdomain-wordlists/best-dns-wordlist.txt google.com
```

🔇 **Quiet mode:**
```bash
puredns bruteforce /opt/subdomain-wordlists/six2dez.txt google.com -q
```

🛠️ **Use custom resolvers:**
```bash
puredns bruteforce /opt/subdomain-wordlists/all-subdomains.txt -r /opt/resolvers.txt google.com
```

📂 **Save output + quiet mode:**
```bash
puredns bruteforce /opt/subdomain-wordlists/all-subdomains.txt -r /opt/resolvers.txt google.com --write google_valid_domains.txt -q
```

🎯 **High batch size & wildcard filtering:**
```bash
puredns bruteforce /opt/subdomain-wordlists/all-subdomains.txt -r /opt/resolvers.txt google.com -q -l 500 --wildcard-batch 1000000 -w google_valid_domains.txt
```

📊 **Larger brute-force:**
```bash
puredns bruteforce /opt/subdomains/master_subdomains_wordlist.txt -l 5000 --wildcard-batch 1000000 -r /opt/my-resolvers/resolvers2.txt tesla.com
```

🟧 **Wildcard filter on different wordlist:**
```bash
puredns bruteforce /opt/subdomain-wordlists/dns-subdomain-master.txt -r /opt/resolvers.txt google.com --wildcard-batch 100000 -w google.com.txt
```

---

## 📚 **Using SecLists Wordlists**

🚗 **Run 20k list on Tesla:**
```bash
puredns bruteforce /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -r /opt/resolvers.txt -l 50 --wildcard-batch 1000 -w tesla_valid_domains.txt tesla.com
```

🔍 **Run on Google:**
```bash
puredns bruteforce /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -r /opt/resolvers.txt google.com --wildcard-batch 100000 -w google.com.txt
```

🔁 **Skip wildcard validation:**
```bash
puredns bruteforce /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -r /opt/resolvers.txt tesla.com --wildcard-batch 100000 --skip-wildcard-validation -w tesla.com.txt
```

🔎 **View valid domains:**
```bash
cat tesla_valid_domains.txt
```

---

## 🛠️ **Generate Wordlist with MkSub**

🔗 [MkSub Repo](https://github.com/trickest/mksub)

📝 **Generate wordlist:**
```bash
mksub -d tesla.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -o tesla_wordlist.txt
```

---

## 🟢 **Resolve Mode**

📚 **Help for resolve:**
```bash
puredns resolve -h
```

📝 **Resolve a generated list:**
```bash
puredns resolve tesla_wordlist.txt -r /opt/my-resolvers/resolvers2.txt
```

📂 **Resolve from saved list:**
```bash
puredns resolve tesla.com.txt -r /opt/resolvers.txt
```

---

