# Day-21 Auto Scaling Hands-on + Quiz

#### **Real-Time Use Case: E-commerce Website During Flash Sales**

**Scenario:**  
Imagine you're running an e-commerce website named **ShopMax**. During the year, traffic is moderate, but you experience massive traffic surges during special events such as **flash sales** or **holiday promotions**. For example, on the **Year-End Sale**, your website’s traffic increases by 10x in just a few minutes, as customers flood your platform to grab the best deals.

Without **Auto Scaling**, your website’s **EC2 instances** (virtual servers) might be overwhelmed by the increased load, causing slow response times, potential downtime, and a poor user experience. This results in frustrated customers and lost sales.

### **The Solution: Auto Scaling Implementation**

**Step 1: Create an Auto Scaling Group (ASG)**  
To handle the surge in traffic efficiently, we need to create an **Auto Scaling Group** (ASG) that defines the scaling rules for the website’s EC2 instances. This allows **ShopMax** to add more servers during traffic spikes and scale down when the demand drops.

**Step 2: Define Launch Configuration**  
We will create a **Launch Configuration** for the EC2 instances. This configuration will contain details about the AMI (Amazon Machine Image), instance type, security groups, key pairs, and other necessary configurations to ensure that every EC2 instance launched is identical and ready to handle the traffic.

**Step 3: Set Scaling Policies**  
The key part of Auto Scaling is defining **Scaling Policies** that will automatically trigger actions based on the website’s performance:

- **Scale Up Policy:**  
  - Trigger: If **CPU Utilization** > 70% for more than 5 minutes.
  - Action: Add **1 more EC2 instance**.
  
- **Scale Down Policy:**  
  - Trigger: If **CPU Utilization** < 30% for more than 10 minutes.
  - Action: Terminate **1 EC2 instance**.

**Step 4: Monitor with CloudWatch**  
Use **Amazon CloudWatch** to continuously monitor metrics like CPU utilization, memory usage, and disk activity. Based on these metrics, Auto Scaling will make decisions to add or remove EC2 instances.

---

### **Implementation Steps:**

1. **Launch Configuration:**
   - Go to **Amazon EC2 Console** → **Launch Configurations**.
   - Click on **Create launch configuration** and select an **AMI** (e.g., Amazon Linux 2).
   - Choose an instance type (e.g., **t2.medium**), configure the security group, and key pair.

2. **Auto Scaling Group (ASG) Setup:**
   - In the EC2 Dashboard, go to **Auto Scaling Groups** and click on **Create Auto Scaling Group**.
   - Select the previously created launch configuration.
   - Set the **Minimum Size** (e.g., 2 instances), **Maximum Size** (e.g., 10 instances), and **Desired Capacity** (e.g., 2 instances).
   
3. **Create Scaling Policies:**
   - For the **Scale Up** policy, set the CloudWatch metric for CPU utilization > 70% for 5 minutes.
   - For the **Scale Down** policy, set the CloudWatch metric for CPU utilization < 30% for 10 minutes.

4. **Testing the Setup:**
   - During the flash sale, when traffic spikes, Auto Scaling will detect the surge in CPU utilization and automatically add more EC2 instances.
   - When traffic decreases after the sale, Auto Scaling will remove the extra instances, saving costs.

---

### **The Outcome:**

By using **Auto Scaling**, **ShopMax** was able to manage the huge traffic spikes during the Year-End Sale without manual intervention. The website remained responsive, and the team didn’t have to worry about over-provisioning or under-provisioning resources. 

- **More instances were added** automatically when demand increased, ensuring that the website performed smoothly even under heavy load.
- **Excess capacity** was removed after the sale ended, ensuring **cost savings**.

### **Benefits for ShopMax:**
- **Cost Efficiency:** Only used the resources needed during peak demand times.
- **Improved User Experience:** The website remained fast, preventing potential sales losses.
- **Scalability:** The system scaled up or down based on real-time traffic, ensuring optimal performance.

---

### **Quiz:**

1. **What is Auto Scaling in AWS?**  
   a) A way to manually add servers  
   b) A service that automatically adjusts the number of servers based on traffic demand  
   c) A service for improving website security  
   d) A monitoring service for EC2 instances

2. **In the real-time use case, what triggered the Scale Up policy?**  
   a) CPU Utilization > 70%  
   b) Traffic increase by 10x  
   c) Website crash  
   d) Memory Usage > 80%

3. **What is the main advantage of using Auto Scaling in an e-commerce application during flash sales?**  
   a) Better marketing strategies  
   b) Automatic adjustments to server count based on real-time traffic  
   c) Increased security  
   d) Reduced server costs at all times

4. **Which AWS service does Auto Scaling use to monitor and take action based on server performance?**  
   a) AWS Lambda  
   b) Amazon CloudWatch  
   c) AWS SNS  
   d) AWS S3

5. **What is the Scale Down policy in Auto Scaling?**  
   a) Adds more EC2 instances when traffic increases  
   b) Terminates EC2 instances when CPU utilization is low for a prolonged period  
   c) Creates a backup of the EC2 instances  
   d) Optimizes EC2 instance performance

6. **Which of the following is NOT a key component of Auto Scaling?**  
   a) Launch Configuration  
   b) Auto Scaling Group  
   c) Scaling Policies  
   d) Amazon RDS

7. **True or False: Auto Scaling only works for EC2 instances running on Amazon Linux 2.**

8. **What happens if CPU Utilization exceeds 70% for a prolonged period with Auto Scaling?**  
   a) No action is taken  
   b) A new EC2 instance is added automatically  
   c) The website crashes  
   d) The server is terminated

9. **Which of the following best describes the Scale Down policy?**  
   a) It adds EC2 instances when the website traffic spikes  
   b) It removes EC2 instances when CPU utilization drops below a certain threshold  
   c) It restarts EC2 instances when they fail  
   d) It monitors traffic to generate reports

10. **How does Auto Scaling help reduce costs for ShopMax during off-peak periods?**  
    a) By adding more EC2 instances to improve performance  
    b) By automatically terminating unnecessary EC2 instances  
    c) By lowering the website prices  
    d) By reducing the number of website visitors

---

### **Answers:**
1. b) A service that automatically adjusts the number of servers based on traffic demand  
2. a) CPU Utilization > 70%  
3. b) Automatic adjustments to server count based on real-time traffic  
4. b) Amazon CloudWatch  
5. b) Terminates EC2 instances when CPU utilization is low for a prolonged period  
6. d) Amazon RDS  
7. False  
8. b) A new EC2 instance is added automatically  
9. b) It removes EC2 instances when CPU utilization drops below a certain threshold  
10. b) By automatically terminating unnecessary EC2 instances  

---

### **Conclusion:**

By implementing **Auto Scaling**, ShopMax ensured its website could handle massive traffic surges during flash sales while keeping costs under control. The solution provided **automatic scaling** based on real-time demand, preventing performance issues and optimizing resource usage. Now, your e-commerce website (or any application) can handle high-traffic events smoothly and efficiently, thanks to the power of **Auto Scaling**.
