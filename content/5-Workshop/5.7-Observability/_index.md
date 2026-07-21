---
title: "Monitoring & Alerting"
date: 2026-07-20
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

### System Observability

For a distributed serverless multi-service architecture like FinVantage, data flowing through API Gateway, entering Lambda, calling AI services (Textract/Bedrock), and finally saving to RDS makes debugging extremely complex. 

If the system slows down or encounters errors, we cannot simply "SSH into the server to view logs" the traditional way. Instead, we must build comprehensive **Observability** capabilities to collect metrics, traces, and logs.

In this section, we will practice:
1. Collecting and visualizing system logs with Amazon CloudWatch.
2. Tracing the latency of each service using AWS X-Ray.
3. Setting up an automated alerting system via Amazon SNS.