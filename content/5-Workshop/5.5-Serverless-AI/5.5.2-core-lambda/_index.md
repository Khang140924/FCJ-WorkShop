---
title: "Function-Based Lambda Design"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.5.2. </b> "
---

### Function-Based Lambda Design

### Objective
This page guides you on accessing the **AWS Lambda Console** to inspect execution settings (function names, Node.js 24 runtime, Memory allocation, Timeout limits), VPC network attachment, environment variables, and IAM execution roles for FinVantage microservice Lambda functions.

### Overview
AWS Lambda is the core compute engine of the FinVantage backend. The architecture follows microservice design patterns, splitting business logic into decoupled functions to optimize execution performance, scale automatically, and isolate runtime errors.

### Core Business Lambda Functions in FinVantage

| Lambda Production Function Name | Event Trigger | Core Business Responsibility | Connected Services |
| :--- | :--- | :--- | :--- |
| **`finvantage-prod-authApi`** | API Gateway | Handles Cognito login callback, generates sessions, and caches tokens in Valkey/Redis. | Cognito, Valkey |
| **`finvantage-prod-importInvoice`** | API Gateway | Receives receipt metadata, creates `invoiceId`, `cacheKey`, and generates S3 presigned URLs for client upload. | Amazon S3 |
| **`finvantage-prod-ocrInvoice`** | S3 ObjectCreated | Automatically triggered upon S3 receipt upload. Invokes Textract OCR and caches raw text output. | Textract, Valkey |
| **`finvantage-prod-analyzeInvoice`** | API Gateway / Web | Reads OCR text from Redis, assumes Bedrock role to perform AI analysis, and saves results to PostgreSQL. | Bedrock, RDS Proxy |
| **CRUD Invoice Functions** | API Gateway | Manages invoice lifecycles: `create`, `list`, `search`, `get`, `update`, `delete`. | RDS Proxy |
| **`finvantage-prod-budgetsApi`** | API Gateway | Manages monthly budget limits, calculates current spending totals, and triggers alerts. | RDS Proxy |
| **`finvantage-prod-dashboardSummary`** | API Gateway | Aggregates category spending summaries and daily expense graphs for users. | RDS Proxy |
| **`finvantage-prod-profileApi`** | API Gateway | Syncs user profiles from Cognito and manages user preferences (language/theme). | RDS Proxy |

---

### Verification Steps on AWS Console

**Step 1:** Log in to AWS Console → Search `Lambda` → Select **Lambda** → Click **Functions** on the left menu.

**Step 2:** Select a business Lambda function (e.g., `finvantage-prod-analyzeInvoice`).

**Step 3:** Under **Code** or **General configuration** under the **Configuration** tab, verify:
*   **Runtime:** `Node.js 24.x` (latest JavaScript runtime).
*   **Handler:** `src/handlers/analysisHandler.handler` (Points to handler export in code).
*   **Memory:** Allocated RAM capacity (e.g., 1024 MB).
*   **Timeout:** Maximum execution duration (e.g., 30 seconds or 1 minute).

---

**Step 4:** Open **Configuration** → Select **VPC**:
*   Verify Lambda is attached to the project VPC.
*   **Subnets:** Attached to **2 Private Subnets** for internal network communication.
*   **Security groups:** Linked to **`Lambda-SG`** (Outbound: All Traffic, Inbound: Empty).

---

![Figure 5.5.2a. Lambda VPC configuration showing Private Subnet attachments and LambdaSecurityGroup binding.](../../../images/finvantage-lambda-vpc.jpg)

---

**Step 5:** Select **Environment variables** under the Configuration tab:
*   Verify key parameters are configured (such as `DB_HOST`, `REDIS_URL`, `BEDROCK_ROLE_ARN`, `BEDROCK_MODEL_ID`...).
*   *Security Note:* Avoid taking screenshots of sensitive passwords or access tokens.

---

![Figure 5.5.2b. Configured Lambda environment variables (Part 1 - Cognito, API Gateway, DB Secrets Manager ARN).](../../../images/finvantage-lambda-env-1.jpg)

---

![Figure 5.5.2c. Configured Lambda environment variables (Part 2 - S3 Bucket, Valkey/Redis Cluster URL, RDS Proxy Endpoint).](../../../images/finvantage-lambda-env-2.jpg)

---

**Step 6:** Select **Permissions** under Configuration tab:
*   Verify attached **Execution role**. Contains IAM permissions for CloudWatch logs, S3 access, Textract invocation, and AssumeRole to Bedrock.

---

### Common ESM Bundling Issues with Lambda
During serverless deployment, esbuild bundlers may encounter ECMAScript Module (ESM) resolution issues:
*   **Error: `Dynamic require of "path" is not supported` or `API Gateway 502 Bad Gateway`**
    *   *Cause:* esbuild bundling code to single ESM files struggles with legacy CommonJS dynamic requires.
    *   *Fix:* Add a `banner` snippet to Serverless bundler configuration to shim CommonJS `require`:
        ```javascript
        banner: "import { createRequire } from 'module'; const require = createRequire(import.meta.url);"
        ```
    *   *Note:* Re-deploying fixed Lambda bundles does **not** require re-running database migrations on PostgreSQL.

### Summary
Backend Lambda microservices are configured with Node.js 24 runtime, VPC attachment, and IAM execution roles for FinVantage workload execution.
