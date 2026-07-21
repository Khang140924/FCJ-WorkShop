---
title: "ElastiCache Valkey/Redis"
date: 2026-07-20
weight: 4
chapter: false
pre: " <b> 5.4.4. </b> "
---

### ElastiCache Valkey/Redis

### Objective
This page guides you on accessing **Amazon ElastiCache Console** to verify the operational status of the **Amazon ElastiCache Valkey/Redis** cluster (including primary endpoint address, port, transit encryption, and linked private subnets) for **FinVantage**.

### Overview
Amazon ElastiCache provides an in-memory caching engine delivering sub-millisecond response latencies. FinVantage uses ElastiCache as an intermediate state store to coordinate asynchronous receipt processing pipelines and manage active user sessions.

### Role of Valkey/Redis in FinVantage
Instead of serving purely as a database query cache, Valkey/Redis acts as a real-time state coordinator across receipt processing pipelines:
1.  **Auth Sessions:** Stores active user session data authenticated via Cognito.
2.  **Upload Tracking:** Tracks initial receipt image upload status landing on S3 (`UPLOADED`).
3.  **OCR Cache:** Caches raw text output extracted by Amazon Textract (`OCR_PROCESSING` -> `OCR_COMPLETED`). The AI Analysis Lambda reads OCR text directly from Redis memory rather than re-invoking Textract, saving cost and reducing latency.
4.  **Analysis Status:** Updates AI invoice analysis state (`ANALYZING` -> `ANALYZED`).

---

### Verification Steps on AWS Console

**Step 1:** Log in to AWS Console → Search `ElastiCache` → Select **ElastiCache**.

**Step 2:** From the left menu, select **Redis OSS** or **Valkey** clusters.

**Step 3:** Select the cluster instance (`finvantage-prod-redis`).

**Step 4:** Inspect the cluster detail page:
*   **Status:** Verify operational status shows `Available` or `Active`.
*   **Primary endpoint:** Note the primary endpoint address.
*   **Port:** Confirm port is set to `6379` (default Redis/Valkey port).
*   **Subnet group:** Linked to VPC Private Subnets.
*   **Security groups:** Attached to `Valkey-SG` (or `Database-SG`).
*   **Encryption in transit:** Verify status shows `Enabled` (Encrypts data transferred between Lambda and cluster).

---

![Figure 5.4.4. Amazon ElastiCache Valkey/Redis cluster configuration details for FinVantage.](../../../images/finvantage-elasticache.jpg)

---

> ⚠️ **Security Warning:** Never expose auth tokens or passwords in documentation or screenshots.

### Integration with Other Services
Backend Lambda functions read the `REDIS_URL` environment variable (formatted as `redis://<endpoint>:6379` or `rediss://...` when TLS is enabled) to instantiate Node.js Redis client connections.

### Common Troubleshooting
*   **Issue: `Redis connection timeout / Network unreachable`**
    *   *Cause:* `Valkey-SG` Security Group lacks inbound rule opening port `6379` to `Lambda-SG`, or Lambda is executing outside the VPC.
    *   *Resolution:* Check Valkey Security Group rules, allowing Inbound port `6379` from `Lambda-SG`.

### Summary
The Valkey/Redis cluster is active, providing high-speed state caching for automated receipt processing workflows.

---

### Report Screenshot Checklist
1.  `finvantage-elasticache.png` - ElastiCache Valkey/Redis cluster details, Endpoint, and Port.