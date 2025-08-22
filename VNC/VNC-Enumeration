# VNC Enumeration

**Virtual Network Computing (VNC)** is a remote desktop protocol widely used for graphical access to systems over a network. Enumerating VNC services is crucial for network reconnaissance, vulnerability discovery, and security assessments.

---

## Common VNC Ports

| Display | Typical Port | Other Possible Ports |
|---------|--------------|-----------------------|
| :0      | 5900         | 5093, 6000, 5800     |
| :1      | 5901         | 5094, 6001, 5801     |
| :2      | 5902         | 5095, 6002, 5802     |
| :3      | 5903         | 6003, 5803           |

- **Default port formula**: `TCP 5900 + N` (where **N** is the display number)  
- **Web interface ports**: Commonly `TCP 5800 + N`

---

## Step-by-Step VNC Enumeration Process

### 1. Identify Open VNC Ports
Scan the target for known VNC ports, both standard and non-standard:

```bash
nmap -p 5900-5903,5901-5905,6000-6004,5800-5803 --open -sV -Pn <target_ip>
```

- `-sV`: Identifies service and version  
- `-Pn`: Disables host discovery (ping)  
- `--open`: Displays only open ports  

---

### 2. Check for Authentication
Some VNC servers may lack strong authentication, presenting serious risks.

- Try connecting with a VNC client:

```bash
vncviewer <target_ip>:5900
```

- Attempt brute-force attacks (with engagement permissions):

```bash
ncrack -p 5900 <target_ip>
hydra -s 5900 -V -P passwords.txt vnc://<target_ip>
```

> If prompted for a password, the server enforces authentication.

---

### 3. Enumerate VNC Service Details
Gather details about the service—protocol version, authentication type, implementation.

```bash
nmap -p 5900 --script vnc-info <target_ip>
```

The `vnc-info` script shows protocol version, authentication mechanism, and sometimes the VNC server type.

---

### 4. Exploit Known Vulnerabilities
If you find an outdated VNC server, research its vulnerabilities and, if in scope, attempt exploitation.

- **Unauthenticated access**: Some servers lack or improperly implement authentication.  
- **Weak encryption**: Older VNC versions may have poor protection against eavesdropping.  

Use **Metasploit** for deeper analysis or automated exploitation:

```bash
msfconsole
use auxiliary/scanner/vnc/vnc_login
set RHOSTS <target_ip>
set RPORT 5900
run
```

---

### 5. Check for Web Access
VNC services can expose a **web interface** for browser-based access.

```bash
nmap -p 5800 <target_ip>
```

If found, browse:

```
http://<target_ip>:5800
```

---

### 6. Document Findings and Review
Thoroughly log all discoveries:

- Detected VNC server versions  
- Open ports and exposed interfaces  
- Authentication methods (none/weak/strong)  
- Encryption in use or lack thereof  
- Any known vulnerabilities  

This documentation is vital for security reporting, remediation, and improving defenses.

---

## Example Workflow

1. Scan ports with Nmap.  
2. Identify open ports related to VNC.  
3. Test for authentication prompts.  
4. Use Nmap scripts for protocol/service details.  
5. Probe with Metasploit if vulnerabilities are suspected.  
6. Scan port `5800` for web interface and test in browser.  
7. Log all findings for review and reporting.  

---

## Useful Tools

- **nmap**: Port scanning and service enumeration  
- **hydra / ncrack**: Password brute-forcing  
- **metasploit**: Automated exploitation and deeper analysis  
- **vncviewer / client apps**: Manual interaction  
- **netcat**: Banner grabbing  

---

## Security Tips & Remediation

- Always use **strong authentication** on VNC services.  
- Prefer **encrypted VNC implementations** (with TLS/SSL support).  
- Restrict access to VNC via firewalls and network controls.  
- Regularly **update VNC software** to patch vulnerabilities.  
- Disable unnecessary VNC services and close exposed ports.  

---

## Summary Table

| Step                  | Tool/Command                                         | Objective                        |
|-----------------------|------------------------------------------------------|----------------------------------|
| Find open VNC ports   | `nmap -p 5900-5903,5093-5095,5800 --open -sV`        | Locate VNC services              |
| Test authentication   | `vncviewer`, `ncrack`, `hydra`                       | Assess security                  |
| Enumerate details     | `nmap --script vnc-info`                             | Gather configuration info        |
| Exploit vulnerabilities | `metasploit`                                       | Attempt exploitation (with scope)|
| Check web interface   | `nmap -p 5800`                                       | Identify VNC web interface       |
| Document findings     | Manual documentation                                | Reporting and defense improvement|

---

## References to Techniques

- **Nmap**: `vnc-info` script for protocol & service details  
- **Hydra, Ncrack**: For brute-forcing authentication  
- **Metasploit modules**: For exploitation and automated checks  
- **Standard ports and display mapping**: For targeted scanning  
- **Documenting, reporting, and remediation steps**: As part of best practices  

---
