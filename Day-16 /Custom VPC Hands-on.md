# **Day-16: Custom VPC Hands-on (Step-by-Step with Story)**

---

## 🧑‍💻 **Story: Priya Builds a Secure Web App**

Priya is a DevOps engineer working on a client project. The client wants a **secure web application** deployed on AWS with a **custom network** setup.

She decides to create a **Custom VPC** — instead of using the default one — so she has **full control over the network**.

---

## ✅ **Goal:**
Create a **Custom VPC** with:
- 1 Public Subnet (for Web Server)
- 1 Private Subnet (for Database)
- Internet Access only for Public Subnet
- Secure and organized architecture

---

## 🛠️ **Step-by-Step: Custom VPC Creation**

---

### 🔹 **Step 1: Create VPC**

1. Go to **VPC Dashboard** → **Your VPCs** → `Create VPC`
2. Name: `my-custom-vpc`  
3. IPv4 CIDR block: `10.0.0.0/16`  
4. Click **Create VPC**

---

### 🔹 **Step 2: Create Subnets**

📍 **Public Subnet:**
- Name: `public-subnet`
- VPC: `my-custom-vpc`
- CIDR: `10.0.1.0/24`
- Availability Zone: `ap-south-1a`

📍 **Private Subnet:**
- Name: `private-subnet`
- VPC: `my-custom-vpc`
- CIDR: `10.0.2.0/24`
- Availability Zone: `ap-south-1a`

---

### 🔹 **Step 3: Create & Attach Internet Gateway**

1. Go to **Internet Gateways** → `Create Internet Gateway`
   - Name: `my-igw`
2. Click **Attach to VPC** → select `my-custom-vpc`

---

### 🔹 **Step 4: Create Route Tables**

📘 **Public Route Table:**
- Name: `public-rt`
- Associate with: `public-subnet`
- Add Route:  
  - Destination: `0.0.0.0/0`  
  - Target: `Internet Gateway (my-igw)`

📕 **Private Route Table:** (Optional for now – no internet route)

---

### 🔹 **Step 5: Launch EC2 in Public Subnet**

1. Go to EC2 → `Launch Instance`
2. Select Amazon Linux 2
3. Network: `my-custom-vpc`
4. Subnet: `public-subnet`
5. Auto-assign Public IP: **Enable**
6. Security Group: Allow SSH (port 22) and HTTP (port 80)
7. Launch the instance

✅ Your web server is now **accessible from the internet**

---

### 🔒 **Step 6: Launch Database in Private Subnet**

1. Launch EC2 instance (simulate DB)
2. Subnet: `private-subnet`
3. Auto-assign Public IP: **Disable**
4. Security Group: Only allow access from **Web Server's private IP**

✅ The database is now **private and secure**

---

## 🧠 **Priya's Architecture**

| Component        | Details                      |
|------------------|------------------------------|
| VPC              | `my-custom-vpc (10.0.0.0/16)`|
| Public Subnet    | `10.0.1.0/24` – Web Server   |
| Private Subnet   | `10.0.2.0/24` – Database     |
| Internet Gateway | For public subnet only       |
| Route Tables     | Public subnet has IGW route  |
| Security Groups  | Limit access securely        |

---

## 🧪 **Outcome**

- Priya built a **fully functional** and **secure** VPC environment
- Web server is public-facing
- Database is protected in private subnet
- Traffic is controlled via routing and security groups

---

