# Day-9: EBS - Concepts & Attach or Detach

#### **EBS Concepts**

**Amazon Elastic Block Store (EBS)** is a block-level storage service designed for use with Amazon EC2 instances. It provides persistent storage that can be attached to EC2 instances, allowing for high-performance data storage with scalable options.

Key concepts of EBS include:

- **Volumes**: EBS storage is available as volumes, which are essentially virtual hard drives that can be attached to an EC2 instance. Volumes are persistent, meaning data remains intact even after the EC2 instance is stopped or terminated.
  
- **Snapshots**: EBS volumes can be backed up using snapshots, which are incremental backups of the data. Snapshots can be used to restore volumes or create new volumes from an existing snapshot.

- **Types of Volumes**: 
  - **General Purpose SSD (gp3)**: Balances price and performance for most workloads.
  - **Provisioned IOPS SSD (io1, io2)**: High-performance SSD for mission-critical applications.
  - **Throughput Optimized HDD (st1)**: Cost-effective storage for frequently accessed workloads.
  - **Cold HDD (sc1)**: Low-cost storage for infrequent access workloads.

- **Volume Size**: EBS volumes can be sized between 1 GiB and 16 TiB, allowing flexibility depending on the storage needs of your application.

- **Performance**: EBS offers various performance metrics such as IOPS (Input/Output Operations Per Second) and throughput, which can be configured based on the volume type.

#### **Attaching and Detaching EBS Volumes**

You can attach and detach EBS volumes to EC2 instances using the AWS Management Console, AWS CLI, or AWS SDKs. Here’s how this works:

##### **Attaching EBS Volume to an EC2 Instance**

**Steps:**

1. **Create an EBS Volume**: First, create a new EBS volume from the AWS Management Console or CLI.
   - Select the volume type, size, and availability zone. The volume must be created in the same availability zone as the EC2 instance you intend to attach it to.

2. **Attach the Volume**:
   - Go to the EC2 Management Console.
   - In the left sidebar, under "Elastic Block Store," click **Volumes**.
   - Select the volume you created.
   - Click **Actions** > **Attach Volume**.
   - Select the EC2 instance you want to attach the volume to, and click **Attach**.

3. **Mount the Volume**:
   - Once attached, SSH into the EC2 instance.
   - Use the appropriate commands to format the volume and mount it to the file system.
   Example:
   ```bash
   sudo mkfs -t ext4 /dev/xvdf
   sudo mount /dev/xvdf /mnt/mydata
   ```

4. **Verify**:
   - Run `df -h` to verify the volume is mounted successfully.

##### **Detaching EBS Volume from EC2 Instance**

**Steps:**

1. **Un-mount the Volume** (if mounted):
   - SSH into the EC2 instance and unmount the volume.
   Example:
   ```bash
   sudo umount /mnt/mydata
   ```

2. **Detach the Volume**:
   - In the EC2 Management Console, go to the **Volumes** section.
   - Select the volume you wish to detach.
   - Click **Actions** > **Detach Volume**.
   - Confirm the detachment.

3. **Verify**:
   - Once detached, the volume will no longer be accessible from the EC2 instance.
   - You can re-attach it to another EC2 instance if needed.

#### **Example:**

Let’s assume you have an EC2 instance running a web server that requires additional storage for user data. You create an EBS volume of 50 GB, attach it to the instance, and mount it to the `/data` directory. Later, you detach the volume when scaling down the infrastructure and reattach it to a different instance for backup purposes.

1. Create a 50 GB EBS volume in the same availability zone as your EC2 instance.
2. Attach the volume to your EC2 instance using the AWS console.
3. Format and mount the volume on your instance.
   ```bash
   sudo mkfs -t ext4 /dev/xvdf
   sudo mount /dev/xvdf /data
   ```
4. Use the volume to store user data, and when no longer needed, unmount and detach the volume:
   ```bash
   sudo umount /data
   ```
5. Finally, detach the volume from the EC2 instance using the console.

This allows for a simple, scalable, and persistent storage solution on AWS.

---


