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
    * Firewall on EC2 Instances
    * Regulate Access to Ports and control of inbound and outbound network.
