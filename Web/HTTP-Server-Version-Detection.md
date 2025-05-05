
# HTTP Server Version Detection

## 1. Using Netcat (nc) for HTTP Server Version Detection

Netcat is a simple networking tool used to manually interact with services on specific ports. When connected to an HTTP server, it allows sending a raw HTTP GET request and observing the banner/version in the response.

**Connect to HTTP server on port 80:**

```
nc 192.168.1.44 80
```

After connecting, type:

```
GET / HTTP/1.1
Host: 192.168.1.44
```

Press Enter twice to send the request.

**Connect with verbose output to HTTP server on port 80:**

```
nc -v 192.168.1.44 80
```

Verbose output helps in identifying the connection status and any immediate banner information sent by the server.

**Connect with verbose output to another HTTP server on port 2222:**

```
nc -v 192.168.1.211 2222
```

This is useful when a web service is running on a non-standard port.

---

## 2. Using Telnet for HTTP Server Version Detection

Telnet works similarly to Netcat and can be used for banner grabbing.

**Connect to HTTP server using Telnet:**

```
telnet 192.168.1.44 80
```

Then send:

```
GET / HTTP/1.1
Host: 192.168.1.44
```

Press Enter twice to get a response. Look for `Server:` header in the response.

---

## 3. Using Nmap for HTTP Server Version Detection

Nmap is a powerful network scanner capable of detecting services, OS versions, open ports, and more.

**Scan all ports on the target host:**

```
nmap -v -p- 192.168.1.211
```

**Detailed scan with service & OS detection on specific ports:**

```
nmap -v -sT -sV -O -p 22,80,2222,3306,8009,8080,8081 192.168.1.211
```

* Useful when targeting known service ports.
* Helps identify web apps, database services, Tomcat, Jenkins, etc.

**Detailed scan on port 80:**

```
nmap -v -sT -sV -A -O -p 80 192.168.1.44
```

**Scan all ports on another target:**

```
nmap -v -sT -p- 172.16.0.129
```

**Detailed scan on port 80 of another target:**

```
nmap -v -sT -sV -A -O -p 80 172.16.0.129
```

Useful when trying to analyze just the HTTP server of a different target.

**Full service scan on all ports:**

```
nmap -v -sT -sV -A -p- 192.168.1.211
```

**Full scan with no ping, version detection, and saving results:**

```
nmap -v -Pn -sT -sV -sC -A -O -p 22,80,2222,3306,8009,8080,8081 -oA output 192.168.56.108
```

* `-Pn` treats the host as alive (even if ping is disabled).
* `-oA output` saves output in 3 formats: normal, XML, and grepable.

---

## Nmap Options Explanation

| Option | Description |
|--------|-------------|
| `-v`   | Verbose output |
| `-p-`  | Scan all 65535 TCP ports |
| `-sT`  | TCP Connect scan |
| `-sV`  | Service version detection |
| `-A`   | Aggressive scan (OS detection, version, scripts, traceroute) |
| `-O`   | OS detection |
| `-Pn`  | Skip host discovery; assume host is up |
| `-sC`  | Use default Nmap scripts |
| `-oA`  | Output to all formats: .nmap, .xml, and .gnmap |

---

When using Netcat or Telnet, always observe the `Server:` header in the HTTP response — this often reveals the web server software and version (e.g., Apache/2.4.41, nginx/1.18.0, etc.). In some cases, banners may be intentionally hidden or modified, so always confirm with multiple tools.
