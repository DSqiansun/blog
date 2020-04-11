---
title: Aws Certified Solution Architect Associate
date: '2020-04-11'
slug: aws-certified-solution-architect-associate
categories:
  - aws
  - certification
---

# 考试范围:

 * Domain 1 : Design Resilient Architecteures
    - AWS Global Infrastructure (Regions, Availavility Zone, Edge Locations, Regional Edge Caches)
    - Multi-tiered architecture within a Virtual Private Cloud (VPC)
    - Amazon Route 53
    - Amazon CloudFront
    - Disaster recovery and business continuity strategies
    - Decoupled and event-driven architectures
    - AWS storage services
 * Domain 2 : Design High-Performing Architectures
    - Auto Scaling and application and network elastic load balancers
    - Amazon EC2, ECS and Elastic Beanstalk
    - Storage performance with the Elastic File System and Amazon S3 features
    - VPC Networking compoonents
    - AWS Databases
    - Amazon DynamoDB and Aurora
 * Domain 3 : Design Secure Applications and Architectures
    - AWS Identity & Access Management
    - Amazon Cognito for web & mobile security
    - AWS organizations - Service Control Policies (SCPs)
    - Protecting application with AWS WAF; Firewall Manager and Shield
    - AWS logging mechanisms
    - Audit, monitor and evaluate with AWS Config and AWS CloudTrail
    - Data encryption using the AWS Key Management Service(KMS)
 * Domain 4 : Design Cost-optimized Architectures 
    - AWS Storage costs across Amazon S3, Glacier, EFS, Storage Gateway, AWS Backup
    - Savings plans and reserved instances for compute instances
    
# Introduction to Amazon EBS and EC2 Instance Storage

## AWS Storage Services
### on-premise storage options
- Storage Areas Network(SAN)
- Network Attached Storage(NAS)
- Directly Attached Storage(DAS)
- Tape Backup
  
    
### AWS Data Storage categorization 
- Block Storage:
  - Data is stored in chunks known as blocks
  - Blocks are stored on a volume and attached to a signle instance
  - Provide very low latency
  - Comparable to DAS storage used on premises

- File Storage 
  - Data is stored as separate files with a series of directories
  - Data is stored within a file system
  - Shared access is provided for multple users
  - Comparable to NAS storage used on premises
  
- Object Storage
  - Objects are stored across a flat address space 
  - Objects are referenced by a unique key
  - Each object can also have associated metadata to help categorize and identify the object

### Amazon EBS (Elastic Block Store)
- Provided Block level storage to EC2 instances
- Offers persistent and durable data storage
- Greater flexibility than that of instance store volumes
- EBS can be attached to EC2
- Multiple EBS cans be attached to a single EC2 instance
- EBS Snapshots 
  - Manual 
  - Automatically scheduled
- High Availability
  - replicated multiple time within the sale availability zone
- Volume Types:
  - SSD (Solid State Drive)
    - Suited for work with smaller blocks
    - Databases using transactional workloads
    - often used for boot volumes on EC2 instances
  - HDD (Hard Disk Drive)
    - Designed for workloads requiring a high rate of throughput(MS/s)
    - Big Data Processing & logging information
    - Larger blocks of Data
  - General Purpose SSD (GP2)
  - Provisioned IOPS(IO1)
  - Cold HDD(SC1)
  - Throughput Optimized HDD(ST1)
- Encryption
  - at rest and in transit
  - is managed by the EBS service itself
  - enabled with a checkbox
- Creating:
  - Management Console
    - During the creation of a new EC2 instance
    - As a stand alone EBS Volume
- Changing the size of an EBS Volume
- Pricing 

### EC2 Instance Storage
- temporary
- not recommended for critical or valuable data
- instance stopped --> data is lost


# Amazon S3
Amazon S3 is a fully managed, object-based storage service that is highly available, highly durable, very cost-effective, and widely accessible.

The smallest file size is 0 bytes, the largest file size is 5 terabytes.

The availability of S3 data objects is dependent on the storage class used and this can range from 99.5% to 99.99%.

The difference between availability and durability is this: when looking at availability AWS ensures that the uptime of Amazon S3 is between 99.5% to 99.99%, depending on the storage class, to enable you to access your stored data. 

