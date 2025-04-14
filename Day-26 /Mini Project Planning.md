# ✅ **Day-26: Mini Project Planning **

![ChatGPT Image Apr 14, 2025, 06_17_23 PM](https://github.com/user-attachments/assets/869209c2-3594-4136-9d8d-efb25466f144)




---

## 📌 **Extended Project Title:**  
**"Secure File Upload System with Real-Time Monitoring and Notification using EC2, S3, IAM, CloudWatch, and SNS"**

---

## ✅ **New Objective:**

In addition to secure file uploads from EC2 to S3:
- Log each S3 file upload using **CloudWatch**
- Send **real-time email notifications** using **SNS** when a file is uploaded

---

## ✅ **Updated Architecture:**

```
User → EC2 Instance → Uploads File to S3
               ↓
        S3 triggers Event Notification
               ↓
          CloudWatch Logs Trigger
               ↓
            SNS Notification
```

---

## ✅ **New AWS Services Added:**

| Service       | Purpose                                     |
|--------------|----------------------------------------------|
| **CloudWatch** | Monitors events like file uploads          |
| **SNS**       | Sends email alerts on file upload events   |

---

## ✅ **Step-by-Step Extended Implementation**

---

### ✅ **Step 1: Enable S3 Event Logging to CloudWatch**

1. Go to your **S3 bucket** → `secure-file-storage-bucket`
2. Click **Properties** → **Event Notifications** → Create event
3. Set:
   - **Event name**: `FileUploadLog`
   - **Event type**: `PUT` (All object create events)
   - **Destination**: Send to **CloudWatch Logs** or **Lambda**

⚠️ If direct CloudWatch is not visible, use **Lambda** to push events to CloudWatch.

---

### ✅ **Step 2: Create SNS Topic for Email Notification**

1. Go to **SNS > Create Topic**
   - Type: `Standard`
   - Name: `FileUploadAlert`
2. Click on the topic → **Create Subscription**
   - Protocol: `Email`
   - Endpoint: `your-email@example.com`
3. Confirm the subscription from your inbox

---

### ✅ **Step 3: Create Lambda Function to Forward Events to SNS**

1. Go to **Lambda > Create Function**
2. Name: `S3ToSNSNotifier`
3. Runtime: Python 3.12
4. Attach IAM Role with:
   - `AmazonSNSFullAccess`
   - `CloudWatchLogsFullAccess`
5. Use the following sample code:

```python
import json
import boto3

sns = boto3.client('sns')

def lambda_handler(event, context):
    print("Received event:", json.dumps(event, indent=2))
    
    file_name = event['Records'][0]['s3']['object']['key']
    bucket = event['Records'][0]['s3']['bucket']['name']
    
    message = f"📁 New File Uploaded!\nBucket: {bucket}\nFile: {file_name}"
    
    sns.publish(
        TopicArn='arn:aws:sns:region:account-id:FileUploadAlert',
        Subject='S3 File Upload Alert',
        Message=message
    )
    
    return {
        'statusCode': 200,
        'body': json.dumps('SNS Notification Sent!')
    }
```

---

### ✅ **Step 4: Add S3 Trigger to Lambda**

1. Go to the **Lambda function** → **Add trigger**
2. Select **S3**
3. Bucket: `secure-file-storage-bucket`
4. Event type: `PUT`
5. Save

---

### ✅ **Step 5: Test the Entire Flow**

1. Upload a file to your S3 bucket using EC2:
```bash
echo "Another test file" > file2.txt
aws s3 cp file2.txt s3://secure-file-storage-bucket/
```

2. Lambda gets triggered → Sends notification via SNS
3. You get an email like:

```
📁 New File Uploaded!
Bucket: secure-file-storage-bucket
File: file2.txt
```

---

## ✅ **Extended Project Output:**

| Action                  | Output                                   |
|--------------------------|-------------------------------------------|
| File upload via EC2      | ✅ Stored in S3                           |
| CloudWatch Logging       | ✅ File PUT logged                        |
| SNS Notification         | ✅ Email received                         |
| Lambda Execution         | ✅ Parses S3 event, pushes to SNS         |

---

## ✅ **Skills You’ve Practiced:**

- Event-Driven AWS Architecture
- Monitoring with CloudWatch
- Real-time Notifications with SNS
- IAM Role Permissions & Triggers
- End-to-End File Workflow Design

---

