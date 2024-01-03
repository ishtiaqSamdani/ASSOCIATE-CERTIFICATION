
## Amazon Elastic Block Store (EBS)

Amazon Elastic Block Store (EBS) provides raw block-level storage that can be attached to Amazon EC2 instances. These volumes are highly available and reliable storage volumes that can be attached to any running instance that is in the same Availability Zone.

### EBS Volume Types

There are five types of EBS volumes:

1. **General Purpose SSD (gp2 and gp3):** Suitable for a broad range of workloads, including small to medium-sized databases, development and test environments, and boot volumes. gp3 offers the ability to independently scale IOPS and throughput.

2. **Provisioned IOPS SSD (io1 and io2):** Designed for I/O intensive applications such as large relational or NoSQL databases. io2 offers 100x more durability and 10x more IOPS-to-storage ratio than io1.

3. **Throughput Optimized HDD (st1):** Designed for frequently accessed, throughput-intensive workloads such as big data, data warehouses, and log processing.

4. **Cold HDD (sc1):** Designed for less frequently accessed workloads, more suitable for sequential reads than random reads.

5. **Magnetic (standard):** Previous generation volumes suited for workloads where data is accessed infrequently, and applications where the lowest storage cost is important.

Each volume type comes with its own performance characteristics and price, so you can choose the type that best fits your needs.

## EBS Volume Types Details

### General Purpose SSD (gp2)

- **Size range:** 1 GB to 16 TB
- **Burst capability:** Up to 3,000 IOPS
- **Baseline performance:** 3 IOPS/GB, up to a maximum of 10,000 IOPS
- **Minimum IOPS:** 100 for volumes smaller than 33.33 GiB

### General Purpose SSD (gp3)

- **Size range:** 1 GB to 16 TB
- **Baseline performance:** 3,000 IOPS and 125 MiB/s
- **Provisioned performance:** Up to 16,000 IOPS and 1,000 MiB/s
- **Minimum IOPS:** 3,000

### Provisioned IOPS SSD (io1)

- **Size range:** 4 GB to 16 TB
- **Provisioning:** Up to 50 IOPS per GB
- **Maximum IOPS:** 64,000 IOPS
- **Minimum IOPS:** 100

### Provisioned IOPS SSD (io2)

- **Size range:** 4 GB to 16 TB
- **Provisioning:** Up to 500 IOPS per GB
- **Maximum IOPS:** 64,000 IOPS
- **Minimum IOPS:** 100

### Throughput Optimized HDD (st1)

- **Size range:** 500 GB to 16 TB
- **Baseline throughput:** 40 MiB/s per TB
- **Burst capability:** Up to 500 MiB/s
- **IOPS specifications:** Not applicable (throughput optimized)

### Cold HDD (sc1)

- **Size range:** 500 GB to 16 TB
- **Baseline throughput:** 12 MiB/s per TB
- **Burst capability:** Up to 80 MiB/s
- **IOPS specifications:** Not applicable (throughput optimized)

### Magnetic (standard)

- **Size range:** 1 GB to 1 TB
- **Burst capability:** Up to hundreds of IOPS
- **Average performance:** 100 IOPS
- **Minimum IOPS:** Not specified for this type


[10:11 am, 22/12/2023] Ishtiaq Ahmed: https://docs.google.com/document/d/1Lq7awc_FQoEHIn_yA6hmkYQxUEV1eL6Ofw1zjV8nRlM/edit
[11:43 am, 22/12/2023] Satyanarayana: Increase EBS Volume Size in AWS
===========================================================
Step 1: Take Snapshot of EBS Volume (to be Safe).
Step 2: Increase EBS Volume Size in AWS Console.
Step 3: Extend a Linux file system after resizing a volume.


Command to Extend the file system:

df -hT

Check whether the volume has a partition:
sudo lsblk

Extend the partition:
sudo growpart /dev/xvda 1

Extend the file system on /:
[XFS file system]: sudo xfs_growfs -d /
[Ext4 file system]: sudo resize2fs /dev/xvda1


===========================================================




Attach new EBS volume:
=============================================================
Step:1- create a new ebs
Step:2- attach to instance
Step:3- mount file system

Mount file system commands

sudo lsblk
df -hT
file -s /dev/xvdf
mkfs -t ext4 /dev/xvdf
file -s /dev/xvdf
mkdir -p /app/frontend
mount /dev/xvdf /app/frontend
df -hT


=============================================================
