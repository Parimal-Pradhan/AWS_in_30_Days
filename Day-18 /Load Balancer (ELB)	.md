# **Day-18: Load Balancer (ELB) **

---

![ChatGPT Image Apr 14, 2025, 12_43_08 PM](https://github.com/user-attachments/assets/d8c29de9-5c2c-4890-9acc-2bf7212d5298)




## 📖 **Short Story: Maya’s Cafe Chain**

Maya owns a chain of cafes across the city. During peak hours, people flood in. To manage the crowd efficiently:

- She hires a **receptionist** who directs each customer to the **least busy waiter**.  
- This **receptionist** is like a **Load Balancer (ELB)** in AWS!

In AWS, Maya’s website gets thousands of users. She wants to ensure:
- No single server is overloaded  
- Users are directed to the best available server  

So, she uses an **Elastic Load Balancer (ELB)**.

---

## 🔁 **What is a Load Balancer (ELB)?**

A **Load Balancer** distributes incoming traffic across multiple targets (like EC2 instances) in multiple Availability Zones.  
It improves:
- **Fault tolerance**
- **Scalability**
- **Performance**

---

## 🛠️ **How Load Balancing Works – Step-by-Step**

1. User sends request to your website (like Maya's Cafe)
2. Load Balancer receives it
3. It chooses the **least loaded, healthy instance**
4. Forwards request to that instance
5. If one instance fails, traffic is rerouted to healthy ones

---

## 🌈 **Types of Load Balancers in AWS**

| Type                     | Best For                            | Protocols Supported             |
|--------------------------|-------------------------------------|----------------------------------|
| **Application LB (ALB)** | HTTP/HTTPS apps (Layer 7)           | HTTP, HTTPS                     |
| **Network LB (NLB)**     | High-performance TCP traffic (L4)   | TCP, UDP, TLS                   |
| **Gateway LB (GLB)**     | Third-party firewalls, appliances   | IP-based traffic (Layer 3/4)    |
| **Classic LB (CLB)**     | Legacy applications                 | HTTP, HTTPS, TCP, SSL           |

---

## 🔎 **Details with Use Cases**

### 1️⃣ **Application Load Balancer (ALB)**
- Works at **Layer 7 (Application Layer)**
- Can route based on **URL paths**, **host headers**
- Example: `/login` goes to one group, `/images` to another

> **Maya’s website:** ALB routes `/orders` to order servers and `/admin` to admin panel.

---

### 2️⃣ **Network Load Balancer (NLB)**
- Works at **Layer 4 (Transport Layer)**
- Handles **millions of requests/sec** with ultra-low latency
- Supports static IPs and **Elastic IPs**

> **Maya’s chat service:** Needs real-time speed and low latency → uses NLB.

---

### 3️⃣ **Gateway Load Balancer (GLB)**
- Designed to **deploy, scale, and manage third-party appliances** (e.g., firewalls, intrusion detection)
- Works at **Layer 3/4**
- Routes traffic to **transparent appliances**

> **Maya’s security team:** Uses GLB to route traffic through a virtual firewall for inspection.

---

### 4️⃣ **Classic Load Balancer (CLB)**
- Old-generation LB supporting Layer 4 and 7 (basic features)
- Now replaced by ALB/NLB for most new workloads

> **Legacy apps:** Still using CLB for basic TCP or HTTP load balancing.

---

## ✅ **Benefits of Using ELB**

- High Availability across AZs
- Health Checks for targets
- Auto Scaling Support
- SSL Termination (especially ALB)

---

## 🔁 Maya’s Summary Table

| Load Balancer | Best For                 | Key Feature                  |
|---------------|--------------------------|------------------------------|
| ALB           | Web apps (Layer 7)       | URL-based routing            |
| NLB           | High-speed TCP/UDP apps  | Low latency, static IP       |
| GLB           | Security appliances      | Routes to firewalls etc.     |
| CLB           | Legacy apps              | Basic, old-school balancing  |

---

Let me know if you'd like:
- A diagram of how these ELBs connect to EC2  
- A hands-on setup for ALB or NLB  
- A quiz to test your knowledge!
