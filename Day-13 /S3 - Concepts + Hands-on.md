# **Day-13: S3 – Concepts + Hands-on**

---

### ✅ **Real-Time Use Case: Website File Hosting for a Startup**

#### **Scenario:**
You’re working as a Cloud Engineer for a startup that is building a **static portfolio website** for its clients. Instead of using a traditional web server (like Apache or Nginx), the team wants a **scalable, cost-effective, and highly available solution** that can serve static HTML, CSS, and JavaScript files globally with minimal effort.

They ask you:  
**“Can we use AWS S3 to host this static website and make it publicly available?”**

You say:  
**“Yes, Amazon S3 is perfect for hosting static websites. Let me show you how!”**

---

### 🔍 **S3 Concepts:**

- **Amazon S3 (Simple Storage Service)**:  
  Object storage service that stores data as objects inside **buckets**.

- **Key Concepts:**
  - **Bucket**: Like a folder, top-level container.
  - **Object**: Individual files (HTML, images, videos, etc.).
  - **Key**: The unique name (path) for the object in the bucket.
  - **Storage Class**: Standard, Intelligent-Tiering, Glacier, etc.
  - **Versioning**: Keeps all versions of an object.
  - **Permissions**: Access Control Lists (ACLs), Bucket Policies, IAM.
  - **Static Website Hosting**: Turn a bucket into a static web host.
  - **Lifecycle Policy**: Rules to transition or delete objects automatically.

---

### 🛠️ **Hands-on: Host a Static Website Using Amazon S3**

---

### Step 1: **Create an S3 Bucket**

1. Go to the **S3 Console** → Click **Create bucket**
2. Bucket name: `my-client-portfolio-site`
3. Region: Select your preferred AWS region
4. **Uncheck** “Block all public access” (you will be warned – it's OK for a public website)
5. Enable or skip versioning (optional)
6. Leave default encryption for now
7. Click **Create bucket**

---

### Step 2: **Upload Website Files**

Let’s say your project folder has:
```
index.html
style.css
script.js
logo.png
```

1. Click on your bucket → Click **Upload**
2. Upload all static files (HTML, CSS, JS, images)
3. After uploading, note the **object URLs** (used for access)

---

### Step 3: **Make Files Public**

1. Select each file → Click **Actions** → **Make public**
2. Or use **Bucket Policy** to allow public access to all objects:

**Example Bucket Policy:**
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Sid": "PublicReadGetObject",
    "Effect": "Allow",
    "Principal": "*",
    "Action": "s3:GetObject",
    "Resource": "arn:aws:s3:::my-client-portfolio-site/*"
  }]
}
```
> Replace `my-client-portfolio-site` with your bucket name.

---

### Step 4: **Enable Static Website Hosting**

1. Go to **Properties** tab → Scroll to **Static website hosting**
2. Click **Edit** → Enable it
3. Index document: `index.html`
4. Error document: `error.html` (optional)
5. Save changes

You will get a **public S3 website endpoint**, something like:
```
http://my-client-portfolio-site.s3-website-us-east-1.amazonaws.com
```

That’s your **live website URL**! 🎉

---

### Step 5: **Optional: Custom Domain (Route 53) + HTTPS (CloudFront)**

If you want to host the website on a custom domain like `www.clientsite.com`:
- Register the domain or use an existing one.
- Point it to S3 using **Route 53 (DNS)**
- Add **CloudFront** to:
  - Serve globally with low latency (CDN)
  - Add **SSL/HTTPS**
  - Add caching for better performance

---

### ✅ **Solution Outcome:**

Your startup now has a **low-cost, scalable, and reliable static website** hosted on AWS S3 with global access. You can replicate this setup for multiple clients by creating new buckets per site.

---

### 🧠 Bonus Tips:

- Use **Lifecycle Rules** to move logs or backup images to Glacier.
- Enable **Versioning** to prevent accidental deletions.
- Use **S3 Transfer Acceleration** for faster uploads.
- Use **Presigned URLs** for secure one-time file downloads.

---

### 📌 Summary:

| Feature                | Value                                                      |
|------------------------|------------------------------------------------------------|
| Storage Type           | Object Storage                                             |
| Durability             | 99.999999999% (11 9’s)                                     |
| Static Hosting         | Yes (with public access enabled)                           |
| Real-time Use Case     | Hosting client portfolio websites                          |
| Security Options       | Bucket Policies, ACLs, IAM                                 |
| Cost                   | Pay only for what you store and transfer                   |

---

