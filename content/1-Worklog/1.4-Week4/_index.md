---
title: "Week 4 Worklog"
date: 2026-05-25
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

* Research the theoretical overview of core cloud storage types: Block Storage, Object Storage, and File Storage.
* Learn in-depth about the object storage service Amazon Simple Storage Service (Amazon S3) and its accompanying advanced features.
* Explore block storage and shared data solutions for virtual server systems: Amazon Elastic Block Store (Amazon EBS) and Amazon Elastic File System (Amazon EFS).
* Practice initializing an S3 Bucket, configuring secure access permissions, and managing data lifecycles on the console interface.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :--- | :--- | :--- | :--- | :--- |
| 2 | - Research the theory of storage types on AWS: Amazon S3, EBS, and EFS. <br> - Watch the visual lecture series on Storage Services. | 25/05/2026 | 25/05/2026 | YouTube AWS Study Group |
| 3 | - Distinguish the nature and use cases of Block Storage, Object Storage, and File Storage models. <br> - Read the data management guide and storage drive differentiation documents. | 26/05/2026 | 26/05/2026 | Platform Bootcamp |
| 4 | - Practice initializing an Amazon S3 Bucket, configuring detailed data access permissions (Public/Private), and enabling the version management feature (S3 Versioning). | 27/05/2026 | 27/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | - Deploy an application and configure the Static Website Hosting feature directly on the Amazon S3 platform. | 28/05/2026 | 28/05/2026 | https://cloudjourney.awsstudygroup.com/ |

### Week 4 Achievements:

* Mastered the concept of Object Storage (Amazon S3), clearly understanding why S3 is the optimal solution for storing static data (images, videos, documents) for Web/App applications due to its outstanding durability of up to 99.999999999% (11 nines).
* Clearly distinguished the differences between Amazon EBS (a high-performance block storage drive attached to a single EC2 server instance) and Amazon EFS (a shared file system allowing multiple EC2 instances to connect and share data simultaneously).
* Understood the security mechanisms on S3 storage by configuring Bucket Policies, Access Control Lists (ACLs), and the Versioning feature to prevent data from being overwritten or accidentally deleted.
* Successfully initialized an Amazon S3 Bucket and proficiently performed upload/download operations of data objects directly via the AWS Management Console.
* Correctly configured the Static Website Hosting feature on Amazon S3, successfully deploying a static website running directly on the Internet without incurring costs for renting and maintaining an EC2 server.
* Practiced writing and successfully configuring S3 Bucket Policies in JSON code format to tightly control access permissions from external networks.
* Understood how to design an optimized Storage Layer for a backend application: instead of storing media files directly on the server's local hard drive (which fills up the disk and increases costs), a Backend Engineer will call APIs to push this data directly to Amazon S3.
* Developed a Cost Optimization mindset through data classification to apply appropriate S3 Storage Classes (Standard for frequently accessed data and Glacier for long-term archival data).