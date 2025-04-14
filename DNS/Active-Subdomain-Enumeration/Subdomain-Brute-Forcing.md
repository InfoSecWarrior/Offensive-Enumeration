# 🔵 Subdomain Brute Forcing

Subdomain brute forcing is the process of discovering valid subdomains by brute-forcing DNS lookups against a target domain using a large list of potential subdomains.

---

## ✅ Types of Subdomain Brute Forcing

### ▶️ Forward Lookup Brute Force  
Attempts to resolve a list of common subdomains to IP addresses using DNS.

### ▶️ Reverse Lookup Brute Force  
Attempts to reverse-resolve IP addresses (e.g., from CIDR ranges or infrastructure) back to subdomains.

---

## 📚 Wordlists for Subdomain Enumeration

### 🟢 Recommended Wordlists  
- [SecLists by Daniel Miessler](https://github.com/danielmiessler/SecLists)  
- [Assetnote Wordlists](https://wordlists.assetnote.io)  
- [Jhaddix’s All.txt](https://gist.github.com/jhaddix/86a06c5dc309d08580a018c66354a056#file-all-txt)

---

## 🖥️ Local Setup (Kali / Parrot / Ubuntu)

```bash
sudo apt install seclists
cd /usr/share/seclists/Discovery/DNS/
```

### 🗂️ Useful files:  
- dns-Jhaddix.txt  
- subdomains-top1million-*

---

## 🔷 Download Wordlists

### Jhaddix All.txt

```bash
wget https://gist.githubusercontent.com/jhaddix/.../all.txt -O all.txt
cat all.txt > /opt/subdomain-wordlists/all-subdomain.txt
```

### Assetnote wordlists

```bash
mkdir -p /opt/Wordlists && cd /opt/Wordlists
wget -r --no-parent -R "index.html*" -e robots=off https://wordlists-cdn.assetnote.io/data/ -nH
```

---

## 🔷 Organize Your Wordlists

```bash
mkdir -p /opt/subdomain-wordlists

for file in $(find . -iname '*subdomain*'); do
  cp -v "$file" /opt/subdomain-wordlists/
done

for file in $(find . -iname '*dns*'); do
  cp -v "$file" /opt/subdomain-wordlists/
done
```

---

## 🔹 DNS Resolvers

For tools like massdns, you’ll need good resolvers:

```bash
cat /usr/share/seclists/Miscellaneous/dns-resolvers.txt
```

Or download the recommended one:

```bash
wget https://raw.githubusercontent.com/blechschmidt/massdns/master/lists/resolvers.txt
```

---

## 🛠️ Tools for Subdomain Brute Forcing

| Tool         | Description                                              | Link |
|--------------|----------------------------------------------------------|------|
| **Massdns**  | High-performance DNS stub resolver for bruteforce       | [GitHub ↗](https://github.com/blechschmidt/massdns) |
| **Findomain**| Fast subdomain discovery using multiple sources         | [GitHub ↗](https://github.com/Findomain/Findomain) |
| **Amass**    | Enumeration, scraping, brute force, and mapping         | [GitHub ↗](https://github.com/owasp-amass/amass) |
| **Sublist3r**| Fast passive subdomain enum                             | [GitHub ↗](https://github.com/aboul3la/Sublist3r) |
| **Knockpy**  | Python-based subdomain brute forcing tool               | [GitHub ↗](https://github.com/guelfoweb/knock) |

---

## ✅ Summary

- Use high-quality wordlists to increase brute-force effectiveness.  
- Combine passive and active tools.  
- Always verify results with resolvers to avoid false positives.  
- Brute force is still one of the most reliable ways to find hidden subdomains when passive methods fail.

---

## 🏱 Bonus Tip

Combine tools like Amass and Massdns with `dnsx` or `httpx` to validate and scan discovered subdomains for open services.

```bash
amass enum -brute -w all.txt -d target.com -o amass.txt
cat amass.txt | dnsx -a -resp-only
```

