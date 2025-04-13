# 📅 **Day-6: EC2 (Linux + Web Server Setup + MySQL Setup)**  

🎯 **Real-time Use Case:** You're building a web app with a backend database. You need a Linux server that can serve web pages **and** store user data using **MySQL**.

---

### 🧭 **Step-by-Step Guide**

---

### 🔹 **Step 1: Launch EC2 Linux Instance**  
(If you already did this in Day-5, skip to Step 2)

- OS: Amazon Linux 2023 (or Ubuntu 22.04)
- Instance type: t2.micro (Free tier)
- Allow ports:
  - **22** (SSH)
  - **80** (HTTP)
  - **3306** (Optional, for MySQL if you want remote access)

---

### 🔹 **Step 2: Connect to EC2 Instance**
Use SSH or MobaXterm (Windows):
```bash
ssh -i "your-key.pem" ec2-user@<your-public-ip>
```

---

### 🔹 **Step 3: Update Your Server**
```bash
sudo yum update -y   # For Amazon Linux
```

---

## 🔧 **Part 1: Web Server Setup (Apache)**

---

### 🔹 **Step 4: Install Apache**
```bash
sudo yum install httpd -y
```

### 🔹 **Step 5: Start and Enable Apache**
```bash
sudo systemctl start httpd
sudo systemctl enable httpd
```

### 🔹 **Step 6: Allow HTTP Access**
Make sure **port 80** is open in EC2 security group.

Now test:  
Open `http://<your-public-ip>` in browser → You should see Apache’s test page.

---

## 🗃️ **Part 2: Install PHP (Optional but Useful for Web + DB)**

```bash
sudo amazon-linux-extras enable php8.2
sudo yum clean metadata
sudo yum install php php-mysqlnd -y
```

---

## 🗄️ **Part 3: MySQL Setup**

---

### 🔹 **Step 7: Install MariaDB (MySQL compatible)**
```bash
sudo yum install mariadb-server -y
```

### 🔹 **Step 8: Start & Enable MySQL**
```bash
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

---

### 🔹 **Step 9: Secure MySQL Installation**
```bash
sudo mysql_secure_installation
```
- Set root password
- Remove anonymous users
- Disallow remote root login (Yes)
- Remove test DB
- Reload privileges

---

### 🔹 **Step 10: Login to MySQL and Create a DB**
```bash
sudo mysql -u root -p
```
Then inside MySQL shell:
```sql
CREATE DATABASE myappdb;
CREATE USER 'webadmin'@'localhost' IDENTIFIED BY 'StrongPass123!';
GRANT ALL PRIVILEGES ON myappdb.* TO 'webadmin'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

---

## 🌐 **Part 4: Test PHP & MySQL Connection**

---

### 🔹 **Step 11: Create Test PHP Page**
```bash
sudo nano /var/www/html/info.php
```

Paste:
```php
<?php
phpinfo();
?>
```

Visit:  
`http://<your-public-ip>/info.php` → You’ll see the PHP info page ✅

---

### 🔹 **Step 12: Sample MySQL Connection Test**
Create:
```bash
sudo nano /var/www/html/dbtest.php
```

Paste:
```php
<?php
$conn = new mysqli('localhost', 'webadmin', 'StrongPass123!', 'myappdb');
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "MySQL connected successfully!";
?>
```

Visit:  
`http://<your-public-ip>/dbtest.php`  
→ You should see: “MySQL connected successfully!”

---

## ✅ Summary:
You’ve now set up:
- ✅ Linux EC2 Server  
- ✅ Apache Web Server  
- ✅ PHP for dynamic web pages  
- ✅ MySQL for backend data storage  
- ✅ Verified the full stack connection!

---


