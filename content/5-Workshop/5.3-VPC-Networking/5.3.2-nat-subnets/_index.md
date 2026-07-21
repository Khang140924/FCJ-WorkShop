---
title: "Public and Private Subnets"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---

### Public and Private Subnets

### Objective
This page guides you on accessing **Subnets** and **NAT Gateways** in the AWS Console to verify public/private network segregation and Multi-AZ configuration for **FinVantage**.

### Overview
For maximum cloud security, an AWS network topology is partitioned into two distinct zones: public subnets exposed to the Internet, and private subnets completely isolated from direct access. Proper subnet setup protects critical data assets.

### Role of Network Subnets in FinVantage
*   **Private Subnets:** Houses the relational database (Amazon RDS PostgreSQL) and cache layer (Amazon ElastiCache Valkey/Redis). For High Availability (HA), RDS and Valkey run Multi-AZ across at least two Private Subnets in different Availability Zones (e.g., `ap-southeast-1a` and `ap-southeast-1b`). If one AZ suffers an outage, the platform automatically fails over to the secondary AZ without data loss.
*   **Public Subnets:** Hosts edge gateways and specifically the **NAT Gateway** (or VPC Endpoints). Because backend Lambda functions reside in Private Subnets without public IP addresses, outbound requests are routed through the NAT Gateway located in a Public Subnet to reach external services like Cognito, STS, or Bedrock.

---

### Verification Steps on AWS Console

#### 1. Verify Subnets List

**Step 1:** From the left menu of the **VPC Console**, click **Subnets**.

**Step 2:** Enter the FinVantage project name into the search filter to display all relevant subnets.

**Step 3:** Inspect the **Availability Zone** column:
*   Ensure the system has at least 2 Public Subnets and 2 Private Subnets.
*   Verify that subnets span different AZs (`ap-southeast-1a` and `ap-southeast-1b`) for high availability.
*   Record the **IPv4 CIDR** blocks for each subnet.

---


#### 2. Verify NAT Gateway

**Step 1:** From the left menu, click **NAT Gateways**. (If using VPC Endpoints, click **Endpoints**).

**Step 2:** Select the NAT Gateway (`FinVantage-NAT` or `finvantage-prod-nat`).

**Step 3:** Inspect the details panel:
*   Verify that **State** shows `Available`.
*   Check the **Subnet** field: Ensure the NAT Gateway is placed inside a **Public Subnet** (placing it in a Private Subnet breaks Internet outbound connectivity).
*   Note the **Elastic IP** address allocated to the NAT Gateway.

---


### Common Troubleshooting
*   **Issue: `Lambda timeout when calling Bedrock API`**
    *   *Cause:* Lambda in Private Subnet cannot reach the Internet because NAT Gateway is misconfigured (placed in Private Subnet) or missing an Elastic IP.
    *   *Resolution:* Check NAT Gateway settings on Console, ensuring the Subnet field points to a Public Subnet attached to an Internet Gateway Route Table.

### Summary
Subnets and NAT Gateway infrastructure are ready, providing secure connectivity for FinVantage backend workloads.
