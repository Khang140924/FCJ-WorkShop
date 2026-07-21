---
title: "Serverless & Artificial Intelligence Layer"
date: 2026-07-20
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

### The Heart of FinVantage: Serverless & AI

In the previous sections, we built the "warehouse" (Database) and the "fortress" (VPC/Security Groups). Now it is time to build the "workers" (Compute) to handle business logic.

The special feature of FinVantage is its full adoption of a **Serverless** architecture. Instead of renting an EC2 server running 24/7 which causes waste, we use AWS Lambda so that the system only runs (and incurs costs) when actual requests occur.

At the same time, this layer is also where Artificial Intelligence (AI) services are integrated to realize automated invoice extraction and classification features.

In this section, we will practice:
1. Setting up the Amazon API Gateway communication port.
2. Deploying AWS Lambda functions to handle core logic.
3. Integrating AI (Amazon Textract and Amazon Bedrock).
4. Optimizing the system using asynchronous processing architecture (Amazon SQS).