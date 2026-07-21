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

![Figure 5.7.2a. AWS X-Ray Service Map visualizing component node dependencies during ocrInvoice execution.](../../../images/finvantage-xray-service-map.jpg)

---

### 2. Security Audit Logging with AWS CloudTrail

Beyond performance monitoring (CloudWatch) and trace path analysis (X-Ray), a financial platform must store an immutable audit log to record: *"Who performed what action and when on the AWS infrastructure?"*. AWS CloudTrail satisfies this requirement:
*   **Recording API Calls:** CloudTrail automatically logs every API request invoked by IAM users, Lambda execution roles, or other AWS services (e.g., Lambda calling Textract APIs, modifying database configurations, altering S3 bucket policies).
*   **Security & Tamper Resistance:** Audit logs are securely persisted inside an encrypted S3 Bucket with Object Lock enabled, preventing unauthorized deletion or modification after a security incident.

---

![Figure 5.7.2b. AWS CloudTrail Event History logging s3.amazonaws.com management API requests.](../../../images/finvantage-cloudtrail-events.jpg)  
> Caption: "Figure 5.7.2b. Automated API audit logging in AWS CloudTrail Event history (Illustrative Example)."

---

### Common Troubleshooting with X-Ray
*   **Issue: `Missing X-Ray daemon connection / Error sending segment`**
    *   *Cause:* Lambda has Active Tracing enabled, but its IAM execution role lacks `xray:PutTraceSegments` write permissions.
    *   *Resolution:* Attach the AWS managed policy `AWSXrayWriteOnlyAccess` to the Lambda execution role.

### Summary
AWS X-Ray and CloudTrail elevate system operational confidence and security compliance to enterprise standards.
