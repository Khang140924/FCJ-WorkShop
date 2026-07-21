---
title: "Observability and System Monitoring"
date: 2026-07-20
weight: 7
chapter: true
pre: " <b> 5.7. </b> "
---

### System Monitoring and Observability

Welcome! For a distributed Serverless application like FinVantage, user requests traverse API Gateway, trigger Lambda microservices, invoke external AI APIs (Textract/Bedrock), and persist records in RDS Proxy and PostgreSQL. If any component experiences failures or latency degradation, identifying root causes requires unified telemetry.

Because there are no traditional 24/7 EC2 servers to SSH into, we establish a centralized **Observability** framework built upon 3 primary pillars: Metrics (system performance data), Logs (runtime event logs), and Traces (request execution flow).

---

### Chapter Roadmap

We will explore implementation across 3 detailed lessons:

1.  **Lesson 5.7.1. Amazon CloudWatch:** Practical logging and metric collection service. Learn how to query CloudWatch Logs for Lambda microservices and construct visual CloudWatch Dashboards monitoring API traffic.
2.  **Lesson 5.7.2. AWS X-Ray and CloudTrail (Proposed Extension):** Explore distributed tracing solutions for request path visualization and account-wide API audit logging.
3.  **Lesson 5.7.3. Automated Alerts via Amazon SNS (Proposed Extension):** Explore CloudWatch Alarms for metric threshold monitoring and automated email notification routing via Amazon SNS topics.

Let's begin with Amazon CloudWatch in the next lesson!
