---
title: "Workshop Overview"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

### Introduction to the Real-world Problem

Manual personal finance management often encounters many difficulties: users have to manually enter each invoice, which is prone to errors and time-consuming. Additionally, traditional invoice processing systems are frequently overloaded when data volume spikes at the end of the month.

This workshop will guide you step-by-step on how to build **FinVantage** – a fully Serverless cloud computing solution capable of auto-scaling, automatically extracting invoice data using Artificial Intelligence (AI), and implementing multi-layered security on AWS to thoroughly solve the aforementioned problem.

### Architecture Diagram

The FinVantage system is designed with an Event-driven Architecture, ensuring High Availability and a clear separation of data flows.

`![FinVantage System Architecture Diagram](../../images/finvantage-architecture.png)`

*Figure 5.1.1: FinVantage architecture data flow diagram on AWS.*

### Core Components Explanation

Based on the architecture diagram, the system is divided into the following specific layers:

*   **Entry & Security Layer:** Users send HTTPS requests through AWS WAF (anti-attack) and Amazon CloudFront (accelerated loading speed). The authentication process is managed by Amazon Cognito.
*   **Compute Layer:** Amazon API Gateway acts as the gateway routing API calls to the corresponding AWS Lambda functions (`Payment Lambda`, `Import Lambda`, `Analysis Lambda`).
*   **AI Integration:** When an invoice is uploaded to S3, AWS Lambda calls **Amazon Textract** to perform OCR (Optical Character Recognition) and passes the data to **Amazon Bedrock** for the AI to smartly categorize expenses.
*   **Data Layer:** Safely located within the Private Subnet. Uses Amazon RDS (MySQL) to store user data, combined with Amazon RDS Proxy to avoid connection overload, and Amazon ElastiCache (Redis) for high-speed caching.
*   **Async Processing:** Uses Amazon SQS to create a queue for handling heavy tasks (such as extracting multiple invoices simultaneously) via the `Worker Lambda`, combined with Amazon SNS to send financial alerts.

### Detailed Workshop Roadmap

In the following sections, we will dive sequentially into provisioning the VPC infrastructure, setting up the database, writing code for AI-integrated Lambda functions, and finally configuring the external security layer.