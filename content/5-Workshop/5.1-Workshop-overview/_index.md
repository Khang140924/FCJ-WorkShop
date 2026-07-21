---
title: "Workshop Overview"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

### Real-World Business Problem

Manual personal financial management is prone to errors and time-consuming as users must manually record each receipt. Moreover, traditional receipt processing systems often suffer from server overload when data traffic surges near the end of the month.

This workshop will guide you step-by-step to build **FinVantage** – a completely Serverless cloud solution on AWS capable of auto-scaling, automated receipt data extraction powered by Artificial Intelligence (AI), and multi-layer security to solve these problems.

### Architecture Diagram

The FinVantage platform is designed using an Event-driven Architecture, ensuring High Availability and clean data stream isolation.

![FinVantage Solution Architecture Diagram](../../images/finvantage-architecture.png)

<p align="center"><i>Figure 5.1.1: FinVantage Architectural Dataflow Diagram on AWS.</i></p>

### Key Component Breakdown

Based on the architectural diagram, the platform is divided into specific functional layers:

*   **Entry & Security Layer:** User HTTPS requests pass through AWS WAF (DDoS/Exploit protection) and Amazon CloudFront CDN (speed acceleration). Authentication is centrally managed by Amazon Cognito.
*   **Compute Layer:** Amazon API Gateway serves as the front door routing API calls to corresponding AWS Lambda microservices (`finvantage-prod-importInvoice`, `finvantage-prod-ocrInvoice`, `finvantage-prod-analyzeInvoice`).
*   **AI Integration Layer:** When an invoice is uploaded to S3, AWS Lambda invokes **Amazon Textract** (`AnalyzeExpense` API) for OCR text extraction and passes extracted data to **Amazon Bedrock** (Claude 3.5 Sonnet) for intelligent expense categorization and financial advice generation.
*   **Data & Cache Layer:** Safely placed inside Private Subnets. Amazon RDS (PostgreSQL) stores structured financial records, combined with Amazon RDS Proxy to prevent connection pool exhaustion and Amazon ElastiCache (Valkey/Redis) for high-speed state caching.
*   **Async Processing Layer:** Uses Amazon SQS to queue heavy processing tasks through `Worker Lambda`, paired with Amazon SNS for instant financial budget alerts.

### Detailed Workshop Roadmap

In the upcoming sections, we will dive deep into VPC networking initialization, database setup, Lambda function development integrated with AI, and outer edge security setup.
