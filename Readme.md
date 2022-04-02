# Amazon Web Services - AWS Cloud Practitioner Certification
<p align="center">
  <img width="384" height="384" src="/img/AWS-Certified_Cloud-Practitioner_512x512.png">
</p>

### Introduction

AWS Cloud Practitioner Certification is a professional certification that is designed to provide the basic knowledge of the AWS Cloud Infrastructure. AWS offers around 319 different services that can be used to build, deploy, and manage applications. However, the AWS Cloud Practitioner Certification covers around 40 different AWS services.

### What is Cloud Computing?
- On Demand Delivery of Compute Power, Storage, Networking, Security and Other Services
- Pay-as-you-go pricing
- Flexible and Scalable Infrastructure

### Types of Cloud Models
1. **Private Cloud** - Cloud Services are hosted on private servers that are not accessible to the public internet.
2. **Public Cloud** - Cloud Resources owned and operated by Cloud Service Providers like Amazon, Microsoft, Google, DigitalOcean, IBM etc. and cloud services are distributed through the internet.
3. **Hybrid Cloud** - Some Servers are on premises and some are on the cloud, this way there is better control over sensitive data.

### Advantages of Cloud Computing
- Flexibilty
- Scalability
- Cost Savings
- Elasticity
- High Availability
- Agility

### Types of Cloud Computing
<p align="center">
  <img width="776" height="468" src="/img/IaaS_PaaS_SaaS.JPG"> 
</p>

1. Infrastructure as a Service (IaaS)
    * Building blocks for Cloud IT
    * Provides Networking, Compute, Storage
    * Flexibility
2. Platform as a Service (PaaS)
    * No need to manage the underlying infrastructure
    * Focus on deployment and management of your application
3. Software as a Service (SaaS)
    * Product that is run and managed by provider for our usage.

### Pricing for AWS Cloud
- Compute - Pay for the compute time used.
- Storage - Pay for data stored in the cloud.
- Networking - Pay for the Data flows out of the cloud.

### AWS Infrastructure
1. AWS Regions
    * Regions are all across the world
    * Every Region has unique name/code eg. us-east-1 or af-south-1 or us-west-2
    * Region == Cluster of Data Centers located near each other.
    * Services are available on regional basis.
2. AWS Availability Zones
    * Each region has multiple availability zones usually around 3, min 2 and max 6
    * AZs are separate from each other
    * Connected with High Bandwidth, Ultra-Low Latency Network
3. AWS Edge Locations (Points of Presence)
    * 216 Points of Presence
    * 84 Cities
    * 42 Countries

### IAM - Users & Group

IAM is Identity and Access Management and it is a global service.
Root account is created by default and we should create groups and users should be placed in groups. Sometimes a user can't be part of a group and some users can be part of multiple groups.
IAM Permissions are managed with JSON document called policies.
Like everywhere else, **Least Privilege Principle** is used here as well.

- Policies 
    * Group - Group inherits permission from Group Policy
    * Inline - Inline policy is only attached to a user
- Police Structure 
    * Version Number - Version of the Policy Language
    * ID - An Identifier for the Policy
    * Statement 
        * SID - Identifier for the statement
        * Effect of Policy - whether the statement allows or denies access
        * Principal - account/user/role to which policy applies
        * Action - list of actions this policy allows or denies
        * Resource - list of resources to which  actions applied to
- Password  Policy
    * Strong Passwords
    * Min password length
    * Characters requirements
    * Password Change after a time period
    * Preventing Password re-use
- IAM Roles for Services
    * Some services will need to perform actions on my behalf
    * Assign permissions to AWS Services with IAM Roles
- Security Tools
    * IAM Credentials Report - Report that lists all your account's users and the status of their various credentials
    * IAM Access Advisor - Shows the service permissions granted to a user and when those services were last accessed and we can find which permissions are not used so we can remove them.
- Best IAM Practices
    * Dont use root account
    * 1 account per person
    * Assign permissions to group and then add the users to the group to inherit permissions
    * Use strong password policy
    * Enforce MFA
    * Create roles to give permission for AWS Services

### Elastic Compute Cloud (EC2)
EC2 Consists of VMs, Virtual Drives for Storage, Load Balancer, Auto-Scaling groups.
For OS, EC2 offers Linux, Windows and MacOS. For Processing, EC2 has options for various CPUs and GPUs with multiple processing cores.
For Storage, there is network attached storage (EBS & EFS) and Hardware attached (EC2 Instance Store)
For Networking, EC2 offers various network cards and public IP addresses.
EC2 also offers Firewall rules thru **Security Groups** and Bootstrap script that contains User Data for the first launch.

- EC2 User Data Script
    * Script is only run once at the first start of the instance
    * Used for Automating boot tasks
    * Runs with Sudo Permissions

```bash
#! /bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>What up Pimps</h1><h2> from $(hostname -f)</h2>" > /var/www/html/index.html
```

- Instance Types
    * Different types of EC2 instances are listed here (https://aws.amazon.com/ec2/instance-types/)
    * Naming Convention Eg - **m6.medium**
        * **m** = instance class
        * **6** = hardware gen
        * **medium** = size within the class
    * General Purpose - Good for code repos and web servers, has good balance of Compute, Networking & Memory
    * Compute Optimized - Good for Compute-intensive tasks like media transcoding, machine learning, gaming servers, etc.
    * Memory Optimizied - Good for memory intensive tasks like  data processing, distribution of web scale cache stores, etc.
    * Storage Optimized - Good for storage intensive tasks like high seq read and write acess to large data sets. Eg. Data Warehousing

- Security Groups
    * Control how traffic is allowed in or out of EC2 Instances.
    * Similar to Port Forwarding on Home Network.
    * Firewall outside EC2 Instance
    * Regulate Access to Ports and control of inbound and outbound network.
    * Locked to Region/VPC
    * By Default -
        * All Inbound Traffic is **BLOCKED**
        * All Outbound Traffic is **ALLOWED**
- Roles for EC2 Instance
    * Action > Security > Modify IAM Role and Attach the IAM Role to the EC2 Instance
    * Only attach policy thru IAM Role
- Instance Purchasing Options
    * Reserved Instances
        * Standard 
            * Long Workloads
            * 75% discount for period over 1 year 
            * Higher discount for 3 year or longer commitment
            * Discount for Upfront and Partial Upfront payments
            * Specific Instance Type
        * Convertible 
            * Long Workloads with Flexible Instances
            * Can Switch Instances
            * Upto 54% discount
        * Scheduled Reserved 
            * Launch within a certain reserved time
            * Commitment of 1 to 3 years is required
    * Spot 
        * Upto 90% compared to On-Demand
        * But can be lost if MAX PRICE < CURRENT SPOT PRICE
        * Most cost-efficient
        * Use for workload that are resilient to failure

    * Dedicated Hosts 
        * Phyical Server with EC2 Capacity
        * Good for Compliance Requirements
        * Existing Server-bound Software licenses can be used
        * 3 year period reservation required
        * More expensive
        * No other AWS customers can use this
    * Dedicated Instances
        * Use of Dedicated Phyical Server
        * Per instance billing
        * Automatic instance billing

### EC2 Instance Storage
- EBS Volume 
    * Elastic Block Store volume is a network drive that can be attached to a instance.
    * Helps keep the data even after the ec2 instance termination
    * Bound to a specific Availability Zone
    * Capacity needs to be provisioned in advance
- Snapshot
    * Basically a BACKUP of a EBS Volume 
    * Snapshots can be copied from one region or AZ to other
    * A new volume can be created from a snapshot
- AMI Amazon Machine Image
    * Pretty much custom OS image
    * Can be created on a specific region and be copied across
    * AMIs are provided by Amazon, can be created by us or can be purchased from AWS Marketplace
- EC2 Image Builder
    * Automates the creation, maintainence and validation of AMIs
    * Can be run on a schedule
    * Free Service (pay only for EC2 instance that is created by Ec2 Builder)
- EC2 Instance Store
    * EBS Volumes are network drives which are good for most cases but have limited performance 
    * EC2 Instance Store is phyical disk that can be connected to the machine for better performance 
    * Storage is lost on termination
    * Good for buffer / cache or temp content
    * Risk of data loss if hardware fails
    * Backup and replication is our responsibility 
- EFS Elastic File System
    * Managed NFS that can be mounted to multiple EC2
    * EFS works with Linux EC2 in multi-AZ
    * 3 x epensive than gp2
    * Shared file system for EC2s
- EFS Infrequent Access
    * Used for less used data
    * 92% discounted
    * EFS will move files to EFS-IA that are less frequently used based on the Lifecyle Policy
- Amazon FSx for Windows File Server
    * Scalable Windows Native Shared File System
    * Supports SMB and NTFS
    * Integrated with Active Directory
    * Can be accessed from on-premises or AWS
- Amazon FSx for Lustre
    * Lustre derived from Linux and Cluster
    * High Performance Scalable file storage system.
    * Good for ML, Data Modeling, Video Processing etc.
    * Can be accessed from on prem or AWS Cloud. Luste stores data on Amazon S3.
    * Uses Linux Filesystem ofcourse 

### Elastic Load Balancing & Auto Scaling 

- High availability & Scalability
    * Vertical Scaling - Increasing or Decreasing Instance Size (t2.micro to t2.large)
    * Horizontal Scaling - Adding or Removing more Instance (1 x t2.micro to 2x or more t2.micro)
    * High Availability 
        * Auto Scaling Group in Multi AZ
        * Load Balancer in Multi AZ
        * Instances in multi AZ
    * Agility - Reduced time for availability of resources

- Elastic Load Balancer
    * Directs traffic to multiple Instances
    * Balances the load by spreading load
    * Single point of Access
    * Can be used across multiple AZs
    * AWS offers 3 kind of ELB
        * Application Load Balancer - Layer 7
        * Network Load Balancer (Ultra High Performance allows TCP)- Layer 4
        * Classic Load Balancer - Layer 4 & 7
- Auto Scaling Group
    * Scale out to match increased load
    * Scale in to match decreased load
    * Auto register new machines to load balancer
    * Replace unhealthy instance with health instance
- Auto Scaling Strategies
    * Manual Scaling - Updating the ASG size manually
    * Dynamic Scaling 
        * Simple/Step Scaling - Based on CPU or Network or Requests
        * Target Tracking Scaling - Average requirement to be a specific target like (69% CPU utilization, more than that new instance is deployed)
        * Scheduled Scaling - Based on Usage Patterns
        * Predictive Scaling - Machine Learning Prediction of future traffic
### Amazon S3
Cloud Native Storage. Inifinitely Scaling Storage.
Backbone for many websites. Snapshots are stored in S3
- Usage     
    * Backup and Storage
    * Disaster Recovery
    * Archive
    * Hybrid Cloud Storage
    * Apps Hosting
    * Data Analysis
    * Static Websites
    * Media Hosting
- Overview       
    * File = Objects
    * Directories = Buckets
    * Buckets must have globally unique name
    * Buckets are regional level
    * Naming Convention
        * No Uppercase
        * No underscore
        * 3-63 Characters Long
        * Can't be an IP
        * Must start with lowercase letter or number
    * Object can't be over 5TB
    * More than 5GB upload should be in multi-part
- S3 Security
    * IAM Policy
    * Resource Based Security
        * Bucket Policies
        * Object Access Control List
        * Bucket Access Control List
    * Encryption
    * IAM Policy for Users or Group or EC2 Instance Role & S3 Bucket Policy for Anonymous Access or Users on Different AWS Account

- S3 Policies
    * JSON based Policies
    * Grant Public Access
    * Grant Access to Users on Different Account
- S3 Verioning
    * Bucket Level
    * Best Practise to Version Buckets
    * Protection against accidental deletion
- S3 Access Logs
    * Log all access to S3 Buckets
    * Any request made to S3 from any account whether authorized or denied will be logged.
    * these logs can be used for Data Analysis
    * Helpful for finding root cause of an issue, or viewing suspicious patterns.
- S3 Replication
    * CRR = Cross Region Replication
    * SRR = Same Region Replication
    * Bucket can be in different accounts
    * Copying happens in background
    * Must give proper IAM permissions to S3

<p align="center">
  <img width="807" height="349" src="/img/S3_storage_class.JPG"> 
</p>

- S3 Storage Classes
    * S3 Standard
        * General Purpose
        * Low latency
        * High throughput
        * Frequently used data
        * Content Distribution, Big Data Anaylsis
    * S3 Standard IA
        * Infrequent Access
        * Less Frequent Accessed but requires Rapid Access
        * Lower cost then S3 Standard, but retrieval fees applies
        * Recovery and Backup
    * S3 One Zone-Infrequent Access
        - Data is stored only in one AZ
        - Lower cost compared to S3-IA
        - Used for storing secondary data
    * Amazon S3 Intelligent Tiering
        - Low latency and High Throughput like S3 Standard
        - Cost Optimized by moving objects between Frequent and Infrequent
        - Resilient against events that impact an AZ
    * Amazon Glacier
        - Archiving and Backup usage
        - Long term usages (years)
        - Retrieval time and fees 
            * Expedited (1 to 5 mins)
            * Standard (3 to 5 hrs)
            * Bulk (5 to 12hrs)
    * Amazon Glacier Deep Archive 
        - Cheapest S3 Tier
        - Standard (12hrs)
        - Bulk (48hrs)
- Transition Rule   
    * Transition objects between storage classes
    * Can be automated with Lifecycle Configuration
    * Eg - Moving files from S3 IA to Glacier 
- S3 Object Lock and Glacier Vault Lock
    * Write Once Read Many
    * Block an Object version deletion for specific amount of time
    * Lock the Policy for future edits in case of Glacier Vault Lock
    * Helpful for compliance and data rention
- Snow Family
    * Highly secure portable devices to collect and process data and migrate data in and out of AWS.
    * Data Migration Devices 
        * Snowcone 
        * Snowball Edge
        * Snowmobile
    * Edge Computing 
        * Snowcone 
        * Snowball Edge
    * Why use data migration devices?
        * Limited Connectivity
        * Limited Bandwidth
        * High Network Cost
        * Connection Stability
    * Snowball Edge 
        * Used for moving TB or PB data to AWS
        * Pay per data transfer job
        * S3 compatible storage 
        * Storage Optimized Version - 80TB HDD Capacity
        * Compute Optimized Version - 42TB HDD Capacity
        * Large data cloud migration 
        * 52vCPUs, 208GB RAM, Optional GPU (Compute Optimized)
        * 40vCPUs, 80GB RAM (Storage Optimized)
    * Snowcone
        * Smaller than Snowball Edge
        * Rugged, secure and can withstand harsh environments
        * 4.5lbs
        * 8TB of storage
        * Own battery and cable is needed
        * Can be used with AWS DataSync or send it to AWS and they can import data.
        * 2CPUs, 4GB RAM, wired or wireless acess, USB-C powered
    * Snowmobile
        * For transferring Exabytes of Data
        * Each Snowmobile has 100PB capacity
        * High Security, Temperature Controlled, GPS 24/7 video surveillance
    * Edge Computing
        * Edge Location - Limited or no internet or access to computing power
        * Snowball and Snowcone are good for the use case
        * Process data while its being created on edge location
        * Can be shipped back to AWS
        * Can run EC2 Instances and AWS Lambda
        * Discount for 1-3 year period
    * AWS OpsHB
        * GUI for controlling Snow Devices
        * Monitoring and Launching Services
