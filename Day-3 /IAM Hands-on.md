# 🏢 **Story: How CloudNova Inc. Manages Security with IAM**  
**Title: “Right Access to the Right People — The IAM Way”**

---

### 📖 **The Story Begins...**

Meet **CloudNova Inc.**, a growing tech company building cloud-native applications. They recently migrated their infrastructure to **AWS** and hired a mix of developers, testers, admins, and interns.

But with a bigger team came a bigger **security challenge**.  
- Developers needed access to EC2 to deploy apps.  
- Testers needed access to S3 to validate logs.  
- DevOps engineers needed to manage auto scaling and monitoring.  
- Interns? Well, they just needed read-only access to documentation.  

**Chaos was about to happen** if everyone got the same access.

---

### 🧙‍♂️ **Enter IAM – The Security Wizard**

The IT manager, **Anaya**, introduced AWS IAM to bring order to the chaos. Here's how she structured it:

---

### 🛠️ **Step-by-Step Setup in CloudNova Inc.**

#### ✅ 1. **Create IAM Users**
Every employee got their own IAM user:
- Unique username & password  
- Optional Access Keys (for CLI/SDK)

This ensured **individual accountability** — no shared root access!

---

#### ✅ 2. **Create IAM Groups by Role**
To avoid managing each user separately, Anaya created **IAM Groups**:

| Group Name         | Policy Attached                      |
|--------------------|--------------------------------------|
| Developers         | `AmazonEC2FullAccess`                |
| Testers            | `AmazonS3ReadOnlyAccess`             |
| DevOps Engineers   | `AutoScalingFullAccess`, `CloudWatchFullAccess` |
| Interns            | `ReadOnlyAccess`                    |

Each user was added to a **group** — **access controlled, no over-permissioning!**

---

#### ✅ 3. **Create IAM Roles for Services**
- An EC2 instance needed to upload logs to S3.
- Instead of hardcoding keys, Anaya created an **IAM Role** with `AmazonS3FullAccess` and attached it to the instance.

Now EC2 can interact with S3 **securely and automatically**.

---

#### ✅ 4. **Enable MFA & Password Policy**
- Enforced **Multi-Factor Authentication (MFA)** for all users
- Set up a strong **password policy** (min length, rotation)

---

### ✅ 5. **Use Case: Intern Restriction**
One day, an intern mistakenly tried to launch an EC2 instance.  
Access denied!

Thanks to **IAM Policies**, the intern’s access was **restricted to documentation only** — no resource wastage, no security risk.

---

### 🧠 **IAM Benefits Realized by CloudNova Inc.**
- **Security**: Fine-grained control over who does what
- **Audit & Accountability**: Each user’s activity can be tracked via CloudTrail
- **Scalability**: Adding new employees is just a group assignment away
- **Automation Friendly**: Services like EC2 and Lambda access other resources securely using **IAM roles**

---

### 📦 **Moral of the Story:**
Just like departments in a real company have access based on job roles, **IAM helps replicate that in the cloud**.  
**Least privilege**, **group-based management**, and **automated access** — all in one system.

---

