---
title: "Amazon RDS PostgreSQL"
date: 2026-07-21
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

### Amazon RDS PostgreSQL

### Objective
This page guides you on accessing the **Amazon RDS Console** to verify the configuration of the **Amazon RDS PostgreSQL** relational database (including availability status, port settings, deletion protection, storage encryption, and private VPC isolation) for **FinVantage**.

### Overview
A relational database acts as the single source of truth for structured financial records. For strict security, the PostgreSQL engine is isolated from public Internet access, encrypted at rest, and only accepts internal connections within the VPC environment.

### Service Role in FinVantage
*   **Core Financial Data Store:** Stores user profiles, structured receipt analysis, spending transaction logs, monthly budget caps, and AI advisory recommendations.
*   **DB Subnet Group:** Groups private subnets spanning multiple Availability Zones to host the database engine.
*   **Deletion Protection:** Safety mechanism preventing accidental database deletion via AWS Console.
*   **Storage Encryption:** Encrypts data at rest under physical storage volumes using AWS KMS keys.

---

### Verification Steps on AWS Console

#### 1. Verify DB Subnet Group

**Step 1:** Log in to AWS Console → Search `RDS` → Select **RDS**.

**Step 2:** From the left menu, click **Subnet groups**.

**Step 3:** Select the FinVantage DB Subnet Group (`finvantage-db-subnet-group`). 
*   Verify association with the FinVantage VPC.
*   Ensure the group contains at least 2 Private Subnets spanning 2 Availability Zones (`ap-southeast-1a` and `ap-southeast-1b`) for high availability.

#### 2. Verify Database Instance

**Step 1:** From the left menu, click **Databases**.

**Step 2:** Click the PostgreSQL instance name (`finvantage-prod-db`).

**Step 3:** Under the **Connectivity & security** tab, verify parameters:
*   **Status:** Confirm status displays `Available`.
*   **Endpoint:** Note the database connectivity endpoint address.
*   **Port:** Confirm database port is `5432` (default PostgreSQL port).
*   **Publicly accessible:** Confirm status displays **No**.
*   **Security groups:** Linked correctly to `Database-SG`.

---

![Figure 5.4.2a. Network and security settings (Port 5432, Publicly Accessible: No) for RDS PostgreSQL.](../../../images/finvantage-rds-connectivity.jpg)

---

**Step 4:** Switch to the **Configuration** tab to inspect infrastructure settings:
*   **Engine:** Confirm `PostgreSQL`.
*   **Deletion protection:** Displays `Enabled`.
*   **Encryption:** Storage Encryption displays `Enabled`.

---

> 📸 PHOTO TO ADD  
> Screenshot: AWS Console → RDS → Databases → Select FinVantage DB → Configuration tab.  
> Content: Engine PostgreSQL, Deletion protection Enabled, Encryption Enabled.  
> Suggested name: `finvantage-rds-configuration.png`  
> Caption: "Figure 5.4.2b. Data protection settings (Deletion Protection & Storage Encryption) for RDS PostgreSQL."

---

**Step 5:** Switch to **Maintenance & backups**:
*   Verify automated **Backups** are enabled with retention period set to at least 7 days.

> ⚠️ **Security Warning:** Never share master database passwords or credentials in screenshots or public channels.

### Connectivity with Other Services
Backend Lambda functions do not connect directly to the raw RDS Endpoint. To optimize database connections, Lambda functions connect through **Amazon RDS Proxy**.

### Common Troubleshooting
*   **Issue: `Connection timeout to PostgreSQL`**
    *   *Cause:* `Database-SG` Inbound rules do not permit port `5432` from `Lambda-SG` (or `RDS-Proxy-SG`), or DB is attached to incorrect subnets.
    *   *Resolution:* Check `Database-SG` Inbound rules in VPC, ensuring port `5432` is allowed from `Lambda-SG`.

### Summary
PostgreSQL database is securely configured with storage encryption and VPC isolation, ready for connection pooling via RDS Proxy.

---

### Report Screenshot Checklist
1.  `finvantage-rds-connectivity.png` - Endpoint, port 5432, and connectivity isolation.
2.  `finvantage-rds-configuration.png` - PostgreSQL engine, Encryption, and Deletion Protection settings.