# Day-12: EFS Hands-on (Mount to EC2)

#### **Real-time Story:**

Imagine you are working for a **media processing company** that handles large volumes of video files. Your company has built a **video editing application** on AWS, where video files are uploaded by users and processed by multiple EC2 instances in parallel. Each EC2 instance in the Auto Scaling group needs access to the same video files to process them efficiently.

To make sure all EC2 instances can access the same files, you choose to use **Amazon EFS (Elastic File System)** because it offers a scalable, shared file system that can be mounted across multiple EC2 instances. This allows your EC2 instances to work on the same set of video files concurrently without needing to copy data between instances.

In this hands-on session, we will walk through the steps to **create an EFS file system**, **mount it to an EC2 instance**, and demonstrate how to use EFS for storing and sharing video files between EC2 instances.

#### **Steps:**

##### **Step 1: Create an EFS File System**

1. **Login to the AWS Management Console** and navigate to the **EFS Dashboard**.
2. Click **Create file system**.
3. Choose the **VPC** where your EC2 instances are running.
4. **Mount Targets**: EFS needs mount targets in each Availability Zone (AZ) where your EC2 instances reside. Select the AZs and enable mount targets.
5. **Performance Mode**: Choose **General Purpose** (this is the default and sufficient for most use cases).
6. **Throughput Mode**: Choose **Bursting** (default) for moderate workloads.
7. Choose the **Encryption** settings (you can enable encryption at rest for security).
8. Click **Create File System**.

After a few moments, your EFS file system will be created, and you will see it listed in the EFS dashboard.

##### **Step 2: Configure Security Groups**

To allow your EC2 instances to access the EFS file system, you need to configure the security group for both your EC2 instances and EFS.

1. In the **EFS Dashboard**, select the file system and go to the **Network** tab.
2. Click on the **Security Group** link next to the mount target.
3. In the **EC2 Security Group** settings, ensure that inbound traffic on **port 2049 (NFS)** is allowed.
4. Also, update the security group of your **EC2 instances** to allow traffic on port 2049 from the EFS security group.

##### **Step 3: Launch EC2 Instance**

1. Go to the **EC2 Dashboard** and launch a new EC2 instance in the same **VPC** and **Availability Zone** as your EFS file system.
2. Choose an **Amazon Linux 2** or **Ubuntu** instance (for this example, we'll use Amazon Linux 2).
3. Make sure that the EC2 instance is attached to the same security group that allows inbound traffic on port 2049 (NFS).
4. Launch the instance and note the **Public IP** or **Private IP**.

##### **Step 4: Install NFS Client on EC2 Instance**

Once your EC2 instance is up and running, SSH into it using your **SSH key**.

1. SSH into your EC2 instance:
   ```bash
   ssh -i your-key.pem ec2-user@<EC2-Instance-IP>
   ```

2. Install the NFS client on the EC2 instance (for Amazon Linux 2):
   ```bash
   sudo yum install -y nfs-utils
   ```

3. Verify that the NFS client was installed successfully:
   ```bash
   nfsstat -c
   ```

##### **Step 5: Mount EFS File System**

Now, you need to mount the EFS file system on the EC2 instance.

1. **Create a directory** where the EFS file system will be mounted:
   ```bash
   sudo mkdir /mnt/efs
   ```

2. **Mount the EFS** file system using the DNS name of the EFS file system (you can find this in the EFS dashboard):
   ```bash
   sudo mount -t nfs4 <EFS-DNS-NAME>:/ /mnt/efs
   ```

   For example:
   ```bash
   sudo mount -t nfs4 fs-12345678.efs.us-west-2.amazonaws.com:/ /mnt/efs
   ```

3. **Verify the mount**:
   ```bash
   df -h
   ```

   You should see your EFS file system mounted at `/mnt/efs`.

##### **Step 6: Test File Access**

Now that your EFS file system is mounted, you can use it like a regular file system.

1. **Create a test directory** in the EFS mount point:
   ```bash
   sudo mkdir /mnt/efs/videos
   ```

2. **Create a test video file** (simulating an uploaded video):
   ```bash
   echo "Video file content" | sudo tee /mnt/efs/videos/sample_video.txt
   ```

3. **List the files** in the directory:
   ```bash
   ls /mnt/efs/videos
   ```

   You should see the `sample_video.txt` file you just created.

##### **Step 7: Mount EFS on Another EC2 Instance**

To demonstrate the shared access feature of EFS, you can mount the same EFS file system on a **second EC2 instance**.

1. Launch a **second EC2 instance** in the same **VPC** and **Availability Zone** as the first instance and attach the same security group.
2. SSH into the second EC2 instance:
   ```bash
   ssh -i your-key.pem ec2-user@<Second-EC2-Instance-IP>
   ```

3. Install the **NFS client**:
   ```bash
   sudo yum install -y nfs-utils
   ```

4. Create a directory to mount the EFS:
   ```bash
   sudo mkdir /mnt/efs
   ```

5. Mount the EFS file system on this second instance:
   ```bash
   sudo mount -t nfs4 <EFS-DNS-NAME>:/ /mnt/efs
   ```

6. Verify the mount and check for the test video file:
   ```bash
   ls /mnt/efs/videos
   ```

   You should see the same `sample_video.txt` file that was created on the first EC2 instance.

##### **Step 8: Automate Mounting on Boot**

To ensure the EFS file system is mounted automatically on both EC2 instances every time they reboot, you need to add the EFS mount to the `/etc/fstab` file.

1. Open the `/etc/fstab` file on each EC2 instance:
   ```bash
   sudo nano /etc/fstab
   ```

2. Add the following line to the file to mount the EFS on boot:
   ```bash
   <EFS-DNS-NAME>:/ /mnt/efs nfs4 defaults,_netdev 0 0
   ```

3. Save and close the file (`CTRL+X`, `Y`, `Enter`).

Now, both EC2 instances will automatically mount the EFS file system when they reboot.

#### **Conclusion:**

In this hands-on exercise, you learned how to create an EFS file system, mount it to an EC2 instance, and use it for shared storage between multiple EC2 instances. EFS is ideal for applications that require shared access to files from multiple instances, such as media processing, content management, and web hosting. With its scalability and high availability, EFS helps ensure that your applications can handle increasing data and traffic demands efficiently.

---

