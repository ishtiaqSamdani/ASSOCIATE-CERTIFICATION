# ASSOCIATE-CERTIFICATION

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


### Increase EBS Volume Size in AWS

**Step 1: Take Snapshot of EBS Volume**

**Step 2: Increase EBS Volume Size in AWS Console**
1. Go to the AWS Console.
2. Navigate to the EBS section.
3. Select the volume you want to modify.
4. Choose the option to modify the volume.
5. Specify the new, larger size for your volume.

**Step 3: Extend a Linux File System after Resizing a Volume**
After increasing the size of the EBS volume, you need to extend the file system on the volume to use the additional space.

1. Check the file system's disk space usage:
    ```bash
    df -h
    ```

2. Check whether the volume has a partition:
    ```bash
    lsblk
    ```

3. If the volume has a partition, extend it:
    ```bash
    growpart /dev/[volume]
    ```

4. Finally, extend the file system:
    - For XFS file system:
        ```bash
        xfs_growfs /dev/[volume]
        ```
    - For Ext4 file system:
        ```bash
        resize2fs /dev/[volume]
        ```

### Attach New EBS Volume

**Step 1: Create a New EBS Volume**
1. In the AWS Console, navigate to the EBS section.
2. Create a new volume with the desired size and type.

**Step 2: Attach the Volume to an Instance**
1. Once the volume is created, attach it to your instance through the AWS Console.

**Step 3: Mount the File System**
After attaching the volume, mount the file system on the volume to your instance.

1. List the block devices:
    ```bash
    lsblk
    ```

2. Check the file system's disk space usage:
    ```bash
    df -h
    ```

3. Check the file system type of the new volume:
    ```bash
    file -s /dev/[new_volume]
    ```

4. If the file system is not created, create an ext4 file system on the volume:
    ```bash
    mkfs -t ext4 /dev/[new_volume]
    ```

5. Check the file system type again:
    ```bash
    file -s /dev/[new_volume]
    ```

6. Create a mount point for the new volume:
    ```bash
    mkdir /mnt/[mount_point]
    ```

7. Mount the volume to the new mount point:
    ```bash
    mount /dev/[new_volume] /mnt/[mount_point]
    ```

8. Check the file system's disk space usage again:
    ```bash
    df -h
    ```

Feel free to adjust the placeholders like `[volume]`, `[new_volume]`, and `[mount_point]` with the actual values based on your AWS configuration. Let me know if you have any further questions!

