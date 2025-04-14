### **Day-14: S3 – Hosting + Lifecycle + Quiz**

---

## ✅ **Use Case: Hosting a Static Website with Lifecycle Rules**

### 🎯 **Real-Time Scenario:**

You’re a Cloud Engineer for a digital portfolio agency. Clients upload their resume files, images, and static HTML/CSS/JS files to be hosted on the cloud.

**Requirements:**
- Host static sites for each client
- Make them public and accessible via a web URL
- Automatically **move old logs/images to cheaper storage** after 30 days
- Delete unused content after 180 days to save cost

---

## 🔍 **Concept 1: S3 Static Website Hosting**

### 🛠️ **Steps to Host a Static Website on S3:**

1. **Create an S3 Bucket**
   - Name: `client-portfolio-website`
   - Uncheck **Block all public access**

2. **Upload Website Files**
   - `index.html`, `style.css`, images, etc.

3. **Set Bucket Policy for Public Read Access**
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Principal": "*",
    "Action": "s3:GetObject",
    "Resource": "arn:aws:s3:::client-portfolio-website/*"
  }]
}
```

4. **Enable Static Website Hosting**
   - Index document: `index.html`
   - Get website URL:  
     `http://client-portfolio-website.s3-website-us-east-1.amazonaws.com`

---

## 🔍 **Concept 2: Lifecycle Configuration**

### 🎯 **Why?**
To **reduce costs** by automatically transitioning or deleting data you no longer need frequently.

---

### 🛠️ **Steps to Add Lifecycle Rules**

1. Go to your bucket → **Management** tab → **Lifecycle rules**
2. Click **Create lifecycle rule**
3. Rule Name: `image-and-logs-management`

4. Choose **Filter Prefix**:
   - `/images/` → transition to **Standard-IA** after 30 days
   - `/logs/` → transition to **Glacier** after 30 days, delete after 180 days

---

### 🧪 **Example Lifecycle Rule**

#### Rule 1: For `/images/` folder:
- Transition objects to **Standard-IA** after **30 days**

#### Rule 2: For `/logs/` folder:
- Transition to **Glacier** after **30 days**
- Delete after **180 days**

This ensures:
- **Lower cost**
- **Automation**
- **No manual cleanup needed**

---

## 🧠 Summary

| Feature           | Purpose                                               |
|------------------|--------------------------------------------------------|
| S3 Hosting        | Host static website (HTML/CSS/JS)                     |
| Public Access     | Via Bucket Policy or Object ACLs                      |
| Lifecycle Rule    | Transition to cheaper storage or delete automatically |
| Storage Classes   | Standard, Standard-IA, Glacier, Deep Archive          |
| Cost Saving       | Automatically optimize storage pricing                |

---

## 📝 **Hands-on Recap**

✅ Created an S3 bucket  
✅ Uploaded static files  
✅ Enabled static website hosting  
✅ Applied bucket policy  
✅ Set lifecycle rules for logs/images  

---

## 🧠 **Day-14 Quiz: Test Your Knowledge!**

> ✅ Choose the correct answer(s)

---

**1. What can you host on an S3 static website?**  
a) PHP applications  
b) HTML, CSS, JS files  
c) WordPress  
d) React/Vue Static build

> 🟩 Correct: **b, d**

---

**2. What does an S3 lifecycle rule do?**  
a) Automatically deletes IAM users  
b) Moves data to cheaper storage over time  
c) Prevents data from being accessed  
d) Increases data redundancy

> 🟩 Correct: **b**

---

**3. Which policy allows public access to your bucket?**  
a) IAM policy  
b) ACL  
c) Bucket Policy  
d) Firewall rules

> 🟩 Correct: **c**

---

**4. What is the purpose of enabling “Static Website Hosting”?**  
a) Host dynamic PHP apps  
b) Serve static content via a web URL  
c) Secure bucket with HTTPS  
d) Encrypt all files

> 🟩 Correct: **b**

---

**5. Which S3 storage class is best for infrequently accessed data?**  
a) Standard  
b) Intelligent Tiering  
c) Standard-IA  
d) Glacier

> 🟩 Correct: **c**

---

