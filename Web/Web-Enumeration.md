
---

# 🌐 Web Server Enumeration

This guide lists common ports and services associated with web servers, application servers, and hosting control panels. Useful during reconnaissance and enumeration phases of penetration testing.

---

## 📌 Common Ports for Web Services

| **Service / Interface** | **Port(s)**             | **Protocol** |
|-------------------------|-------------------------|--------------|
| HTTP                    | 80, 8080, 8081, 8000     | TCP          |
| HTTPS                   | 443, 8443, 4443          | TCP          |

---

## 🖥️ Web Servers / Application Servers

| **Technology**                 | **Port(s)**                       | **Details**                                        |
|-------------------------------|-----------------------------------|---------------------------------------------------|
| Apache Tomcat                 | 8005, 8009, 8080, 8443            | Startup, Shutdown, AJP Connector, SSL             |
| GlassFish                     | 4848, 8080, 8181                  | Admin, HTTP, HTTPS                                |
| Jetty                         | 8080                              | Lightweight Java server                           |
| Jonas Admin Console           | 9000                              | Java EE server admin                              |
| IBM IHS Admin                 | 8008                              | IBM HTTP Server                                   |
| JBoss / WildFly               | 8080, 9990                        | Admin Console, HTTP                               |
| WebLogic Admin                | 7001                              | Oracle WebLogic Admin                             |
| WebSphere Admin (WAS)        | 9043, 9060                        | SSL & non-SSL Admin Console                       |
| WAS JVM HTTP/HTTPS           | 9080, 9443                        | Java-based HTTP/S                                 |
| Alfresco                     | 8080                              | ECM Web UI                                        |
| Apache Derby                 | 1527                              | Java DB, network server                           |
| Oracle HTTP Server           | 7777, 4443                        | Oracle HTTP + SSL                                 |
| Jenkins                      | 8080                              | DevOps automation tool                            |

---

## 🛠️ Hosting Control Panels & Services

| **Control Panel / Service**    | **Port(s)**                      | **Notes**                                         |
|-------------------------------|----------------------------------|--------------------------------------------------|
| cPanel                        | 2082 (HTTP), 2083 (SSL)          | Web hosting panel                                |
| WHM (Web Host Manager)        | 2086 (HTTP), 2087 (SSL)          | Admin interface                                   |
| Webmail                       | 2095 (HTTP), 2096 (SSL)          | Email client web access                          |
| Plesk Control Panel           | 8880 (HTTP), 8443 (SSL)          | Admin panel                                      |
| Virtuozzo                     | 4643                             | Container-based virtualization                   |
| DotNet Panel                  | 9001                             | Windows web hosting panel                        |
| DotNet Panel Login            | 80                               | Default HTTP login                               |
| Plesk Linux Webmail           | N/A                              | Dependent on config                              |
| Plesk Windows Webmail         | 9998                             | SmarterMail interface                            |
| Webdisk                       | 2077 (HTTP), 2078 (SSL)          | File management                                   |
| SFTP Shared Servers           | 2222                             | Alternative SSH port                             |
| Remote Desktop Protocol (Alt) | 4489                             | RDP on non-standard port                         |

---

🧠 **Note:** Many of these ports are used for administrative access. Always consider privilege escalation or configuration exposure during enumeration.

---

