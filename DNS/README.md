## DNS Enumeration

DNS enumeration is the process of finding all the DNS servers and their corresponding records for an organization. Like usernames, computer names, and IP addresses of target systems.

- [DNS Enumeration](#dns-enumeration)
  - [DNS Records](#dns-records)
  - [Tools](#tools)
    - [dnsenum](#dnsenum)
    - [nslookup](#nslookup)
    - [dig](#dig)
    - [host](#host)
  - [DNS Zone Transfer](#dns-zone-transfer)
    - [Find Name Server](#find-name-server)  
    - [Find Name Server IP Address](#find-name-server-ip-address)
    - [Transfer Target Zone](#transfer-target-zone)
  - [Subdomain Enumeration Tool](#subdomain-enumerate-tool)
    - [massdns](#massdns)
    - [subfinder](#subfinder)
     
### Impact

An attacker can use this information to obtain the internal network information if the DNS server is vulnerable to Zone Transfer Attack.

## DNS Records

| Record | Description |
|--------|-------------|
| A | The record that holds the IP address of a domain. |
| CNAME | Forwards one domain or subdomain to another domain, does NOT provide an IP address |
| MX | Directs mail to an email server |
| TXT | Lets an admin store text notes in the record. |
| NS | Stores the name server for a DNS entry |
| SOA | Stores admin information about a domain |
| SRV | Specifies a port for specific services. |
| PTR | Provides a domain name in reverse-lookups |

# Tools

## dnsenum
It is a multithread script to enumerate information on a domain and to discover non-contiguous IP blocks, Mainly it is ued to enumerate information about subdomins via custom dns server. 

	--noreverse           Skip the reverse lookup operations.
	-p, --pages <value>   The number of google search pages to process when scraping names,
    -s, --scrap <value>   The maximum number of subdomains that will be scraped from Google (default 15)
    --dnsserver   <server>

	# dnsenum --noreverse example.com

	# dnsenum --noreverse -o out.xml example.com

	# dnsenum --dnsserver <DNS_Server_Address> <Domain> -p <Pages> -s <Subdomain_Scrap>

	# dnsenum --dnsserver 192.168.1.100 example.tk -p 10 -s 50

## nslookup
nslookup  is  a  program  to query Internet domain name servers.  nslookup has two modes: interactive and non-interactive. Interactive mode allows the user to
query name servers for information about various hosts and domains or to print a list of hosts in a domain.  Non-interactive mode prints just the name and requested information for a host or domain.

	# nslookup <Server_IP/Domain> <DNS_Server_Address>

	# nslookup 192.168.1.100 192.168.1.1

	# nslookup --type=PTR 192.168.1.100 192.168.1.1

	# nslookup --type=A example.tk 192.168.1.1

	# nslookup -type=NS example.tk 192.168.1.1

	# nslookup -type=MX example.tk 192.168.1.1

## dig
It performs DNS lookups and displays the answers that are returned from  the  name  server(s)  that were  queried

	# dig <domain> @<DNS_Server_Address>

	# dig example.tk @192.168.1.100

	# dig A example.tk @192.168.1.100

	# dig AAAA example.tk @192.168.1.100

	# dig CNAME example.tk @192.168.1.100

	# dig NS example.tk @192.168.1.100

## host
It is normally used to convert names to IP addresses and vice versa.

	-t specifies the query type

	# host -t A <Domain> <DNS_Server_Address>

	# host -t A example.tk 192.168.1.32

	# host -t NS example.tk 192.168.1.32

	# host -t AAAA example.tk 192.168.1.32

	# host -t CNAME example.tk 192.168.1.32

	# host -t PTR 192.168.1.32 192.168.1.32

## DNS Zone Transfer

Zone Transfer can be applicable on Both Forward and Reverse Zone, if zone transfer is allow to all ip. It can be done in three steps.

### Find Name Server

	# nslookup -type=ns example.tk 192.168.1.100

	# dig NS example.tk @192.168.1.100

	# host -t ns example.tk 192.168.1.100

	# dig NS zonetransfer.me

### Find Name Server IP Address

	# nslookup -type=A server.example.tk 192.168.1.100

	# dig A server.example.tk @192.168.1.100

	# host -t A server.example.tk 192.168.1.100

	# dig A nsztm2.digi.ninja

### Transfer Target Zone

	# nslookup -type=axfr example.tk 192.168.1.100

	# dig AXFR example.tk @192.168.1.100

	# host -t AXFR example.tk 192.168.1.100

	# dig AXFR zonetransfer.me @nsztm2.digi.ninja

# Subdomain Enumerate Tool

## massdns
MassDNS is a simple high-performance DNS stub resolver targeting those who seek to resolve a massive amount of domain names in the order of millions or even billions. Without special configuration, MassDNS is capable of resolving over 350,000 names per second using publicly available resolvers.

	https://github.com/blechschmidt/massdns

	# git clone https://github.com/blechschmidt/massdns
	
	# cd massdns/

	# make

	# cp bin/massdns /usr/bin/

	# massdns -h
	-r  --resolvers        Text file containing DNS resolvers.
	-t  --type             Record type to be resolved. (Default: A)
	-w  --outfile          Write to the specified output file instead of standard output.
	-o  --output           Flags for output formatting.

	# massdns -r lists/resolvers.txt -t AAAA /dev/shm/domain.txt

	# massdns -r lists/resolvers.txt -t NS /dev/shm/domain.txt > /dev/shm/NS.txt

	# massdns -r lists/resolvers.txt -t SOA /dev/shm/domain.txt -w /dev/shm/SOA.txt

	# massdns -r lists/resolvers.txt -t PTR /dev/shm/domain.txt -w /dev/shm/PTR.txt

	# massdns -r lists/resolvers.txt -t CNAME /dev/shm/domain.txt -w /dev/shm/CNAME.txt
	
	# massdns -r lists/resolvers.txt /dev/shm/domain.txt -t A -o S -w /dev/shm/results.txt

## subfinder
Subfinder is a subdomain discovery tool that discovers valid subdomains for websites by using passive online sources. It has a simple modular architecture and is optimized for speed. subfinder is built for doing one thing only - passive subdomain enumeration, and it does that very well.

	https://github.com/projectdiscovery/subfinder

	# GO111MODULE=on go get -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder

	# cp /root/go/bin/subfinder /usr/bin/subfinder

	# subfinder --help
	-d string        Domain to find subdomains for
	-dL string       File containing list of domains to enumerate
	-nW        Remove Wildcard & Dead Subdomains from output
	-rL string        Text file containing list of resolvers to use
	-silent        Show only subdomains in output
	-o string        File to write output to (optional)
	
	# subfinder -d example.com

	# subfinder -d example.com -v
	
	# subfinder -d example.com -all -v

	# subfinder -d example.com -recursive

	# subfinder -dL /dev/shm/domain.txt

	# subfinder -d example.com -nW

	# subfinder -d example.com -nW -rL /opt/Tools/massdns/lists/resolvers.txt

	# subfinder -d example.com -silent

	# subfinder -d example.com -nW -silent -o /dev/shm/result.txt





---

# Why DNS Enumeration is Important

- **Information Gathering** – It allows attackers and security testers to gather data about the target's network.  
- **Identifying Attack Surfaces** – Misconfigured DNS records, exposed subdomains, and outdated infrastructure can be potential entry points.  
- **Social Engineering** – Collected data can be used to craft more targeted phishing or social engineering attacks.  
- **Pentesting & Red Teaming** – Understanding the DNS infrastructure helps in simulating real-world attack scenarios.

---

# Types of DNS Enumeration

1. **Direct Domain Enumeration**  
   - Identifying subdomains and associated records through direct queries.

2. **Reverse DNS Lookup**  
   - Resolving an IP address back to its domain name.

3. **Zone Transfer (AXFR) Enumeration**  
   - Attempting to transfer the entire DNS zone file from a misconfigured DNS server.

4. **Brute-Force Subdomain Discovery**  
   - Trying common subdomain names to identify valid ones.

5. **PTR Record Lookup**  
   - Resolving IP addresses to domain names.

6. **Certificate Transparency Logs**  
   - Checking for subdomains and domains listed in publicly available SSL/TLS certificates.

7. **WHOIS Lookup**  
   - Gathering domain registration and ownership details.

---

# Key DNS Enumeration Tools

| Tool        | Purpose                               | Example Command                                             |
|-------------|---------------------------------------|-------------------------------------------------------------|
| nslookup    | Query DNS records                     | `nslookup armourinfosec.com`                                 |
| dig         | Detailed DNS lookup                   | `dig armourinfosec.com ANY`                                  |
| host        | Simple DNS lookup                     | `host armourinfosec.com`                                     |
| nmap        | DNS and port scanning                 | `nmap -p 53 --script=dns-brute armourinfosec.com`            |
| dnsrecon    | Automated DNS enumeration             | `dnsrecon -d armourinfosec.com`                              |
| dnsenum     | Brute force DNS enumeration           | `dnsenum armourinfosec.com`                                  |
| sublist3r   | Subdomain enumeration                 | `sublist3r -d armourinfosec.com`                             |
| crt.sh      | Certificate search for subdomains     | [crt.sh link](https://crt.sh/?q=armourinfosec.com) |

---



---

# Example DNS Enumeration Commands

1. **Find all DNS records using `dig`:**

```bash
dig armourinfosec.com ANY
```

2. **Reverse lookup for PTR records using `dig`:**

```bash
dig -x 192.168.1.43
```

3. **Find subdomains using `dnsrecon`:**

```bash
dnsrecon -d armourinfosec.com -t std
```

4. **Find subdomains using `sublist3r`:**

```bash
sublist3r -d armourinfosec.com
```

5. **Perform zone transfer using `dig`:**

```bash
dig axfr @ns1.armourinfosec.com armourinfosec.com
```

6. **Identify DNS servers using `nslookup`:**

```bash
nslookup -type=NS armourinfosec.com
```

7. **Enumerate DNS records with `nmap`:**

```bash
nmap -p 53 --script=dns-brute armourinfosec.com
```

---


