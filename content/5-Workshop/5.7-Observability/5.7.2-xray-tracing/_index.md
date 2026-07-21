---
title: "AWS X-Ray and CloudTrail"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.7.2. </b> "
---

### AWS X-Ray and CloudTrail (Proposed Security & Tracing Extension)

> ⚠️ **IMPORTANT NOTE:**  
> **Proposed Architectural Extension (Not deployed in current production).**  
> To simplify configuration overhead and conserve storage capacity on lab accounts, deep tracing via AWS X-Ray and audit logging via AWS CloudTrail are omitted in the current test deployment. This section describes theoretical design patterns for enterprise operations.

---

### Objective
This page outlines theoretical design principles for **AWS X-Ray** and **AWS CloudTrail** in performing security auditing, latency bottleneck analysis, and distributed request tracing across **FinVantage**.

---

### 1. Distributed Tracing with AWS X-Ray

In a serverless microservices architecture, an uploaded receipt triggers requests traversing multiple services: Browser → API Gateway → `importInvoice` Lambda → S3 → `ocrInvoice` Lambda → Textract → Redis → `analyzeInvoice` Lambda → Bedrock → RDS Proxy → PostgreSQL. If an API call suffers latency spikes, pin-pointing the bottleneck requires distributed tracing.

AWS X-Ray resolves distributed tracing challenges:
*   **Active Tracing:** When enabled on API Gateway and Lambda, X-Ray injects a unique `X-Amzn-Trace-Id` header into HTTP requests, propagating context across AWS boundaries.
*   **Service Map:** Automatically visualizes FinVantage service topology nodes, rendering call relationships and response latencies visually.
*   **Traces Timeline (Gantt Chart):** Displays granular timing breakdowns for each execution segment. Helps administrators isolate whether latency originates from PostgreSQL queries, Textract OCR scanning, or Claude 3.5 Sonnet Bedrock inference.

---

> 📸 PHOTO TO ADD  
> Screenshot: Sample AWS X-Ray Service Map diagram showing request flow across API Gateway, Lambda, S3, and Bedrock nodes.  
> Suggested name: `finvantage-xray-service-map.png`  
> Caption: "Figure 5.7.2a. AWS X-Ray visual Service Map topology (Illustrative Example)."

---

### 2. Security Audit Logging with AWS CloudTrail

While CloudWatch monitors code performance and X-Ray traces request flows, financial platforms require immutable audit logs answering: *"Who performed what API action, and when?"*. AWS CloudTrail satisfies audit logging requirements:
*   **API Activity Recording:** CloudTrail logs all API calls made by IAM users, Lambda execution roles, or AWS services (e.g., Lambda invoking Textract, modifying database configurations, or updating S3 bucket policies).
*   **Immutable Storage:** CloudTrail audit trails are stored securely in an encrypted S3 Bucket configured with Object Lock to prevent tamper attempts or log deletion.

---

> 📸 PHOTO TO ADD  
> Screenshot: AWS CloudTrail Console Event history page displaying recorded API events (GetBucketPolicy, AssumeRole, InvokeModel).  
> Suggested name: `finvantage-cloudtrail-events.png`  
> Caption: "Figure 5.7.2b. Automated API audit logging in AWS CloudTrail Event history (Illustrative Example)."

---

### Common Troubleshooting with X-Ray
*   **Issue: `Missing X-Ray daemon connection / Error sending segment`**
    *   *Cause:* Lambda has Active Tracing enabled, but its IAM execution role lacks `xray:PutTraceSegments` write permissions.
    *   *Resolution:* Attach the AWS managed policy `AWSXrayWriteOnlyAccess` to the Lambda execution role.

### Summary
AWS X-Ray and CloudTrail elevate system operational confidence and security compliance to enterprise standards.

---

### Report Screenshot Checklist
1.  `finvantage-xray-service-map.png` - AWS X-Ray visual Service Map diagram.
2.  `finvantage-cloudtrail-events.png` - AWS CloudTrail API event history.