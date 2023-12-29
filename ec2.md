# Elastic Compute Cloud (EC2) Overview

**Regional Service:**
- EC2 is an Infrastructure as a Service (IaaS) provided by AWS.
- It operates on a regional level, and instances can be launched in different AWS regions.

**Instance Lifecycle:**
- Stopping and starting an instance may change its public IP but not its private IP.
- AWS Compute Optimizer recommends optimal AWS Compute resources for workloads.

**User Data:**
- User Data contains commands that run when an instance is launched for the first time.
- It automates dynamic boot tasks, including installing updates, software, and downloading files.
- Runs with root user privileges.

**Instance Classes:**
- General Purpose: Suitable for diverse workloads like web servers or code repositories.
- Compute Optimized: Ideal for compute-intensive tasks like batch processing, media transcoding, HPC, and gaming servers.
- Memory Optimized: Great for in-memory databases or distributed web caches.
- Storage Optimized: Designed for storage-intensive tasks like accessing local databases, OLTP systems, and DFS.

**Security Groups:**
- External firewall for EC2 instances, allowing or blocking inbound/outbound traffic.
- Rules only contain Allow statements.
- Default Security Group allows inbound traffic from the same group and permits all outbound traffic.

**IAM Roles for EC2 instances:**
- IAM Roles are recommended for EC2 instances to avoid entering AWS credentials directly into instances.

**Purchasing Options:**
- On-demand Instances: Pay per use with no upfront payment, suitable for short-term, unpredictable workloads.
- Reserved Instances: Offered in Standard (1 or 3 years), Convertible, and Scheduled types.
- Spot Instances: Work on a bidding basis and are cost-effective for resilient workloads.
- Dedicated Hosts: Provide dedicated server hardware allocated to a specific company.

**Elastic IP:**
- Static public IP that you own as long as it is associated with a running EC2 instance.
- Can be attached to a stopped instance.
- Soft limit of 5 Elastic IPs per AWS account.

**Spot Instances, Spot Requests, and Spot Fleets:**
- Spot Instances work on a bidding basis and are suitable for resilient workloads.
- Spot Requests can be one-time or persistent, and Spot Fleets combine spot and on-demand instances.
- Spot Fleets can use launch templates and have different allocation strategies.

**On-Demand Capacity Reservations:**
- Ensure available capacity in an Availability Zone (AZ) to launch EC2 instances when needed.
- Can reserve for a recurring schedule without a long-term commitment.

**Comparison of Reserved Capacity & Instances:**
- Image provided for visual representation of Reserved Capacity and Instances.

