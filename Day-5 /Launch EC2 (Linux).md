# 📅 **Day-5: Launch EC2 (Linux)**  

**Real-time Use Case: Deploying a Personal Portfolio Website**

---

### 🎯 **Goal:**  
You're a developer and want to showcase your skills. You decide to host your **portfolio website** on an EC2 Linux server.

---

### 🧭 **Step-by-Step to Launch EC2 (Linux)**

---

### 🔹 **Step 1: Log into AWS Console**
- Go to: [https://console.aws.amazon.com/](https://console.aws.amazon.com/)
- Sign in using your AWS account credentials.

---

### 🔹 **Step 2: Choose EC2 Service**
- In the search bar, type **EC2** and click the **EC2** service.

---

### 🔹 **Step 3: Launch Instance**
- Click **"Launch Instance"**
- Name your instance (e.g., `PortfolioServer`)

---

### 🔹 **Step 4: Select Amazon Machine Image (AMI)**
- Choose: **Amazon Linux 2023** (Free tier eligible)

---

### 🔹 **Step 5: Choose Instance Type**
- Select: **t2.micro** (1 vCPU, 1 GB RAM — Free tier eligible)

---

### 🔹 **Step 6: Key Pair (For Login)**
- Create a new key pair (e.g., `PortfolioKey`)
- Download the `.pem` file and store it safely

> _You’ll use this file to connect to your server securely._

---

### 🔹 **Step 7: Configure Network Settings**
- Allow traffic via **SSH (port 22)** to connect to your server
- Add a rule for **HTTP (port 80)** to allow web traffic

---

### 🔹 **Step 8: Configure Storage**
- Default 8 GB EBS is enough (can change if needed)

---

### 🔹 **Step 9: Launch the Instance**
- Click **Launch Instance**
- Wait a few seconds… boom! ✅ You’ve got your Linux server running!

---

### 🔹 **Step 10: Connect to EC2 (via SSH)**
Open terminal (Mac/Linux) or use MobaXterm (Windows) and type:

```bash
chmod 400 PortfolioKey.pem
ssh -i "PortfolioKey.pem" ec2-user@<Public-IP-of-Instance>
```

> _Replace `<Public-IP-of-Instance>` with your EC2 instance's public IP._

---

### 🧪 **Real-Time Use Case in Action: Hosting Portfolio Website**

#### Once connected to EC2:
```bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```

#### Create your HTML file:
```bash
echo "<h1>Welcome to My Portfolio</h1>" | sudo tee /var/www/html/index.html
```

Now visit `http://<Your-Public-IP>` in your browser — and voilà! 🎉  
Your website is live from your EC2 instance.

---

### ✅ **Recap:**
- Launched a Linux server
- Connected via SSH
- Installed Apache
- Hosted a sample webpage

---


