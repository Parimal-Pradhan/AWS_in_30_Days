# **Day-17: Security Groups vs NACLs – Concept with Story**

---

## 🔐 **What are Security Groups and NACLs?**

In AWS networking, **Security Groups** and **NACLs (Network Access Control Lists)** help **control traffic** to and from your resources. Think of them like **firewalls**, but with different scopes and rules.

---

## 📖 **Short Story: Amit’s Fort**

Amit builds a digital **fort (VPC)** for his new gaming app. He hires:

- 🛡️ **Security Guards (Security Groups)** to protect each **room (EC2 instance)**
- 🚧 **Gatekeepers (NACLs)** to guard the **main roads (subnets)** leading to the rooms

Let’s see how they work together 👇

---

### ✅ **Security Group (SG) – Instance Level Firewall**

- Works at the **instance level**
- **Stateful**: Response traffic is automatically allowed
- Only controls **allowed traffic**
- Can only **allow** rules (not deny)
- Applied to: **EC2, RDS, Load Balancer, etc.**

> **Example:**  
Amit allows HTTP (80) and SSH (22) only on the web server EC2.

```plaintext
Inbound Rules:
- Allow TCP 80 from 0.0.0.0/0
- Allow TCP 22 from Amit’s IP only
```

---

### ✅ **NACL (Network ACL) – Subnet Level Firewall**

- Works at the **subnet level**
- **Stateless**: Response traffic needs its own rule
- Can **allow and deny** traffic
- Evaluated in **rule order**
- Applied automatically to all resources in the subnet

> **Example:**  
Amit uses a NACL to **block all incoming access** to the database subnet **except** the web server subnet.

```plaintext
Inbound Rules:
- Allow TCP 3306 from 10.0.1.0/24 (Web Subnet)
- Deny everything else
```

---

## 🧠 **Key Differences: Security Groups vs NACLs**

| Feature                  | Security Group                        | NACL                                |
|--------------------------|----------------------------------------|--------------------------------------|
| **Applies To**           | EC2 / ENI level                        | Subnet level                         |
| **Stateful**             | ✅ Yes                                 | ❌ No (Stateless)                    |
| **Allow/Deny Rules**     | Only Allow                            | Allow & Deny                         |
| **Default Behavior**     | Deny all inbound, allow all outbound   | Allow all inbound & outbound         |
| **Rule Evaluation**      | All rules checked                     | Evaluated in number order (lowest first) |
| **Use Case**             | Secure specific instances              | Control subnet-wide traffic          |

---

## 🏰 **Amit’s Fort Analogy Summary**

| Concept         | In the Fort Example     |
|-----------------|-------------------------|
| **Security Group** | Guards outside each room (instance) checking ID |
| **NACL**            | Checkpoints at the gate of each road (subnet)   |
| **Stateful vs Stateless** | SG remembers who came in; NACL forgets every time |

---

## 🧪 Final Tip:
> Use **Security Groups** for **fine-grained access** to instances  
> Use **NACLs** for **broad access control** across **subnets**

---

