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

1. **EC2 Instance Types Overview:**
   - AWS offers a variety of EC2 instances optimized for different use cases.
   - Each instance type is designed to meet specific performance, computing, and memory requirements.
   - The selection of an instance type depends on the nature of the workload and the desired balance of resources.

2. **Naming Convention:**
   - Instances follow a specific naming convention, as exemplified by "m5.2xlarge."
   - **m:** Represents the instance class, indicating the general purpose or balance of compute, memory, and networking resources.
   - **5:** Denotes the generation of the instance. AWS continually improves and releases new generations of instances.
   - **2xlarge:** Specifies the size within the instance class, indicating the specific configuration and capacity of the instance.

3. **Instance Class:**
   - The instance class (e.g., "m") defines the general characteristics of the instance, such as its intended use case and resource balance.
   - Other common instance classes include "c" for compute-optimized, "r" for memory-optimized, and "t" for burstable performance instances.

4. **Generation:**
   - The generation number (e.g., "5") indicates the iteration or version of the instance type.
   - New generations often bring improvements in performance, efficiency, and additional features.

5. **Size Within Instance Class:**
   - The size within the instance class (e.g., "2xlarge") specifies the specific capacity and configuration of the instance.
   - Different sizes offer varying amounts of vCPUs, memory, and storage.

6. **Instance Types Use Cases:**
   - AWS provides a detailed overview of each instance type and its recommended use cases on the EC2 Instances webpage.
   - Users can choose instances tailored to applications such as general computing, memory-intensive tasks, high-performance computing, and more.
   
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

## PURCHASING OPTIONS

1. **On-Demand Instances:**
   - Suitable for short workloads with predictable pricing.
   - Billed per second for Linux or Windows (after the first minute).
   - No upfront payment or long-term commitment.
   - Recommended for short-term and unpredictable workloads.

2. **Reserved Instances:**
   - Offers up to a 72% discount compared to On-Demand.
   - Reserved for 1 or 3 years.
   - Payment options include No Upfront, Partial Upfront, and All Upfront.
   - Recommended for steady-state usage applications (e.g., databases).
   - Can be bought and sold in the Reserved Instance Marketplace.

3. **Convertible Reserved Instances:**
   - Similar to Reserved Instances but with flexibility to change attributes.
   - Allows changes to the instance type, family, OS, scope, and tenancy.
   - Offers up to a 66% discount.

4. **Savings Plans:**
   - Offers a discount based on long-term usage (up to 72%, similar to RIs).
   - Commits to a specific type of usage for 1 or 3 years.
   - Billed at On-Demand prices beyond the committed usage.
   - Locked to a specific instance family and AWS region.
   - Flexible across instance size, OS, and tenancy.

5. **Spot Instances:**
   - Provides a discount of up to 90% compared to On-Demand.
   - Instances can be terminated at any time if the max price is below the spot price.
   - Most cost-efficient for resilient workloads, batch jobs, data analysis, etc.
   - Not suitable for critical jobs or databases.

6. **Dedicated Hosts:**
   - A physical server fully dedicated to your use.
   - Addresses compliance requirements and supports existing licenses.
   - Purchasing options include On-Demand and Reserved (1 or 3 years).
   - Most expensive option, useful for software with complex licensing or strong compliance needs.

7. **Dedicated Instances:**
   - Instances run on hardware dedicated to your account.
   - May share hardware with other instances in the same account.
   - No control over instance placement, as hardware can be moved after Stop/Start.

