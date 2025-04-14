# ✅ **Day-26: Mini Project Planning **

---

## 📌 **Project Title:**  
**Secure File Upload & Notification System using EC2, S3, IAM, CloudWatch, and SNS**

---

## 🎯 **Project Objective:**  
To design a secure and automated AWS-based system where:
- Files are uploaded securely from an EC2 instance to an S3 bucket.
- IAM roles manage permissions securely.
- CloudWatch and Lambda monitor the upload activity.
- SNS sends email notifications on each successful file upload.

---

## 🧱 **AWS Services Used:**

| Service       | Purpose                                                     |
|---------------|-------------------------------------------------------------|
| IAM           | Securely manage permissions between EC2 and S3              |
| EC2           | Virtual server to upload files                              |
| S3            | Cloud storage to hold uploaded files                        |
| CloudWatch    | Monitor and log S3 events                                   |
| SNS           | Send notifications on file uploads                          |
| Lambda        | Act as a middle layer between S3 and SNS (event handler)    |

---

## 🗂️ **Project Phases:**

### ✅ **Phase 1: Infrastructure Setup**

1. **Create S3 Bucket**  
   - Name: `secure-file-storage-bucket`  
   - Enable versioning & logging if needed.

2. **Create IAM Role for EC2**  
   - Attach policy: Custom S3 PUT-only policy (least privilege)

3. **Launch EC2 Instance**  
   - Attach IAM role  
   - Install and configure AWS CLI  
   - Use the EC2 to upload test files to S3  

---

### ✅ **Phase 2: Monitoring & Notification Setup**

4. **Create SNS Topic**  
   - Name: `FileUploadAlert`  
   - Subscribe your email  

5. **Create Lambda Function**  
   - Language: Python  
   - Purpose: Send notification to SNS on S3 PUT event  
   - Permissions: `AmazonSNSFullAccess` & `CloudWatchLogsFullAccess`

6. **Add Trigger to Lambda**  
   - Event Source: S3 bucket  
   - Event Type: PUT object (file upload)

---

### ✅ **Phase 3: Integration & Testing**

7. **Upload File via EC2 CLI**  
   - Command:  
     ```bash
     aws s3 cp sample.txt s3://secure-file-storage-bucket/
     ```

8. **Monitor Results**  
   - File should appear in S3  
   - Lambda gets triggered  
   - SNS sends email with upload details  
   - CloudWatch logs show Lambda invocation details  

---

## 📬 **Sample Notification Email:**
```
📁 New File Uploaded!
Bucket: secure-file-storage-bucket
File: sample.txt
```

---

## 🧠 **Expected Learning Outcomes:**

- Secure file handling using IAM and EC2
- Real-time event processing using Lambda
- System monitoring using CloudWatch
- Alerting system with SNS
- Event-driven architecture in AWS

---

## 🔐 **Security Considerations:**

- Use minimal IAM permissions (principle of least privilege)  
- Encrypt S3 bucket (SSE-S3 or SSE-KMS)  
- Use VPC + Security Groups to limit EC2 access  
- Rotate IAM keys if manually configured  

---

## 📈 **Possible Future Enhancements:**

- Add CloudTrail for detailed audit logs  
- Use a web app instead of EC2 for file upload  
- Notify via SMS or Slack using SNS  
- Auto-delete old files using S3 Lifecycle policies  
- Create a dashboard using CloudWatch Metrics  

---

