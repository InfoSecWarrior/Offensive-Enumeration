### Subfinder

---

Subfinder is a subdomain discovery tool that discovers valid subdomains for websites. It is designed as a passive framework, useful for bug bounties and safe for penetration testing.

---

**It is best to use API Keys / Tokens for best and most sub domain outputs.**

---

### Installation

Clone the repository and install `subfinder` using `go`:

```bash
GO111MODULE=on go get -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder
```

OR

```bash
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
```

**Add Go Bin to PATH (If Needed)**

```bash
export PATH=$PATH:$(go env GOPATH)/bin
```

Install the latest version:

```bash
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
```

Move the binary to `/usr/local/bin/`:

```bash
cp-v/root/go/bin/subfinder/usr/local/bin/
```

Verify the installation:

```bash
subfinder -v
```

List all available sources:

```bash
subfinder -ls
```

---

For more details, visit:

Subfinder GitHub Repository → https://github.com/projectdiscovery/subfinder/

Post Installation Instructions

---

### Configuration

To set up API keys, create a provider configuration file:

```bash
vim $HOME/.config/subfinder/provider-config.yaml
```

Example `provider-config.yaml`:

```bash
binaryedge:
	- 0f8919b-aab9-4204-9574-d3b639324597
	- ac244e2f-b635-4581-878a-33f4e79a2c13
censys:
	- ac244e2f-b635-4581-878a-33f4e79a2c13:dd510d6e-1b6e-4555-83f6-f347b363def9
certspotter: []
passivetotal:
	- sample-email@user.com:sample_password
securitytrails: []
shodan:
	- AAAACLP1bJJSRMEYJazgwhJKrggRwKA
github:
	- ghp_lkyJGU3jv1xmwk4SDXavrLDJ4dl2pSJMzj4X
	- ghp_gkUuhkIYdQPj131FH4KA3cXRn8JD2lqir2d4
zoomeye:
	- zoomeye_username:zoomeye_password
```

---

### Usage Examples

Basic Usage

Run a simple scan for subdomains:

```bash
subfinder -d tesla.com
```

Verbose output:

```bash
subfinder -d tesla.com -v
```

Save output to a file:

```bash
subfinder -d tesla.com -o tesla_domain.txt
```

Count the number of discovered subdomains:

```bash
cat tesla domain.txt | wc -l
```

---

### Using Specific Sources

Search using `crt.sh`:

```bash
subfinder -d tesla.com -s crtsh
```

Search using multiple sources ( `crt.sh` and `GitHub`):

```bash
subfinder -d tesla.com -s crtsh, github
```

### Comprehensive Scan

Perform a full scan using all sources:

```bash
subfinder -d tesla.com -all
```

Perform a full scan without wildcard filtering:

```bash
subfinder -d tesla.com -all -nW
```

Use a custom resolver list:

```bash
subfinder -d tesla.com -all -rL /opt/massdns/lists/resolvers.txt
```

Silent mode with resolver list and output file:

```bash
subfinder -d tesla.com -all -nW -silent -rL /opt/massdns/lists/resolvers.txt -o tesla_domain2.txt
```

---

### Scanning Multiple Domains

Create a file with multiple domains:

```bash
vim target domain.txt
```

Example `target_domain.txt`:

```bash
google.com
google.co.in
google.us
```

Scan all domains from the file and save output:

```bash
subfinder -dL target_domain.txt -o google_domain.txt
```

Count the discovered subdomains:

```bash
cat google_domain.txt | wc -1
```

---

### Silent Mode

Scan a single domain in silent mode:

```bash
subfinder -silent -d youtube.com
```

Full scan for Facebook with verbose output:

```bash
subfinder -all -d facebook.com -v -o subdomain-facebook.com.txt
```

Using `echo` for Input:

```bash
echo youtube.com | subfinder -silent
```

Save output using `echo`: 

```bash
echo youtube.com | subfinder -silent -o youtube_domain.txt
```

Full scan using a custom resolver list:

```bash
subfinder -d tesla.com -all -rL /opt/massdns/lists/resolvers.txt
```

---

### Conclusion

Subfinder is a powerful tool for passive subdomain enumeration. By using different sources and configurations, it can help security researchers efficiently map out a target’s subdomains. Integrate it with other tools like `Amass` , `Assetfinder` , or `Findomain` for a more comprehensive approach.

---
