---
title: "Serverless and Artificial Intelligence"
date: 2026-07-20
weight: 5
chapter: true
pre: " <b> 5.5. </b> "
---

### The Heart of FinVantage: Serverless & Artificial Intelligence (AI)

Welcome! Having constructed secure VPC networking and database persistence layers in preceding chapters, we now enter the application logic tier of FinVantage – implementing business workflows and AI capabilities for automated receipt processing.

FinVantage is built completely on a **Serverless** cloud architecture. Instead of paying for traditional 24/7 EC2 instances that waste idle capacity, we leverage event-driven AWS compute services. The platform auto-scales dynamically with incoming request volume, charging only for active execution milliseconds.

---

### Core Layer Components

1.  **Amazon API Gateway:** The front-door proxy accepting inbound HTTP requests from the React Frontend and routing them to appropriate Lambda functions.
2.  **AWS Lambda (Node.js 24):** Hosts all backend microservice handlers (Authentication, Invoice CRUD, AI Analysis, Budget Management).
3.  **Amazon Textract:** Specialized AI service extracting raw document OCR text from uploaded receipt images and PDFs.
4.  **Amazon Bedrock (Claude 3.5 Sonnet):** Advanced LLM foundation model performing intelligent spending categorization and financial advice generation.

Notably, FinVantage implements a real-world enterprise architecture pattern: **Cross-account Bedrock Invoke**. The Lambda backend in the primary account assumes an IAM role (`FinVantageBedrockInvokeRole`) in a separate AWS account hosting Bedrock models, centralizing AI governance.

---

### Chapter Roadmap

We will verify and explore implementation across 4 dedicated pages:

1.  **Lesson 5.5.1. Amazon API Gateway:** Verify API Routes, `prod` deployment stage, and CORS settings.
2.  **Lesson 5.5.2. Function-Based Lambda Design:** Deep-dive into execution properties, environment variables, VPC connectivity, and IAM Roles for each microservice Lambda.
3.  **Lesson 5.5.3. AI Integration (Textract & Bedrock):** Inspect Textract OCR API calls, cross-account IAM role configuration for Bedrock, and CloudWatch execution logs.
4.  **Lesson 5.5.4. Amazon SQS and Worker Lambda (Extension):** Explore architectural designs leveraging SQS Queues and DLQs for asynchronous high-volume processing.

Let's begin with API Gateway in the next lesson!
