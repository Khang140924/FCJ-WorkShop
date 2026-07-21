---
title: "Networking & Security"
date: 2026-07-20
weight: 3
chapter: true
pre: " <b> 5.3. </b> "
---

### Network & Security Infrastructure (VPC Networking)

Welcome! In this chapter, we will explore and establish the first line of defense for the entire FinVantage platform – the **Amazon VPC (Virtual Private Cloud)** network topology.

For a personal financial management application, protecting transaction data and budget information is paramount. A minor network misconfiguration could expose the database to unauthorized external access. Building an isolated network environment is an indispensable foundation.

---

### Why FinVantage Needs a Dedicated VPC

1.  **Isolate Sensitive Resources:** Databases like PostgreSQL or ElastiCache Valkey cannot be exposed directly to the public Internet. By deploying a custom VPC, we isolate them inside private subnets – completely detached from direct inbound Internet access.
2.  **Strict Data Flow Control:** Only valid API requests passing through Amazon API Gateway can safely trigger AWS Lambda functions running inside the VPC to query the database.
3.  **Principle of Least Privilege:** By combining Subnets, Route Tables, and Security Groups, we explicitly define which services and IP ranges are allowed to communicate.

---

### Why AWS Lambda Needs VPC Attachment

Although AWS Lambda functions are inherently serverless execution units, to query PostgreSQL or access Valkey Redis sessions located deep within private subnets, Lambda must be attached to the same VPC. Upon attachment, AWS provisions Elastic Network Interfaces (ENIs) for Lambda to communicate internally and securely.

---

![AWS Console → VPC → Your VPCs.](../../images/finvantage-vpc-overview.png) 

---

### Chapter Learning Agenda

To construct a resilient and secure network topology for FinVantage, we will proceed through 3 targeted lessons:

1.  **Lesson 5.3.1. Create or Verify VPC:** Inspect base VPC topology and configure Internet Gateway for edge routing.
2.  **Lesson 5.3.2. Subnets & NAT Gateway Configuration:** Create public subnets and private subnets distributed across 2 Availability Zones (AZs) for High Availability.
3.  **Lesson 5.3.3. Routing & Security Groups:** Configure Route Tables for egress routing and set up firewall Security Groups for Lambda, RDS Proxy, and Valkey.

Let's begin with VPC verification in the next lesson!
