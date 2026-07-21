---
title: "Data & Cache Layer"
date: 2026-07-20
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

### Distributed Data Layer Design

In the FinVantage architecture, data storage and retrieval are clearly separated based on the characteristics of each data type to optimize cost and performance. The system utilizes three main storage mechanisms:

1.  **Object Storage:** Uses Amazon S3 to receive and store original invoice files (images, PDFs) uploaded by users.
2.  **Relational Database:** Uses Amazon RDS (MySQL) as the Single Source of Truth to store tightly structured transaction information, identities, and spending categories.
3.  **In-memory Cache:** Uses Amazon ElastiCache (Redis) to accelerate retrieval speeds for frequently called financial analysis reports.

Specifically, to solve the Connection Pool Exhaustion problem—a classic "pain point" when combining AWS Lambda with traditional databases—we will deploy an additional component, **Amazon RDS Proxy**.