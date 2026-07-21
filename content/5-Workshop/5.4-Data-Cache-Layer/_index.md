---
title: "Data and Cache Layer"
date: 2026-07-20
weight: 4
chapter: true
pre: " <b> 5.4. </b> "
---

### Data & Caching Layer Architecture (Data Layer & Caching)

Welcome! In this chapter, we will walk through configuring and verifying the data persistence and caching layer for the FinVantage system.

To ensure a personal finance management application operates smoothly and securely, the data layer design segregates storage based on specific data characteristics. FinVantage utilizes three core storage engines:

1.  **Object Storage:** Uses **Amazon S3** to ingest and persistently store raw receipt image and PDF files uploaded by users.
2.  **Relational Database:** Uses **Amazon RDS PostgreSQL** as the Single Source of Truth for structured user accounts, financial transactions, monthly budgets, and AI analysis records.
3.  **In-memory Cache:** Uses **Amazon ElastiCache Valkey/Redis** for session management and transient OCR data caching to minimize database load and accelerate response speeds.

---

### RDS Proxy - Solving Serverless Connection Challenges

A classic challenge when combining Serverless Lambda functions with relational databases is **Connection Pool Exhaustion**. When hundreds of concurrent user requests arrive, AWS Lambda auto-scales up to hundreds of parallel function instances. Each instance attempting to open its own database connection can quickly exhaust PostgreSQL connection limits, causing database crashes.

To solve this problem, FinVantage implements **Amazon RDS Proxy** as an intermediate connection pooler that intelligently multiplexes and reuses database connections, ensuring system stability during peak traffic spikes.

---

### Data Layer Roadmap
1.  **Amazon S3 Receipt Storage:** Configure private receipt bucket policies and CORS Rules.
2.  **Amazon RDS PostgreSQL:** Verify secure relational database configuration and parameter groups.
3.  **Amazon RDS Proxy:** Verify connection management and target group health.
4.  **Amazon ElastiCache Valkey/Redis:** Configure Valkey/Redis cluster for session and OCR state caching.
5.  **AWS Secrets Manager:** Securely manage database credentials and secrets.
6.  **Database Migration:** Confirm database schema migration status.

Let's begin with Amazon S3 in the next lesson!
