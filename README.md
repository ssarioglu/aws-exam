# AWS Exam

## Sections In the Exam

1. Building a scalable, fault-tolerant and cost-efficient architecture. (60%)
2. Designing secure VPN (applications using AWS Resources), how to use the IA Policies.  (20%)
3. Implementation (for example:  how would you implement a two-tier architecture)/ Deployment (how would you migrate resources to AWS ) (10%)
4. Troubleshooting (example: how would you restore a faulty VM) (10%)

## Exam tips
#### 1. Building a scalable, fault-tolerant and cost-efficient architecture

This is the most important section of the exam as it covers 60% of the total score. Here are the top points you need to know:

**AWS EC2, Load Balancer, and Storage Options:**

In this section, the exam will question your knowledge on various topics such as the payment plans, types of storage for the instances, etc.

**Key points to remember:**

Understand the difference between the three payment plans:
* **On-Demand instances:** pay per hour

Use cases: development/ testing environment.

* **Reserved instances:** 1 or 3-year agreement (up to 60% discount)

Use cases: production-ready application, applications that will be live for a long time.

* **Spot Instances:** bid on the price

Use cases: applications that termination of an instance won’t cause an issue.

Spot Instance: If the price of the spot instance goes above the bid price, or there is not enough capacity, the AWS EC2 instance will receive a termination notice and will be terminated in two minutes.

There are three tenancy options:
* **Shared Tenancy:** Multiple instances run on the same hardware (default option)
* **Dedicated instance:** A dedicated hardware that runs only a single customer instance
* **Dedicated host:** Physical server with full EC2 capacity dedicated to the user. It’s mostly used for Licensing reasons.

Instance store data is lost when an Amazon EC2 instance is restarted or terminated. It is temporary data!

There are four types of AMI’s
* **AMI’s that are published by AWS:** These are maintained and managed by AWS and are very reliable.
* **AWS Marketplace:** You could purchase AMI’s from other providers such as Bitnami, Drupal. You don’t need to install the applications.
* **Existing Instance AMI’s:** AMI’s from a current EC2.
* **Uploaded AMI’s from Virtual Servers:**  These are AMI’s that have been Imported or Exported via AWS Import/Export Service.

**EFS** volume can be mounted on multiple servers.

**EBS** volume can be mounted on a single server.

Public IP is changed on a stop/start of an instance. To avoid the change of IP,  associate an Elastic IP to your instance.
Elastic IP attached to an EC2 instance will not incur any charge! But, if it is not associated you will be charged.

A newly launched Window Instance can be accessed via the Random Password which AWS generates upon the completion of the instance creation.

**Bootstrapping:** Allows you to execute a script when an instance is booted.  Usually, it involves installing certain packages or configuring Chef/Puppet.

**Enhanced Networking:** Is a feature in AWS EC2 which improves the network connectivity. Note: Only specific EC2 types support it and can be enabled in a VPC only.

**Termination Protection** prevents accidental deletion of an EC2 instance.

**Placement Group:**  Let’s you place multiple AWS EC2 instances in a group, this will provide a lower network latency.

There are four types of EBS Volumes:
* **Cold HDD** Use case: applications with few data access. Max IOPS 250.
* **Throughput HDD** Use case: data warehouse, log processing. Max IOPS 500.
* **General Purpose SSD** Use case: OS boot volume, databases. Max IOPS 10,000
* **Provisioned IOPS SSD** Use case: Applications which need very fast data access, large databases Max IOPS 20,000.
---

#### 2. AWS Databases

**OLTP** – Online Transaction Processing (database types: AWS RDS, AWS Aurora)

**OLAP** – Online Analytic Processing (AWS Redshift)

**RPO (Recovery Point Objective)** – the acceptable data loss.

**RTO (Recovery Time Objective)** – the time in future that your application can be live.

* Manual DB Snapshots are not deleted automatically compared to Automated DB Snapshots!

* To create a fault tolerant and high available database architecture, implement Multi-AZ.
Use the DNS name in your application to connect to the database. If the database fails, AWS will update the records so it won’t impact your application.

* Use Read Replicas in a heavy read traffic website.

* Use AWS Redshift bulk import command, it is much more efficient than raw SQL Queries.

* Amazon DynamoDB is the AWS Managed NoSQL database.

* Increase the write efficiency of an Amazon DynamoDB by randomizing the primary key value.

* AWS Aurora is the database engine developed by AWS which is faster and cheaper than AWS RDS.
---

#### 3. AWS Storage, S3, Glacier
This section focuses on various storage options, security of data storage and implement/deployment of storage options.

**Key points:**

* Block level (EBS) and file storage (EFS) are covered here
* AWS S3 is an object storage, everything saved in S3 is stored as data objects.
* Each object consists of a MetaData (created by Amazon) and Data (custom data).
* An object size could be from 0 to 5 TB.
* S3 Objects are replicated across multiple devices within a region!
* S3 Objects are saved in a container called “Bucket“, consider Bucket as the root folder.
* To prevent accidental object deletion, enable versioning and MFA.
* S3 data can be replicated across other regions, this is usually done for compliance. Note: Only new objects will be replicated.
* Bucket names are unique across all AWS Accounts!
* Bucket name must be between 3 and 63 characters and can contain numbers, hyphens or periods.

**Consistency Model of S3**

* When you create a new object, you will receive the latest object. (Read After Write Consistency)PUTS to new object
* When you PUT or DELETE a current object,  AWS provides Eventual consistency, it might take a while for the changes to be affected.

**There are three S3 storage classes:**
* **S3 Standard:** 99.99% availability, ideal for frequently accessed data.
* **S3 Infrequent Access:** 99.9% availability, ideal for less frequently accessed data, cheaper than S3 Standard, minimum object size 128kb
* **S3 RRS (Reduced Redundancy Storage):** 99.99% availability, cheapest. ideal for objects that data loss is not important.
AWS Glacier is ideal for archiving data, data stored in Glacier is not immediately available. Retrieving data takes time.
