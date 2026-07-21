---
title: "Core Logic (AWS Lambda)"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.5.2. </b> "
---

### Deploying Serverless Processing Functions

Following the Microservices principle, instead of writing a massive monolithic block of code, we break down the logic into independent **AWS Lambda** functions, each taking on a single responsibility (Single Responsibility).

#### 1. Import Lambda & Payment Lambda
*   **Payment Lambda:** Handles transactions manually entered by users. It connects via RDS Proxy to write data directly into MySQL.
*   **Import Lambda:** Receives data streams (Base64 or binary) from API Gateway. Its task is lightweight: uploading invoice files to the S3 Bucket (Raw Files).

#### 2. VPC Configuration for Lambda
This is a critically important step for Lambda to be able to see the Database:
*   In the Lambda function configuration, enable the **VPC** feature.
*   Assign the Lambda function to the **2 Private Subnets** created in Section 5.3.
*   Attach the **Lambda-SG** (Security Group) to allow outbound calls and access to RDS/ElastiCache.

> 📸 **[IMAGE INSERTION REMINDER]:** Take a screenshot of the **VPC** configuration section inside a Lambda function's configuration interface (e.g., `Payment Lambda`), clearly showing the assigned Subnets and Security Group.
> *Markdown code:* `![Lambda VPC Configuration](../../../images/lambda-vpc-config.png)`