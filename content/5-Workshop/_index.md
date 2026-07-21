---
title: "Workshop"
date: 2026-07-20
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# FINVANTAGE CLOUD INFRASTRUCTURE DEPLOYMENT WORKSHOP

### Overview

In the modern Financial Technology (FinTech) sector, maintaining a stable, highly automated system with strict user data security is vital.

In this Lab, you will get hands-on experience designing, configuring, and deploying the entire AWS cloud infrastructure for the **FinVantage** platform (Personal Finance Management & Automated Alert System). The system is built on a **Serverless** architecture combined with AI, featuring a clear separation of service layers.

Specifically, this practice emphasizes system design thinking and core security by completely hiding the database within an internal network (Private Subnets), utilizing asynchronous processing (Async), and automating data extraction.

### Core Services Utilized

*   **Entry & Security:** AWS WAF, Amazon CloudFront, Amazon S3, Amazon Cognito.
*   **Compute & APIs:** Amazon API Gateway, AWS Lambda.
*   **AI & OCR:** Amazon Textract, Amazon Bedrock.
*   **Database & Cache:** Amazon RDS (MySQL), Amazon RDS Proxy, Amazon ElastiCache.
*   **Async Processing:** Amazon SQS, Amazon SNS.
*   **Observability:** Amazon CloudWatch, AWS X-Ray, AWS CloudTrail.

### Workshop Content

1. [Workshop Overview](5.1-workshop-overview/): Understand the real-world problem and analyze the Solution Architecture Diagram.
2. [Prerequisites](5.2-prerequisite/): Prepare the AWS environment, IAM Roles, and AI model access permissions.
3. [VPC & Networking Infrastructure](5.3-vpc-networking/): Build the internal network framework, configure Public/Private routing, and optimize security.
4. [Data & Cache Layer](5.4-data-cache-layer/): Deploy Amazon RDS, ElastiCache, and configure RDS Proxy.
5. [Serverless & AI Layer](5.5-serverless-ai/): Configure API Gateway, write AWS Lambda logic, and integrate Textract and Bedrock.
6. [Edge & Security Layer](5.6-edge-security/): Distribute static content via S3/CloudFront, set up AWS WAF, and implement Cognito authentication.
7. [Observability & Alerts](5.7-observability/): Monitor with CloudWatch, trace with X-Ray, and set up SNS alerts.
8. [Live Demo & Reflection](5.8-live-demo/): Experience the live system and extract optimization lessons.
9. [Resource Cleanup](5.9-cleanup/): Safely destroy the infrastructure to eliminate unexpected costs.