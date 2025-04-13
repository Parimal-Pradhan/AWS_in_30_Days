# Day-10: EBS Hands-on

#### **Real-time Story:**

Let’s consider a scenario where you are managing an e-commerce platform on AWS. The platform handles a large number of customer orders, and each order generates product data, shipping information, and transaction logs. Over time, the application has grown, and the amount of data has increased significantly. To handle this data growth, you need to scale the storage for your EC2 instances without affecting the application's performance. This is where **Amazon EBS (Elastic Block Store)** comes in.

In this story, we'll walk through the steps of managing EBS volumes for your e-commerce platform, from creating and attaching a volume to an EC2 instance to expanding and managing the volume to meet the needs of growing data.

#### **Scenario:**

Your application is running on an EC2 instance with a 30 GB root volume, which is starting to run out of space. You need more storage for customer transaction logs. You decide to use EBS to create an additional volume for storing these logs and then mount the volume to the EC2 instance.

#### **Steps:**

##### **Step 1: Create an EBS Volume**

1. **Login to AWS Management Console** and navigate to the **EC2 Dashboard**.
2. In the left panel, select **Volumes** under **Elastic Block Store**.
3. Click **Create Volume**.
4. Configure the volume:
   - **Volume Type**: Choose `General Purpose SSD (gp3)` for cost-effective and balanced performance.
   - **Size**: Set the volume size to `50 GB` (enough for growing log data).
   - **Availability Zone**: Choose the same Availability Zone (AZ) as your EC2 instance to avoid latency or attachment issues.
5. Click **Create Volume**. Your new EBS volume will be created in a few moments.

##### **Step 2: Attach the EBS Volume to the EC2 Instance**

1. Go to the **Volumes** section, and select the newly created volume.
2. Click **Actions** > **Attach Volume**.
3. Choose the EC2 instance you want to attach the volume to. For this example, let’s assume the instance is named `WebServer-01`.
4. Choose the device name (e.g., `/dev/xvdf`), and click **Attach**.

##### **Step 3: SSH into the EC2 Instance**

Now that the EBS volume is attached, you need to SSH into the EC2 instance to format and mount the volume.

1. Open your terminal and SSH into the EC2 instance:
   ```bash
   ssh -i your-key.pem ec2-user@<EC2-Instance-IP>
   ```
2. Check if the volume is detected by running:
   ```bash
   lsblk
   ```
   You should see the new volume listed as `/dev/xvdf`.

##### **Step 4: Format and Mount the EBS Volume**

1. **Format the new volume** to use the `ext4` filesystem:
   ```bash
   sudo mkfs -t ext4 /dev/xvdf
   ```

2. **Create a mount point** where the volume will be mounted:
   ```bash
   sudo mkdir /data
   ```

3. **Mount the volume** to the `/data` directory:
   ```bash
   sudo mount /dev/xvdf /data
   ```

4. **Verify** the mount by running:
   ```bash
   df -h
   ```
   You should see the `/dev/xvdf` volume mounted to `/data` with the appropriate size and available space.

##### **Step 5: Automate Mounting on Boot**

To ensure that the volume is automatically mounted each time the instance is restarted, you need to add it to the `/etc/fstab` file.

1. Open the `/etc/fstab` file in a text editor:
   ```bash
   sudo nano /etc/fstab
   ```

2. Add the following line to the file:
   ```bash
   /dev/xvdf  /data  ext4  defaults,nofail  0  0
   ```
   This ensures the volume is mounted automatically on boot.

3. Save and exit the editor (`CTRL+X`, `Y`, `Enter`).

##### **Step 6: Store Data in the EBS Volume**

Now that your volume is ready and mounted, you can use it to store transaction logs or any other application data. For example, you could write new log data from the e-commerce application to the `/data` directory.

1. Create a sample log file:
   ```bash
   echo "Transaction log entry: Order #1234" | sudo tee /data/transaction.log
   ```

2. Verify the log file was created:
   ```bash
   cat /data/transaction.log
   ```

##### **Step 7: Expand the EBS Volume**

As the data grows, you may find that you need more storage. Let’s expand the EBS volume from 50 GB to 100 GB.

1. In the **EC2 Dashboard**, go to **Volumes**.
2. Select the volume and click **Actions** > **Modify Volume**.
3. Increase the size to 100 GB and click **Modify**.
4. After modification, go back to the EC2 instance and extend the file system to use the newly added space:
   ```bash
   sudo growpart /dev/xvdf 1
   sudo resize2fs /dev/xvdf1
   ```

5. Verify the new size:
   ```bash
   df -h
   ```

Now, your EC2 instance has a larger EBS volume ready for more data storage.

#### **Step 8: Detach the EBS Volume**

If you need to detach the volume for backup or migration:

1. SSH into the EC2 instance and unmount the volume:
   ```bash
   sudo umount /data
   ```

2. In the **EC2 Management Console**, go to **Volumes**.
3. Select the volume and click **Actions** > **Detach Volume**.

Your volume is now detached and can be attached to another instance or snapshot for backup.

#### **Conclusion:**

This hands-on exercise shows how to create, attach, format, and mount an EBS volume to an EC2 instance, as well as how to expand and detach it. Amazon EBS provides a scalable and flexible storage solution for your EC2 instances, enabling you to handle increasing data storage needs efficiently. Whether you're dealing with logs, databases, or application files, EBS volumes offer persistence and high availability.

---

