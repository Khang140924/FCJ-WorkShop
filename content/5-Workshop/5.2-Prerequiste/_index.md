---
title: "Prerequisites"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

### Environment Preparation & Permissions (Prerequisites)

Before starting to build the network architecture and write code for FinVantage, we need to set up the foundational environment and configure strict security permissions (Identity and Access Management - IAM) following the **Least Privilege** principle.

#### 1. AWS Environment
*   **Region:** Ensure all resources (VPC, Lambda, Bedrock...) are deployed in the same Region (e.g., `us-east-1` or `ap-southeast-1`) to optimize latency and avoid cross-region data transfer fees.

#### 2. Enabling Artificial Intelligence (Amazon Bedrock Model Access)
Amazon Bedrock does not automatically unlock Large Language Models (LLMs). For the `Analysis Lambda` function to call the AI to analyze spending habits, you need to request access to the models (e.g., Anthropic Claude 3 or Amazon Titan).
*   Navigate to the **Amazon Bedrock** console > **Model access**.
*   Submit a request (Request model access) for your chosen models and wait for AWS approval (usually takes a few minutes).

> 📸 **[IMAGE INSERTION REMINDER]:** Please take a screenshot of the **Model access** interface in Amazon Bedrock, showing the "Access granted" status (in green) for the AI model you requested.
> *Markdown code:* `![Enabling Amazon Bedrock Model](../../images/bedrock-model-access.png)`

#### 3. Setting up IAM Roles for Serverless Architecture
In a Serverless architecture, AWS Lambda does not inherently have access to RDS or S3. We need to create specific IAM Roles:
*   **Core-Lambda-Role:** For logic processing functions (`Payment Lambda`, `Worker Lambda`). This role requires the `AWSLambdaVPCAccessExecutionRole` policy so Lambda can enter the Private Subnet to communicate with RDS and ElastiCache, plus permissions to read/write messages to Amazon SQS.
*   **AI-Processing-Role:** For `Import Lambda` and `Parse & Categorize Lambda`. Besides VPC access, this Role must be attached with the `AmazonTextractFullAccess` policy, read/write permissions for S3 files (`s3:PutObject`, `s3:GetObject`), and permission to invoke Bedrock APIs (`bedrock:InvokeModel`).

> *Markdown code:* ![Setting up IAM Roles for Lambda](../../images/iam-roles-lambda.png)