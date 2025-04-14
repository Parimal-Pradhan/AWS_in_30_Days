# **Day-25: SNS - Notification System**


![ChatGPT Image Apr 14, 2025, 06_06_46 PM](https://github.com/user-attachments/assets/3cafc48f-fa1e-45cb-84f3-0bb846849270)

---

### ✅ **What is SNS in AWS?**

**Amazon SNS (Simple Notification Service)** is a **fully managed messaging service** that allows you to **send notifications/messages** to various **subscribers** via:

- Email
- SMS
- HTTP/HTTPS endpoint
- AWS Lambda
- SQS (Simple Queue Service)
- Mobile push notifications

SNS is **pub/sub (publish/subscribe)** model:
- **Publisher (Sender)** sends messages to an SNS **Topic**
- **Subscribers (Receivers)** receive messages via their preferred protocol

---

### ✅ **Key Features:**

- **Fan-out messaging** to multiple services or users
- **Decouples services** in microservice architecture
- **Real-time push-based delivery**
- **Durable & Scalable**

---

## ✅ **Use Case: Send Alert Emails when a File is Uploaded to S3**

---

### 🎯 **Goal:**
When a user uploads a file to an S3 bucket, send a notification email via **SNS**.

---

### ✅ **Step-by-Step Implementation**

---

### **Step 1: Create an SNS Topic**

1. Go to **Amazon SNS** in the AWS Console
2. Click **Create topic**
3. Select **Standard** type
4. Name the topic (e.g., `FileUploadAlerts`)
5. Click **Create topic**

---

### **Step 2: Subscribe to the Topic (Email)**

1. Inside your created topic, click **Create subscription**
2. Protocol: **Email**
3. Endpoint: Enter your **email address**
4. Click **Create subscription**
5. Check your inbox and **confirm the subscription** via the link

---

### **Step 3: Create an S3 Bucket**

1. Go to **S3**, click **Create bucket**
2. Name it (e.g., `my-upload-bucket-sns`)
3. Keep default settings or adjust as needed

---

### **Step 4: Create an Event Notification on S3**

1. Go to your S3 bucket
2. Go to the **Properties** tab
3. Scroll down to **Event notifications**
4. Click **Create event notification**
   - Name: `UploadEvent`
   - Event type: **PUT** (for upload)
   - Destination: **SNS Topic**
   - Choose the topic you created (`FileUploadAlerts`)
5. Save changes

---

### ✅ **Step 5: Test the Flow**

1. Upload a test file into your S3 bucket
2. Check your **email inbox**
3. You should receive an SNS email notification instantly with event details

---

### ✅ **Summary of Flow**

```
S3 File Upload ---> SNS Topic ---> Sends Email to Subscribers
```

---

### ✅ **Use Case Benefits**

| Feature           | Benefit                            |
|-------------------|-------------------------------------|
| Real-time alerts  | Immediate response to file uploads  |
| Multiple protocols| Email, SMS, Lambda, HTTP, SQS       |
| Easy integration  | With other AWS services             |
| Scalable          | Handles high message volume         |

---


