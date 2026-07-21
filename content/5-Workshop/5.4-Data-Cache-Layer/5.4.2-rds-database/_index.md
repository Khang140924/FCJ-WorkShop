---
title: "Database Deployment (Amazon RDS)"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

### 1. Creating a Subnet Group for the Database
To ensure Amazon RDS resides entirely within the internal network, we need to combine the 2 Private Subnets (created in the previous section) into a single group.
*   Navigate to the RDS Console > **Subnet groups**.
*   Create a new group, select the project's VPC, and add the 2 Private Subnets into it.

### 2. Provisioning Amazon RDS (MySQL)
Proceed to create a Database Instance to store financial data.
*   **Engine:** MySQL.
*   **Deployment Option:** Select **Multi-AZ DB Instance**. This feature allows RDS to automatically create a standby replica (Standby) in a second Availability Zone. If the primary server crashes, the system will automatically failover to the standby server without any data loss.
*   **Connectivity:** 
    *   Virtual Private Cloud (VPC): Select the project's VPC.
    *   Subnet group: Select the group created in step 1.
    *   Public access: **No** (Crucial for security).
    *   VPC security group: Select `Database-SG` (Only allows Inbound traffic from Lambda).

> 📸 **[IMAGE INSERTION REMINDER]:** Take a screenshot of the RDS details (**Connectivity & security** tab), highlighting the text "Publicly accessible: No" and "Multi-AZ: Yes" in red.
> *Markdown code:* `![Amazon RDS Configuration](../../../images/rds-multi-az.png)`