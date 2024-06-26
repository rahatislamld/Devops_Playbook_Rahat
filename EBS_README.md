# Resizing EBS Volume on an EC2 Instance

This guide provides step-by-step instructions for resizing an EBS (Elastic Block Store) volume attached to an EC2 (Elastic Compute Cloud) instance.

```bash
# 1. Check Disk Information
sudo lsblk

# 2. Extend the Partition
sudo growpart /dev/xvda 1

# 3. Resize File System
sudo resize2fs /dev/xvda1

# 4. Check Disk Usage
df -h

# 5. Verify the Volume Size
lsblk /dev/xvda1

# 6. Additional Checks
df -h
```

Follow these steps carefully to resize the EBS volume on your EC2 instance. Ensure that you replace `/dev/xvda` and `/dev/xvda1` with the appropriate device identifiers for your system.

For any issues or additional assistance, refer to the AWS documentation or consult with your system administrator.
