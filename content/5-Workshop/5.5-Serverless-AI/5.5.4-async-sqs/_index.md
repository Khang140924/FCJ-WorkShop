---
title: "Amazon SQS and Worker Lambda"
date: 2026-07-20
weight: 4
chapter: false
pre: " <b> 5.5.4. </b> "
---

### Amazon SQS and Worker Lambda (Proposed Extension Architecture)

> ⚠️ **IMPORTANT NOTE:**  
> **Proposed Architectural Extension (Not deployed in current production).**  
> To optimize development resources and operational overhead during testing, FinVantage processes AI requests synchronously via API calls. The architecture below presents an optional asynchronous queue extension for high-traffic scalability.

---

### Objective
This page introduces **asynchronous processing** using **Amazon SQS** and **Worker Lambda** to decouple heavy AI workloads from synchronous user requests.

### Overview
Invoking Amazon Textract OCR and passing raw text to Amazon Bedrock LLMs can take 3 to 10 seconds. In high-traffic production environments, forcing users to wait for synchronous HTTP API responses can cause browser timeouts or degraded user experience. Message queues resolve this bottleneck.

### Component Roles in Proposed Asynchronous Pattern

*   **Amazon SQS (Simple Queue Service):** Serves as an intermediary message queue. When a user uploads a receipt, the API Lambda records metadata, pushes a task message (containing receipt ID and S3 URI) to SQS, and returns `202 Accepted` immediately. The UI displays an `Analyzing` state while freeing the client.
*   **Worker Lambda:** Background function triggered automatically by SQS. The worker polls messages from SQS and asynchronously executes heavy workloads: Textract OCR → Bedrock LLM Analysis → PostgreSQL Persistence.
*   **Amazon SQS Dead Letter Queue (DLQ):** Secondary queue holding failed messages after repeated processing failures (e.g., corrupted image or network outages). If Worker Lambda fails 3 retries (Retry Limit), the message routes to DLQ for administrator inspection without blocking main queues.
*   **Visibility Timeout:** Period during which SQS hides a message after retrieval by a Worker Lambda, preventing duplicate processing by concurrent worker instances.

---

![Figure 5.5.4. Textract OCR text extraction processing in FinVantage.](../../../images/06-01-textract-processing.jpg)

---

### Common Asynchronous Queue Pitfalls
*   **Issue: `Duplicate processing of invoices`**
    *   *Cause:* Processing duration of Textract + Bedrock exceeds SQS **Visibility Timeout**, leading SQS to consider the message unacknowledged and re-exposing it to concurrent workers.
    *   *Resolution:* Increase SQS Queue Visibility Timeout to at least 6 times the Worker Lambda timeout (e.g., 5 minutes).

### Summary
Asynchronous queuing patterns using SQS and DLQ enable FinVantage to scale seamlessly for high-concurrency workloads without crashing backend services.

---

### Report Screenshot Checklist
1.  `06-01-textract-processing.png` - Textract OCR extraction progress.