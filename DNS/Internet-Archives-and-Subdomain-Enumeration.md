## 🌐 Internet Archives and Subdomain Enumeration

Internet Archives are web crawlers and indexing systems that periodically crawl websites, storing historical snapshots of their content. These archives can be valuable for discovering subdomains that once existed but may no longer be publicly visible. By analyzing past records, we can:

- 🔍 Identify old and forgotten subdomains.
- 🧩 Perform permutations to find more valid subdomains.
- 🛡️ Enhance reconnaissance efforts in security research and penetration testing.

---

### 📂 Extracting Historical Subdomains

#### 🔎 Querying the Internet Archive for URLs
We use tools like `waybackurls` or `gau` (GetAllUrls) to fetch historical URLs for a target domain.

**Using waybackurls**
```bash
waybackurls tesla.com > tesla.com-waybackurls.txt
```

**Using gau (GetAllUrls)**
```bash
gauplus -t 5 -random-agent -subs tesla.com > tesla.com-gauplus.txt
gau example.com > urls.txt
```
This will output a list of archived URLs related to `example.com`.

---

### 🧵 Extracting Unique Subdomains from URLs
Since we only need subdomains (not full URLs), we process them using `unfurl`, which extracts domain parts.
```bash
cat urls.txt | unfurl -u domains | sort -u > subdomains.txt
```
- `unfurl -u domains` : Extracts unique domains from the URL list.
- `sort -u` : Ensures we get only unique subdomains.

**Example output in `subdomains.txt`:**
- blog.example.com  
- mail.example.com  
- dev.example.com

---

### 🧬 Generating Permutations of Subdomains
To discover more potential subdomains, we can use `dnsgen`:
```bash
cat subdomains.txt | dnsgen - > permutations.txt
```
This generates possible subdomain variations like:
- admin.blog.example.com  
- test.mail.example.com  
- dev2.example.com

---

### ✅ Validating and Resolving Subdomains

#### Using `dnsx` (DNS Resolution)
```bash
cat permutations.txt | dnsx -resp > valid_subdomains.txt
```
- `dnsx` resolves the domains and checks if they exist.
- `-resp` : Retrieves response data for further analysis.

#### Using `httprobe` (Checking HTTP/S Services)
```bash
cat valid_subdomains.txt | httprobe > live_subdomains.txt
```
- `httprobe` checks which subdomains have active web services.

---

### ⚙️ Automating the Process
To streamline the entire workflow:
```bash
echo "example.com" | waybackurls | unfurl -u domains | sort -u | tee subdomains.txt
cat subdomains.txt | dnsgen - | tee permutations.txt
cat permutations.txt | dnsx -resp | tee valid_subdomains.txt
cat valid_subdomains.txt | httprobe | tee live_subdomains.txt
```
This ensures a smooth pipeline from historical data to identifying active subdomains.

---

### ✅ Conclusion
By using Internet Archives along with tools like `unfurl`, `dnsgen`, `dnsx`, and `httprobe`, we can effectively enumerate subdomains — even those that have vanished from the public eye 🕵️‍♂️.

This method is especially helpful for:
- 🔐 Security researchers conducting deep reconnaissance
- 🎯 Bug bounty hunters exploring hidden attack surfaces
- 🏢 Organizations monitoring their digital exposure



