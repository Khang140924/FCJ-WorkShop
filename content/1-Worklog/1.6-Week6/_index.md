---
title: "Week 6 Worklog"
date: 2026-06-08
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Research SQL and NoSQL database service types on the AWS cloud environment.
* Learn and practice using the Amazon RDS relational database service (MySQL/PostgreSQL).
* Explore and practice using the high-performance Amazon DynamoDB NoSQL database service.
* Understand database security, automated backups, and Multi-AZ high availability features.
* Practice configuring secure connections from a backend application on an EC2 instance to the database system.
* Complete practical bonus tasks (Labs) to earn AWS Credits.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Research the theory of database service types on the AWS platform: Relational Database (RDS) and Non-relational Database (NoSQL) <br> - Watch video lectures on Database on AWS | 08/06/2026   | 08/06/2026      | YouTube AWS Study Group |
| 3   | - Learn in-depth about Amazon RDS, DynamoDB, and the Managed Service concept <br> - Research database security, backup mechanisms, and Multi-AZ Deployment high availability features | 09/06/2026   | 09/06/2026      | Platform Bootcamp |
| 4   | - **RDS Practice:** <br>&emsp; + Initialize an RDS DB Instance (MySQL/PostgreSQL) inside a Private Subnet <br>&emsp; + Configure a Security Group to allow the EC2 server to connect to the database | 10/06/2026   | 10/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - **DynamoDB Practice:** <br>&emsp; + Create tables and learn about Primary Keys (Partition Key & Sort Key) <br>&emsp; + Add data (PutItem) and execute queries on the Console interface | 11/06/2026   | 11/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Advanced Practice (Earn AWS Credit):** <br>&emsp; + Task 3: Set up AWS Budgets (Earn $20 credit) <br>&emsp; + Task 4: Create Lambda Web App (Earn $20 credit) | 12/06/2026   | 12/06/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Week 6 Achievements:

* Mastered the core differences between Amazon RDS (optimal for applications requiring high data consistency and complex relations) and Amazon DynamoDB (optimal for applications requiring ultra-fast read/write speeds, flexible schemas, and massive scaling).

* Fully understood the Managed Service concept: AWS takes responsibility for installation, OS patching, and backups, allowing developers to focus entirely on data structure design and backend coding.

* Comprehended the Multi-AZ mechanism: How AWS automatically fails over to a database replica in another Availability Zone during an outage, ensuring continuous application availability.

* Successfully initialized an RDS DB Instance running a MySQL/PostgreSQL database engine securely within a Private Subnet.

* Correctly configured a Security Group rule to allow a backend server (running on an EC2 instance) to seamlessly connect to database ports 3306 or 5432.

* Proficiently operated Amazon DynamoDB by creating tables, defining Primary Keys, adding data items (PutItem), and executing queries via the Console interface.

* Learned how to utilize the Snapshot feature for manual database backups and schedule automated backup baselines for the database architecture.

* Accumulated practical experience in connecting backend applications to a Database via specialized Endpoints instead of static IP addresses, enhancing system flexibility during maintenance or upgrades.

* Developed an architectural mindset: Knowing exactly when to choose an SQL solution to guarantee data integrity versus when to deploy NoSQL to handle high-concurrency traffic volumes.

* Successfully completed 2 extended Lab assignments (Task 3: Set up AWS Budgets and Task 4: Create Lambda Web App), earning an additional $40 in AWS Credits to fund upcoming hands-on experimentation.