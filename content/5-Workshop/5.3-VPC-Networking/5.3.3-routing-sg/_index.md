---
title: "Routing & Security Groups"
date: 2026-07-20
weight: 3
chapter: false
pre: " <b> 5.3.3. </b> "
---

### 1. Route Tables Configuration
Routing tables direct network traffic inside the VPC.
*   **Public Route Table:** Associated with 2 Public Subnets. Add Rule: Route `0.0.0.0/0` (all outbound internet traffic) with Target set to **Internet Gateway (IGW)**.
*   **Private Route Table:** Associated with 2 Private Subnets. Add Rule: Route `0.0.0.0/0` with Target set to **NAT Gateway**. This rule allows Lambda functions to privately call external AI APIs.

### 2. Security Groups Configuration (Firewall Rules)
Instead of traditional IP filtering, AWS Cloud uses Security Groups (SGs).
*   **Create Lambda-SG:** Attached to AWS Lambda functions. Inbound rules empty (no direct ingress). Outbound rules set to Allow All.
*   **Create Database-SG:** Attached to RDS PostgreSQL and ElastiCache. Inbound rules open port `5432` (PostgreSQL) and `6379` (Redis). Key detail: **Source set to Lambda-SG ID instead of IP address**.

This setup guarantees that only authorized Lambda functions can access the database, blocking external scanners.

---

![Figure 5.3.3. Inbound & Outbound Security Group Rules for Database Security Group linked to Lambda Security Group.](../../../images/finvantage-database-sg.jpg)
