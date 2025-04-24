
# Enumeration

## Definition

Enumeration is the process of obtaining network resources, usemames, passwords, services, and computer names. It extends the amount of information you have about a target network by providing detailed insights. Enumeration is typically the first attack on a target network and involves gathering information such as OS detalls, user accounts, services, domain information, and network infrastructure.

Enumeration is crucial for successful penetration testing, as it helps identify potential entry points and vulnerabilities.

It is typically the **first active step** in attacking a network and includes:
- OS details
- User accounts
- Services
- Domain info
- Network infrastructure

## Key Concepts of Enumeration

Enumeration involves making actual connections to the target or running commands on the target if you have physical access.

Enumeration can be performed using built-in operating system commands, utilities, or third-party security programs that can run remotely—sometimes without credentials.

Some information can come from error or informational messages sent back from the remote host.

Multipurpose tools such as Nmap and Nessus can enumerate services and provide general information, but specialized tools often provide deeper insights.

## Key Goals of Enumeration

- Identifying user, system, and admin accounts
- Establishing an active connection with the target on a local network
- Directly querying the target for information
- Looking for remote IPC$ shares and services that expose data
- Creating a null session to gain more access



## Information Gathered During Enumeration

### 1. User and Account Details
- Usernames  
- Groups  
- Default configurations  
- Default passwords  

### 2. Network and Host Details
- Domain names  
- Computer names  
- MAC addresses  
- Network resources  
- Running services  

### 3. System and Service Details
- Auditing services  
- Windows details  
- DNS, SMTP, SNMP information
- Application details  
- Banners from FTP Server, Web Server and Email Server
- Routing tables  

## Approaches to Enumeration

### 1. Local Host Enumeration
- Inside the target network
- Requires access (direct or indirect)

### 2. Remote Host Enumeration
- Performed from outside the network
- Uses scanning and network service interrogation

## Port and Service Enumeration

| Service    | Ports             |
|------------|-------------------|
| POP3/POP3S | 110/tcp, 995/tcp  |
| IMAP/IMAPS | 143/tcp, 993/tcp  |
| SNMP       | 161/udp           |
| MSSQL      | 1433/tcp          |
| RPC        | 111/tcp, 135/tcp  |
| SIP        | 5060/udp          |
| AJP        | 8009/tcp          |

## Example Commands for Enumeration

### 1. Enumerating Network Resources
#### Use net viow to list available network resources:
```bash
net view \\<target-ip>
```

### 2. Enumerating Users and Groups
#### Use net user to list local user accounts:
```bash
net user
```

#### Use met group to list groups:
```bash
net group
```

### 3. Finding Open Ports with Nmap
#### Use Nmap to scan for open ports and services:
```bash
nmap -sV -O <target-ip>
```

### 4. Enumerating SMB Shares
#### Use sabclient to list SMB shares.
```bash
smbclient -L //<target-ip> -U ""
```

### 5. Gathering SNMP Information
#### Use smapwalk to gather SNMP data
```bash
snmpwalk -v 2c -c public <target-ip>
```

### 6. Extracting Routing Tables
#### Use route print to display routing tables
```bash
route print
```

### 7. Checking DNS Information
#### Use nslookup to gather DNS details
```bash
nslookup <domain>
```

### 8. Banner Grabbing with Netcat
#### Use ne to grab banners from a target service:
```bash
nc <target-ip> 80
```

## Additional Tips
- Misconfigured services and open shares are vulnerable.
- Default passwords = weak point.
- SNMP and DNS can leak infrastructure info.
- Tools: **Nmap, Netcat, SMBclient, SNMPwalk**
- Combine findings with **privilege escalation**.

## Conclusion
Enumeration is essential for successful penetration testing. It builds a foundation for:
- Lateral movement
- Privilege escalation

Use a mix of automation and manual probing to maximize effectiveness.
