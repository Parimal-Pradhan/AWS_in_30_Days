### ✅ What is **Amazon CloudFront** in AWS?

**Amazon CloudFront** is a **Content Delivery Network (CDN)** service provided by AWS. It securely delivers content (like HTML, CSS, JS, images, videos, or entire websites) to users globally with **low latency and high transfer speeds**.

CloudFront **caches** content in **edge locations** worldwide so that users can access data faster from the nearest location, instead of always connecting to the origin server (like an S3 bucket or EC2 instance).

---

### ✅ Key Features:

- Global **Edge Locations** for faster content delivery
- Integrated with **AWS Shield** for DDoS protection
- Supports **HTTPS**, **signed URLs** for secure content delivery
- Works with **S3**, **EC2**, **Elastic Load Balancer**, or even **non-AWS servers**
- Logs requests and supports **Lambda@Edge** to run functions at edge locations

---

## ✅ Use Case: Deliver a Static Website with Amazon CloudFront

### 💡 Scenario:  
You have a **static website hosted on S3** and you want to serve it securely and faster to users around the world using CloudFront.

---

### ✅ Step-by-Step Guide:

#### **Step 1: Host Static Website on Amazon S3**

1. Go to **Amazon S3**
2. Create a bucket (e.g., `my-static-site-bucket`)
3. Upload your website files (HTML, CSS, images)
4. Enable **Static Website Hosting** under **Properties**
5. Set the index document (`index.html`)
6. Make your content public via **Bucket Policy**

#### **Step 2: Create a CloudFront Distribution**

1. Go to **CloudFront** service in AWS Console
2. Click **Create Distribution**
3. Under **Web**, choose:
   - **Origin domain**: your S3 bucket endpoint (e.g., `my-static-site-bucket.s3.amazonaws.com`)
   - **Viewer Protocol Policy**: Redirect HTTP to HTTPS
   - **Cache Policy**: Use default or custom cache behavior
   - **Alternate domain (CNAME)**: if using a custom domain (optional)
4. Choose **Default Root Object** as `index.html`
5. Click **Create Distribution**

#### **Step 3: Wait for CloudFront Distribution to Deploy**

- It takes a few minutes (~15–30 mins).
- Once deployed, note the **CloudFront URL** (e.g., `d1234abcd.cloudfront.net`)

#### **Step 4: Test Your Website**

- Open the CloudFront URL in your browser
- You should see your static website load faster from the edge location

---

### ✅ Optional: Add Custom Domain + HTTPS

If you want your website to be served via your domain (e.g., `www.example.com`):

1. **Register a domain** via Route 53 or another registrar
2. Add **A Record (Alias)** in Route 53 pointing to your CloudFront distribution
3. Use **AWS Certificate Manager (ACM)** to create a **free SSL certificate**
4. Attach the SSL certificate to your CloudFront distribution for **HTTPS**

---

### ✅ Summary of CloudFront Benefits in This Use Case

| Feature                  | Benefit                          |
|--------------------------|----------------------------------|
| Edge Caching             | Faster load times globally       |
| HTTPS support            | Secure content delivery          |
| Integration with S3      | Easy static site hosting         |
| Access Logs              | Detailed user access logs        |
| Custom Domain + SSL      | Professional and secure branding |

---


