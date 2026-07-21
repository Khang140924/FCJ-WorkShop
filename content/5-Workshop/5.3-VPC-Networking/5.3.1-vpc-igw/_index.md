---
title: "VPC & Internet Gateway"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---

### 1. Provisioning Amazon VPC
The first step is to create a completely isolated network space on AWS.
*   **VPC Name:** `FinVantage-Production-VPC`
*   **IP Range (IPv4 CIDR block):** `10.0.0.0/16`. This IP range provides up to 65,536 IP addresses, which is perfectly abundant for the system to auto-scale Lambda functions and other resources later.

### 2. Setting up the Internet Gateway (IGW)
For our VPC to communicate with the outside world (the Internet), an Internet Gateway must be attached.
*   Create an IGW named `FinVantage-IGW`.
*   Perform the **Attach to VPC** action and select the newly created `FinVantage-Production-VPC`.

### 3. Partitioning Public Subnets
We create 2 Public Subnets located in 2 different Availability Zones (AZs) to ensure High Availability.
*   **Public Subnet 1:** CIDR `10.0.1.0/24` (Located in AZ `us-east-1a`)
*   **Public Subnet 2:** CIDR `10.0.2.0/24` (Located in AZ `us-east-1b`)
*   Enable the *Auto-assign public IPv4 address* feature for these 2 subnets.

> 📸 **[IMAGE INSERTION REMINDER]:** Take a screenshot of the newly created Subnets list in the VPC Console interface, clearly showing the IPv4 CIDR and Availability Zone columns.
> *Markdown code:* `![Public Subnets List](../../../images/public-subnets.png)`