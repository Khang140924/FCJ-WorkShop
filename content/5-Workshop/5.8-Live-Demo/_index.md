---
title: "Live Testing and Evaluation"
date: 2026-07-20
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

### Live Testing and Architectural Evaluation

### Objective
This page guides you through executing a complete end-to-end live testing scenario on the running **FinVantage** platform: from Cognito Hosted UI authentication, receipt upload, Textract OCR extraction, and Bedrock AI analysis, to verifying database records in PostgreSQL and rendering spending summary dashboards.

---

### Live Demo Scenario

**Step 1: Access Web Application & Log In**
*   Open your browser and navigate to: `https://main.dp5hgt6k889yu.amplifyapp.com/?v=3`.
*   Click **Sign In**. The browser redirects to the AWS-hosted **Cognito Hosted UI** login page.
*   Enter registered email credentials → Log in successfully → The browser redirects back to the main FinVantage Dashboard.

**Step 2: Upload Real Receipt File**
*   Click **Import Invoice** (or Upload Receipt button).
*   Select a receipt image from your machine (e.g., supermarket receipt, coffee shop bill, utility invoice).
*   The application receives metadata, acquires a secure S3 presigned URL, and uploads the image directly to S3.
*   The UI displays real-time status: `Uploading...` → `Processing OCR...`.

**Step 3: Observe AI Processing Pipeline**
*   Behind the scenes, the automated event pipeline executes:
    1.  Receipt image lands in S3 bucket `finvantage-invoices-hieu-2026-395840094907` → S3 event fires `ocrInvoice` Lambda.
    2.  `ocrInvoice` Lambda invokes Amazon Textract `AnalyzeExpense` API to extract raw text → Result cached in Valkey/Redis.
    3.  `analyzeInvoice` Lambda reads text from Redis → Assumes Bedrock role → Calls Claude 3.5 Sonnet to categorize spending → Saves structured JSON into PostgreSQL via RDS Proxy.
*   The UI updates status to `Analyzed` upon completion.

**Step 4: Verify Results on UI**
*   Open the invoice detail page → Verify fields parsed accurately by AI: Vendor Name, Total Amount, Date, Spending Category, and AI Financial Advice.
---

### Live System Demonstration Video

<div align="center">
  <video width="100%" controls preload="metadata">
    <source src="../../images/demo.mp4" type="video/mp4">
    Your browser does not support the HTML5 video player.
  </video>
  <p><i>Video 5.8: End-to-end live demonstration of the FinVantage platform.</i></p>
</div>

---

![Figure 5.8a. Receipt details parsed and categorized by AI on FinVantage web interface.](../../images/finvantage-live-demo-result.jpg)

---

![Figure 5.8b. Executive spending summary dashboard rendering AI-processed financial data.](../../images/finvantage-dashboard-summary.jpg)

---

### Key Architectural Learnings & Reflection

Deploying a Serverless AI architecture yields valuable engineering insights:

*   **Cold Starts & VPC Attachment:** Lambda functions placed inside VPC Private Subnets incur initial connection latency for ENI attachment. Solution: Utilizing ElastiCache Valkey/Redis as a high-speed state cache mitigates heavy database connections.
*   **RDS Proxy Connection Pooling:** Direct Lambda connections into PostgreSQL under high concurrency cause connection pool exhaustion. RDS Proxy multiplexes database connections, keeping PostgreSQL healthy under traffic spikes.
*   **Cross-Account Bedrock Governance:** Invoking Bedrock across AWS accounts via `sts:AssumeRole` decouples AI model governance from infrastructure accounts, simplifying cost management and adhering to Least Privilege.
*   **Textract AnalyzeExpense vs AnalyzeDocument:** Utilizing the specialized `AnalyzeExpense` API yields far higher parsing accuracy for receipts than multi-purpose `AnalyzeDocument` APIs, as AWS ML models are pre-trained specifically on financial invoices.
*   **Amplify Hosting & Rewrites:** Configuring Amplify Rewrites and Redirects to reverse-proxy `/auth` endpoints to API Gateway is critical for Cognito Hosted UI callbacks to work seamlessly without custom domain overhead.

### Summary
The FinVantage platform operates end-to-end: from secure authentication and receipt upload to automated AI extraction and financial dashboard visualization. Serverless AI architectures demonstrate exceptional elasticity, cost efficiency, and business workflow automation.
