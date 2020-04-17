---
title: AWS Storage
date: '2020-04-11'
slug: aws-storage
categories:
  - aws
  - certification
---


    
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

Tuto:

  * S3 --> Create Bucket 
  * Bucket name: unique name
  * Region
  * Versioning
  * Server access logging
  * Permission
  * Review
  * Create folder 
  * uploder
    * Permission 
    * Storage class

S3 Storage class:

  * S3 Standard   
    * Lifecycle rule --> S3 INT
  * S3 INT   
  * S3 S-IA  
  * S3 Z-IA   
  * S3 Glacier
    * Moving Data into S3 Glacier for the 1er time: Create your vaults as a container for your archives --> Move your data into the Glacier vault using the availabke APIs or SDKs
    * APIs, SDKs, CLI
    * Retrieval options
      * Expediteed: under 250MB, available in 5 mins 
      * Standard: any size, avalable in 3-5 hours
      * Bulk: PB of data at a time 5-12 hours
  * S3 G_DA: the cheapest, minimal access Retrieval within 12 hours

# Using Amazon S3 Bucket Properties & Management Features to Maintain Data

## Versioning

This is a bucket feature that allows for multiple versions of the same object to exist. This is useful to allow you to retrieve previous versions of a file, or recover a file should it subjected to accidental deletion, or intended malicious deletion of an object.

Versioning is managed automatically against objects when you overwrite or delete an object in a bucket that has versioning enabled. To ensure you are always working with the most current version of an object, only the latest version of the object is displayed within the console.

Versioning is not enabled by default, however, once you have enabled it, you can't disable it. instead, you can only suspend it on the bucket which will prevent any further versions from being created of your objects, but it will keep all existing versions of objects up to the point of suspension. 

## Server-Access Logging

when server-access logging is enabled on a bucket it captures details of requests that are made to that bucket and its objects. Logging is important when it comes to security, root-cause cause analysis following incidents, and it can also be required to conform to specific audit and governance certifications.

Bucket owner - Represents the canonical user ID of the owner of the Source bucket. The canonical user ID is used for cross-account access via bucket policies.

Bucket - This shows the name of the bucket related to the request.

Time - This is a timestamp of the request in UTC (Coordinated Universal Time).

Remote IP Address - Represents the internet address of the identity carrying out the request.

Requester - For authenticated users, this field will show the IAM identity. For any unauthenticated users a hyphen (-) would be displayed instead.

Request ID - A random string to identify each request.

Operation - This will display the operation of the request that was carried out.

Key - The "key" part of the request, URL encoded, or if no key parameter is used then a hyphen will be displayed as in this example. A hyphen in any field of the request indicates that the available data was not known or was not applicable for the request.

Request URI - This represents the Request-URI element of the HTTP request.

HTTP Status - This displays the HTTP status returned from the request as a numeric value.

Error Code - If an error was experienced, then S3 will return the error code received.

Bytes Sent - The number of bytes sent as a response.

Object Size - The size of the object in question in the request.

Total Time: - Measured in milliseconds, it represents how long the request took from receiving the request to the last byte of sending a response.

Turn-Around Time - This shows how long it took S3 to process the request.

Referer - The value is taken from the HTTP referer header, however, in this case, there was none present and so a hyphen is represented as the value.

User-Agent - This shows the value taken from the HTTP user-agent header.

Version ID - If present, this will show the Version ID of the request.

Host Id - The x-amz-id-2 or Amazon S3 extended request ID. The x-amz-id-2 header is a token that is used together with the x-amz-request-id header to help AWS troubleshoot problems.

Signature Version - This will show which signature version was used to authenticate the request.

Cipher Suite - If SSL was used it will show which cipher suite was used. If HTTP was used, then a hyphen would be shown instead.

Authentication Type - This shows the type of authentication used for the request.

Host Header - Represents the endpoints used to connect to Amazon S3 in the request.

TLS Version - This shows which version of TLS was used by the client.


## Static Website Hosting

S3 endpoint as your website URL address. Firstly, it does not support HTTPS requests. The bucket and its contents must be marked as publicly accessible. And it does not support Requester Pays.

The other option available to you is Redirect Requests. And this option allows you to redirect all traffic to your website endpoint. 

- Block public access 
- Bucket Policy

## Object-Level Logging

This feature is actually more closely related to the AWS CloudTrail service than S3 in a way, as it’s AWS CloudTrail that performs logging activities against Amazon S3 data events. These data events are specific API calls used in S3, such as GetObject, DeleteObject, and PutObject.

So what is CloudTrail? CloudTrail is a service that has a primary function to record and track all AWS API requests made. These API calls can be programmatic requests initiated from a user using an SDK, the AWS command-line interface, from within the AWS management console or even from a request made by another AWS service.

When an API request is initiated, AWS CloudTrail captures the request as an event and records this event within a log file which is then stored on S3. Each API call represents a new event within the log file. CloudTrail also records and associates other identifying metadata with all the events. For example, the identity of the caller, the timestamp of when the request was initiated and the source IP address.

## Default Encryption

Using default encryption, you are able to set a default encryption mechanism for every new object that is uploaded to the bucket. However, please note that for any objects that are already in your bucket prior to enabling default encryption, they will NOT be encrypted.

- AES-256, also known as SSE-S3 which stands for Server-side encryption using S3 managed keys
- AWS-KMS, this is often referred to as SSE-KMS which stands for Server-side encryption using KMS managed keys. KMS is the Key Management Service. 

## Object Lock

This feature is often used to meet a level of compliance known as WORM, meaning Write Once Read Many.. It allows you to offer a level of protection against your objects in your bucket and prevents them from being deleted, either for a set period of time that is defined by you or alternatively prevents it from being deleted until the end of time! The ability to add retention periods using Object Lock help S3 to comply with regulations such as FINRA, the Financial Industry Regulatory Authority.

These retention modes are Governance Mode and Compliance Mode.

By enabling Governance Mode it prevents your users from performing a delete or an overwrite of any of the versions of your objects in the bucket throughout the duration set by the retention period. However, if you have very specific permissions, including s3:BypassGovernanceMode, s3:GetObjectLockConfiguration, s3:GetObjectRetention, then a user will still be able to delete an object version within the retention period or change any retention settings set on the bucket.

When setting Governance Mode you will be asked to add a retention period in days and therefore defines how long the object is protected by object lock preventing it from being deleted. When an object is added to the bucket, a timestamp is added to the metadata reflecting the retention period. When the retention period is over, the object can then be deleted again.

## Tags

It is likely when using Amazon S3 that you are using it for a variety of different use cases and solutions, across multiple business units and departments, each with different cost centers. This can make it difficult to manage budgets across your organization. Using bucket tags, known as S3 cost allocation tags, you can assign key-value pairs at the bucket level to help with categorization. 

Using the Cost Explorer from within your AWS Billing and Cost Management, you can report on these Key values, for example, you could identify and highlight the costs associated with your resources that were tagged with Project:CloudAcademy. This will highlight all the AWS resources that had this key value pair allowing you to get a full understanding of the project costs for that particular project, in this case, ‘CloudAcademy’.

Adding S3 Cost Allocation Tags To add your tags to your bucket, select your bucket and from the Properties tab select Tags Select the tile and configure your tags as required and click save. One point to note is that you must activate your cost allocation tags from within AWS Billing before they will show up on any reports. To do this, go to your AWS Billing and Cost Management dashboard from within the AWS Management Console, select Cost Allocation tags and then activate any user-defined tags that you created.

## Transfer Acceleration

When transferring data into or out of Amazon S3 from and to your remote client, or to another AWS region, transfer acceleration can dramatically speed up the process by utilizing another AWS service, Amazon CloudFront.

Amazon CloudFront is a content delivery network service (CDN), which essentially provides a means of distributing traffic worldwide via edge locations. AWS edge locations are sites deployed in major cities and highly populated areas across the globe. More information on Amazon CloudFront can be found in our existing course here.

## Events

Any events which are recorded can then be sent to either an SNS Topic, an SQS Queue or a Lambda Function.

Firstly, you need to give your Event a name, followed by the required events that you want to monitor, as you can see there is quite a long list that can be monitored and captured within your bucket covering new objects, object removals, restores, RRS and replication events.

The Prefix element allows you to specify the events to be captured based on the objects prefix within the bucket, for example, you could capture all PUT, COPY and POST events for objects with a prefix of Logs/.

The Suffix provides a similar function of the prefix, it allows you to apply the event captures to objects with a certain suffix, for example all objects with a *.jpg file extension.

The Send to component determines where your events notifications will be sent, either to an SNS Topic, an SQS Queue or a Lambda Function.

Depending on the existing configurations of your destination of event notifications, permissions will need to be granted to your SNS Topic, SQS queue or Lambda function to enable S3 to publish events to them.

## Requester Pays

A fundamental condition of enabling requester pays is ensuring that all access is authenticated to your bucket, as anonymous access requests will not be able to take advantage of the requester pays attribute. This is because AWS would not know which account to charge the request and data download to. By authenticating requests, it allows a trace back to the identity and to which AWS account that identity is originating from, and the cost is then transferred to that account.


# Understanding and Optimizing Costs with AWS Storage Services

## Amazon S3 and Glacier

- S3 Standard - General purpose storage for any type of data, typically used for frequently accessed data

- S3 Intelligent - Tiering - Automatic cost savings for data with unknown or changing access patterns

- S3 Standard - Infrequent Access  - For long-lived but infrequently accessed data that needs millisecond access

- S3 One Zone - Infrequent Access - For re-creatable infrequently accessed data that needs millisecond access

- S3 Glacier - For long-term backups and archives with retrieval option from 1 minute to 12 hours
- S3 Glacier Deep Archive - For long-term data archiving that is accessed once or twice in a year and can be restored within 12 hours