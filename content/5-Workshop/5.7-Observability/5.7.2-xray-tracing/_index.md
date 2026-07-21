---
title: "System Tracing (AWS X-Ray)"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.7.2. </b> "
---

### Analyzing Latency with AWS X-Ray

When a user uploads an invoice, the request passes through numerous stations. If the API returns a response slowly (e.g., taking up to 5 seconds), we need to know precisely where that time is being wasted.

**AWS X-Ray** is the perfect tool for Serverless architectures.
*   **Activation:** Enable the *Active tracing* feature in the configurations of Amazon API Gateway and the AWS Lambda functions.
*   **Service Map:** X-Ray automatically draws an intuitive connection map of the FinVantage network. You will see requests flow from Client -> API Gateway -> Lambda -> Textract -> Bedrock -> RDS.
*   **Traces:** Provides a Gantt chart breaking down the time spent at each leg of the journey, helping us instantly identify whether the Bedrock AI model is responding slowly or if a MySQL query hasn't been optimized.

> 📸 **[IMAGE INSERTION REMINDER]:** Take a screenshot of the AWS X-Ray **Service Map** (the interconnected service bubbles) or the Traces timeline chart of a request.
> *Markdown code:* `![AWS X-Ray Service Map](../../../images/xray-service-map.png)`