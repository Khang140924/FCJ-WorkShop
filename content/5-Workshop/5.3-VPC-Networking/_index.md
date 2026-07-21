---
title: "Routing & Security Groups"
date: 2026-07-20
weight: 3
chapter: false
pre: " <b> 5.3.3. </b> "
---

### 1. Configuring Route Tables
Routing acts like traffic signs, directing data in the correct direction.
*   **Public Route Table:** Attached to 2 Public Subnets. Add Rule: Route `0.0.0.0/0` (all traffic to the Internet) with the Target pointing to the **Internet Gateway (IGW)**.
*   **Private Route Table:** Attached to 2 Private Subnets. Add Rule: Route `0.0.0.0/0` with the Target pointing to the **NAT Gateway**. Thanks to this rule, Lambda can silently invoke the AI API from the internal network.

> 📸 **[IMAGE INSERTION REMINDER]:** Take a screenshot of the Private Subnet's Route Table interface, showing the outbound traffic being directed through `nat-...`.
> *Markdown code:* `![Private Route Table](../../../images/private-route.png)`

### 2. Setting up Security Groups (Firewalls)
Instead of traditional IP blocking, Cloud architecture allows blocking by Security Groups (SG).
*   **Create Lambda-SG:** Attached to Lambda functions. Leave Inbound empty (no incoming connections accepted). Allow all for Outbound to make external calls.
*   **Create Database-SG:** Attached to RDS and ElastiCache. For Inbound, only open ports `3306` (MySQL) and `6379` (Redis). The key point: **In the Source column, do not enter an IP address, but enter the ID of the Lambda-SG**.

This configuration ensures the principle: Only authorized Lambda functions have the right to knock on the Database's door, effectively blocking any risks of system scanning from external sources.