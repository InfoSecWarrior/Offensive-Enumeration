# Subfinder 

## Introduction
Subfinder is a subdomain discovery tool that discovers valid subdomains for websites. It is designed as a passive framework, useful for bug bounties and safe for penetration testing. It does not directly touch the target, so it’s safe and silent during scanning.

### Advantages
- 🔒 **Passive & Safe**: It doesn’t directly interact with the target website.
- ⚡ **Fast & Lightweight**: Scans are quick and don’t use heavy resources.
- 🔌 **Multiple Data Sources**: Uses many APIs and online services.
- 🔧 **Easy to Configure**: Just set up your API keys and it’s ready to go.
- 🎯 **Focused on Subdomains**: Specifically built to find valid subdomains efficiently.

---

## Installation
Clone the repository and install Subfinder using Go:
```sh
GO111MODULE=on go get -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder
```
Install the latest version:
```sh
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
```
Move the binary to `/usr/local/bin/`:
```sh
cp -v /root/go/bin/subfinder /usr/local/bin/
```
Verify the installation:
```sh
subfinder -v
```
List all available sources:
```sh
subfinder -ls
```

For more details, visit:
- [Subfinder GitHub Repository](https://github.com/projectdiscovery/subfinder)
- [Recon Guide](https://github.com/projectdiscovery/recon-guide)
- [Post Installation Instructions](https://github.com/projectdiscovery/subfinder/wiki/Post-Installation-Instructions)

---

## Configuration
To set up API keys, create a provider configuration file:
```sh
vim $HOME/.config/subfinder/provider-config.yaml
```
Example `provider-config.yaml`:
```yaml
binaryedge:
  - 0bf8919b-aab9-4204-9574-d36639324597
  - ac244e2f-b635-4581-878a-33f4e79a2c13
censys:
  - ac244e2f-b635-4581-878a-33f4e79a2c13:dd510d6e-1b6e-4655-83f6-f347b363def9
certspotter: []
passivetotal:
  - sample-email@user.com:sample_password
securitytrails: []
shodan:
  - AAAAClP1bJJSRMEYJazgwhJKrggRwKA
github:
  - ghp_1kyJGU3jv1xmwk4SDXavrLDJ4d12pSJMzj4X
  - ghp_gkUuhkIYdQPj13ifH4KA3cXRn8J02lqir2d4
zoomeye:
  - zoomeye_username:zoomeye_password
```

---

## Usage Examples
### Basic Usage
Run a simple scan for subdomains:

> `-d` flag is used to specify the domain name to scan.

```sh
subfinder -d tesla.com
```
Verbose output:
```sh
subfinder -d tesla.com -v
```
Save output to a file:
```sh
subfinder -d tesla.com -o tesla_domain.txt
```
Count the number of discovered subdomains:
```sh
cat tesla_domain.txt | wc -l
```

### Using Specific Sources
Search using crt.sh:
```sh
subfinder -d tesla.com -s crtsh
```
Search using multiple sources (crt.sh and GitHub):
```sh
subfinder -d tesla.com -s crtsh,github
```

### Comprehensive Scan
Perform a full scan using all sources:
```sh
subfinder -d tesla.com -all
```
Perform a full scan without wildcard filtering:
```sh
subfinder -d tesla.com -all -rW
```
Use a custom resolver list:
```sh
subfinder -d tesla.com -all -rL /opt/massdns/lists/resolvers.txt
```
Silent mode with resolver list and output file:
```sh
subfinder -d tesla.com -all -nw -silent -rL /opt/massdns/lists/resolvers.txt -o tesla_domain2.txt
```

### Scanning Multiple Domains
Create a file with multiple domains:
```sh
vim target_domain.txt
```
Example `target_domain.txt`:
```
google.com
google.co.in
google.us
```
Scan all domains from the file and save output:
```sh
subfinder -dL target_domain.txt -o google_domain.txt
```
Count the discovered subdomains:
```sh
cat google_domain.txt | wc -l
```

### Silent Mode
Scan a single domain in silent mode:
```sh
subfinder -silent -d youtube.com
```
Full scan for Facebook with verbose output:
```sh
subfinder -all -d facebook.com -v -o subdomain-facebook.com.txt
```
Using echo for input:
```sh
echo youtube.com | subfinder -silent
```
Save output using echo:
```sh
echo youtube.com | subfinder -silent -o youtube_domain.txt
```
Full scan using a custom resolver list:
```sh
subfinder -d tesla.com -all -rL /opt/massdns/lists/resolvers.txt
```

---

## Conclusion 🚀
**Subfinder** is a powerful and easy-to-use tool for passive subdomain enumeration. It safely finds subdomains without touching the target directly. Use it along with other tools like Amass, Assetfinder, or Findomain for best results.
