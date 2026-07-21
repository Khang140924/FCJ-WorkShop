---
title: "Workshop"
date: 2026-07-20
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# FINVANTAGE CLOUD INFRASTRUCTURE DEPLOYMENT HANDS-ON WORKSHOP

### Overview

In modern Financial Technology (FinTech), maintaining a highly stable, automated, and strictly secured system for user data is a vital factor.

In this Lab, you will manually design, configure, and deploy the complete AWS cloud infrastructure for the **FinVantage** platform (Personal Expense Management & Financial Alert System). The system is built using a **Serverless** architecture combined with AI, clearly separating distinct service layers.

In particular, this hands-on workshop emphasizes system design thinking and core security principles by completely hiding the database inside private networks (Private Subnets), processing asynchronously, and automating data extraction.

### Core Services Utilized

*   **Entry & Security:** AWS WAF, Amazon CloudFront, Amazon S3, Amazon Cognito.
*   **Compute & APIs:** Amazon API Gateway, AWS Lambda.
*   **AI & OCR:** Amazon Textract, Amazon Bedrock.
*   **Database & Cache:** Amazon RDS (PostgreSQL), Amazon RDS Proxy, Amazon ElastiCache (Valkey).
*   **Async Processing:** Amazon SQS, Amazon SNS.
*   **Observability:** Amazon CloudWatch, AWS X-Ray, AWS CloudTrail.

### Workshop Agenda

1. [Workshop Overview](5.1-workshop-overview/): Understand real-world business problems and analyze the Solution Architecture Diagram.
2. [Prerequisites](5.2-prerequiste/): Prepare local AWS environment, IAM Roles, and AI model access permissions.
3. [VPC Networking & Security](5.3-vpc-networking/): Build internal network topology, Public/Private routing, and optimize security.
4. [Data & Cache Layer](5.4-data-cache-layer/): Deploy Amazon RDS, ElastiCache, and configure RDS Proxy.
5. [Serverless & AI Integration](5.5-serverless-ai/): Configure API Gateway, author AWS Lambda logic, and integrate Textract & Bedrock.
6. [Edge Security, Authentication & Hosting](5.6-edge-security/): Static hosting via S3/CloudFront, setup AWS WAF, and Cognito authentication.
7. [Observability & System Monitoring](5.7-observability/): Monitor via CloudWatch, trace with X-Ray, and setup SNS alerts.
8. [Live Testing & Evaluation](5.8-live-demo/): Hands-on test of the live system and extract architectural best practices.
9. [Resource Cleanup](5.9-cleanup/): Safely destroy infrastructure to eliminate recurring costs.
