---
title: "Raw File Storage (Amazon S3)"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

### 1. Provisioning an S3 Bucket for Invoices
We create a bucket named `finvantage-raw-invoices-[random-id]` to act as a landing zone for invoice files coming from the `Import Lambda`.
*   **Security:** Enable the **Block all public access** feature. No one from the Internet can directly access these files without a valid IAM Role.
*   **Encryption:** Enable Server-Side Encryption with the SSE-S3 standard to protect sensitive data at rest.

### 2. Configuring Event Notifications (Triggering Events)
Serverless architecture is Event-driven. When a new invoice file is successfully uploaded to S3, S3 will automatically emit an Event to wake up the `Parse & Categorize Lambda` function or `Textract` to start working.
*   Navigate to the **Properties** tab of the S3 Bucket.
*   Create an Event notification: Capture the `s3:ObjectCreated:Put` event.
*   Destination: Select the Lambda function responsible for handling OCR.

> 📸 **[IMAGE INSERTION REMINDER]:** Take a screenshot of the **Event notifications** setup in S3, showing the S3 Bucket routing the event flow to a Lambda function.
> *Markdown code:* `![S3 Event Notification](../../../images/s3-event-notification.png)`