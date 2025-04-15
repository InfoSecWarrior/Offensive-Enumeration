# 📘 Massdns

**MassDNS** is a lightning-fast DNS stub resolver optimized for bulk lookups and reconnaissance tasks. It supports multiple DNS record types including A, AAAA, CNAME, and PTR—making it a powerful tool for subdomain enumeration workflows.

🔗 **Repository** — [github.com/blechschmidt/massdns](https://github.com/blechschmidt/massdns)

---

## ✅ Installation  
Clone the MassDNS repository:
```bash
git clone https://github.com/blechschmidt/massdns.git
```

Navigate to the MassDNS directory:
```bash
cd /opt/massdns/
```

Build the MassDNS binary:
```bash
make
```

Create a symbolic link to use MassDNS globally:
```bash
ln -s /opt/massdns/bin/massdns /usr/local/bin/massdns
```

---

## 🔍 Verify Installation  
Check if MassDNS is accessible and view available options:
```bash
massdns -h
```

---

## 📄 Resolver List  
MassDNS requires a list of DNS resolvers.

Check the provided resolvers list:
```bash
cat /opt/massdns/lists/resolvers.txt
```

Alternatively, you can use SecLists or custom resolver lists:
```bash
cat /usr/share/seclists/Miscellaneous/dns-resolvers.txt
```

🌐 **Online Resolver List** — [View here](https://raw.githubusercontent.com/blechschmidt/massdns/master/lists/resolvers.txt)

---

## 🛠️ Preparing the Wordlist

Copy a DNS wordlist from SecLists for brute-forcing subdomains:
```bash
cp /usr/share/seclists/Discovery/DNS/all.txt all.txt
```

Append the target domain (e.g., tesla.com) to each entry:
```bash
sed -i -e 's/$/.tesla.com/' all.txt
```

Preview the first 1000 entries:
```bash
head -n 1000 all.txt
```

Preview the last 1000 entries:
```bash
tail -n 1000 all.txt
```

---

## 🔎 Subdomain Enumeration Using A Records

Use MassDNS to resolve subdomains to A records:
```bash
massdns -r /usr/share/seclists/Miscellaneous/dns-resolvers.txt -t A all.txt -o S -w tesla_domain.txt
```

---

## 🔁 Using CNAME Resolution

Run MassDNS with CNAME type to discover alias relationships:
```bash
massdns -t CNAME -w tesla.com.CNAME.txt -o S -r /opt/resolvers.txt tesla.com.txt
```

---

## 🧹 Post-processing Results

Count how many results were returned:
```bash
cat tesla_domain.txt | wc -l
```

Clean up the output by removing record types and trailing dots:
```bash
sed -e 's/A.//; s/CN.//; s/\..$//' tesla_domain.txt
```

Or apply the changes directly to the file:
```bash
sed -i -e 's/A.//; s/CN.//; s/\..$//' tesla_domain.txt
```

---

## 🔎 CNAME Lookup for All Subdomains

```bash
massdns -r /opt/massdns/lists/resolvers.txt -t CNAME all.txt -o S -w tesla_domain_cname.txt
```

---

## 📦 JSON Output for Automation

Use the `-o J` option to produce JSON formatted results:
```bash
massdns -r /opt/resolvers/resolvers.txt -t A subdomains-top1million-5000.txt -o J -w tesla.com.json
```

---

## 🔁 PTR Record Enumeration

Reverse DNS lookups use PTR records to resolve IPs to hostnames.

📄 Format IP addresses for PTR lookup:
```bash
sed -i -e 's/$/.in-addr.arpa/' ip.txt
```

📂 Verify the file contents:
```bash
cat ip.txt
```

🚀 Perform PTR queries:
```bash
massdns -r /usr/share/seclists/Miscellaneous/dns-resolvers.txt -t PTR ip.txt -o S -w hosts-ptr.txt
```

🧹 Extract hostnames from the result:
```bash
cut -f3 -d " " hosts-ptr.txt
```

---

## 🎁 Bonus: Using Assetfinder with MassDNS

🛠️ Install assetfinder to discover subdomains from public sources:
```bash
apt install assetfinder
```

🔍 Count discovered subdomains for a domain:
```bash
assetfinder tesla.com | wc -l
```

🔄 Pipe assetfinder results directly into MassDNS:
```bash
assetfinder tesla.com | massdns -r /opt/massdns/lists/resolvers.txt -o S -w tesla_domain2.txt
```

