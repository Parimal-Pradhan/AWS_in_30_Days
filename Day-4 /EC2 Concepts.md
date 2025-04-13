# 📅 **Day-4: EC2 Concepts**

---

### 🚀 **What is EC2?**
**EC2 (Elastic Compute Cloud)** is a virtual server in the cloud. Think of it like renting a computer from AWS that you can use anytime, anywhere — no physical setup needed!

---

### 🧱 **Key EC2 Concepts (Explained Simply):**

#### 🖥️ 1. **Instances**  
An **instance** is a virtual machine (VM). You choose the OS (like Linux or Windows), CPU, memory, etc.

> _"Imagine renting a room in a hotel — the size, view, and furniture are your instance type choices."_

---

#### 🧩 2. **Instance Types**  
Different types for different needs:
- `t2.micro` – Small, free tier eligible
- `m5.large` – General purpose
- `c5.xlarge` – For compute-heavy tasks

---

#### 🏗️ 3. **AMI (Amazon Machine Image)**  
Pre-configured templates for your EC2 instance (includes OS + software).  
> _"Like ordering a pizza with toppings — AMI gives you everything pre-prepared."_

---

#### 🗃️ 4. **EBS (Elastic Block Store)**  
A **hard disk** for your instance — stores files, logs, databases, etc.

---

#### 🌐 5. **Security Groups**  
Think of this as a **firewall** for your EC2. It controls traffic — what can enter or leave your server.

---

#### 📍 6. **Key Pair**  
Used to log in securely to your EC2 instance via SSH (for Linux) or RDP (for Windows).  
> _"It's like the master key to your virtual machine."_

---

#### 🛑 7. **Stopping vs Terminating**
- **Stop** = Pause your instance (you can restart)
- **Terminate** = Delete your instance forever

---

### 💡 **Use Case Example**  
Hosting a website, running a backend API, or setting up a virtual lab — EC2 is your go-to for flexible computing in the cloud.

---

