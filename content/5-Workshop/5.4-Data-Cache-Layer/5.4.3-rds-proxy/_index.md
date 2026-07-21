---
title: "Amazon RDS Proxy"
date: 2026-07-21
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

### Amazon RDS Proxy

### Objective
This page guides you on accessing **Amazon RDS Proxy Console** to verify RDS Proxy operational status, proxy endpoint address, TLS encryption settings, Secrets Manager integration, and target group connection health for **FinVantage**.

### Overview
Amazon RDS Proxy acts as a database connection pooler sitting between AWS Lambda backend functions and the RDS PostgreSQL database, protecting the database engine from overload during traffic surges.

### Why Lambda Connects via RDS Proxy Instead of Direct DB Connection
1.  **Connection Pooling:** RDS Proxy maintains a fixed pool of physical database connections to PostgreSQL. When hundreds of concurrent Lambda instances fire, RDS Proxy multiplexes connection requests across the pooled connections.
2.  **Prevents Connection Exhaustion:** PostgreSQL imposes maximum client connection limits. Without RDS Proxy, rapidly scaling Lambda functions would exhaust connection pools, causing database crashes.
3.  **Enhanced Transport Security:** Enforces TLS encrypted transport between Lambda and DB Proxy (`Require TLS`).
4.  **Automatic Failover:** If the primary PostgreSQL instance fails, RDS Proxy seamlessly shifts traffic to the standby replica without requiring Lambda functions to change endpoints or restart.

---

### Verification Steps on AWS Console

**Step 1:** Log in to AWS Console → Search `RDS` → Select **RDS** → Click **Proxies** on the left menu.

**Step 2:** Select the RDS Proxy (`finvantage-prod-proxy`).

**Step 3:** Under the **Summary** tab, verify parameters:
*   **Proxy endpoint:** Note the proxy connection endpoint address.
*   **Status:** Confirm status displays `Available`.
*   **Require TLS:** Confirm setting displays `True` (Enforces TLS encryption).
*   **VPC, Subnets & Security groups:** Ensure Proxy is placed inside the project VPC, Private Subnets, and attached to `RDS-Proxy-SG`.

**Step 4:** Under **Connections**, check **Secrets Manager secrets**:
*   Confirm the attached Secrets Manager secret containing database credentials.

---


**Step 5:** From the Proxy detail menu, select **Targets**:
*   Click the default target group `default`.
*   Verify **Target type** displays `Database` and points to the PostgreSQL Instance.
*   Verify **Target Health** column displays `Available` or `Healthy` (green).

---


### Common Troubleshooting
*   **Issue: `RDS Proxy Target status is Unavailable`**
    *   *Cause:* Username/password stored in Secrets Manager does not match PostgreSQL master credentials, or RDS Proxy IAM role lacks permissions to retrieve secrets.
    *   *Resolution:* Verify secret values in Secrets Manager and confirm RDS Proxy IAM Role has GetSecretValue permissions.

### Summary
RDS Proxy is configured and operational, ensuring Lambda database traffic is safely pooled and routed to PostgreSQL.
