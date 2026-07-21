---
title: "Cache Layer (ElastiCache Redis)"
date: 2026-07-20
weight: 4
chapter: false
pre: " <b> 5.4.4. </b> "
---

### Accelerating Data Retrieval with ElastiCache

In expense management systems, users constantly refreshing the page to view their total monthly spending generates numerous expensive queries to the RDS.

We use **Amazon ElastiCache (Redis)** as an in-memory cache layer to reduce the load on the RDS and minimize latency.
*   **Cluster Provisioning:** Create a Redis cluster completely contained within the project's Private Subnets. Attach the `Database-SG` to control access permissions.
*   **Caching Strategy (Workflow):**
    1. When a user calls the API to view statistics, the `Analysis Lambda` function queries Redis first.
    2. If the data exists (Cache Hit), it is returned immediately (usually under 1ms).
    3. If it does not exist (Cache Miss), the Lambda will route through the RDS Proxy to retrieve data from MySQL, then write the result back to Redis with a specific Time-To-Live (TTL), and finally return it to the user.

> 📸 **[IMAGE INSERTION REMINDER]:** Take a screenshot of the Amazon ElastiCache cluster management interface showing the "Available" state, displaying the Endpoint (connection string) used for Lambda configuration.
> *Markdown code:* `![Amazon ElastiCache Redis](../../../images/elasticache-redis.png)`