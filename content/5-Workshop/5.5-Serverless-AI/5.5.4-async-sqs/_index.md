---
title: "Asynchronous Processing (Amazon SQS)"
date: 2026-07-20
weight: 4
chapter: false
pre: " <b> 5.5.4. </b> "
---

### Optimizing Architecture with Queues

The process of Textract analyzing images and Bedrock reasoning logic can take anywhere from 3 to 10 seconds. If users (Frontend) are forced to wait for this process to complete, the application will be perceived as slow (timeout). Therefore, the system is designed using an **Asynchronous Processing** workflow.

#### 1. Using Amazon SQS (Simple Queue Service)
*   Instead of calling the AI directly, the `Import Lambda` simply pushes a "Task" (containing the S3 file path) into an **Amazon SQS** queue, and then immediately returns a response to the Frontend: *"Invoice is being processed!"*.
*   The SQS queue securely holds these tasks, preventing data loss when thousands of users upload concurrently.

#### 2. Worker Lambda & Dead Letter Queue (DLQ)
*   We configure a **Worker Lambda** whose responsibility is to continuously poll SQS. Whenever a new task arrives, it picks it up and invokes the Textract + Bedrock logic chain.
*   **Dead Letter Queue (DLQ):** If an invoice is blurry and the AI cannot read it, causing the Worker Lambda to report errors 3 consecutive times, that task is pushed to the DLQ. Administrators (Dev/Admin) can inspect the DLQ to review these failed invoices without clogging the main processing flow.

> 📸 **[IMAGE INSERTION REMINDER]:** Take a screenshot of the Amazon SQS configuration interface, showing the main queue linked with a Dead-letter queue (DLQ) and Lambda trigger.
> *Markdown code:* `![Amazon SQS Queue Configuration](../../../images/sqs-dlq-config.png)`