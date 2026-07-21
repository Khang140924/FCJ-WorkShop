---
title: "Logging & Metrics (CloudWatch)"
date: 2026-07-21
weight: 1
chapter: false
pre: " <b> 5.7.1. </b> "
---

### Monitoring with Amazon CloudWatch

By default, all AWS Lambda functions automatically push execution logs (such as `print()` or `console.log()` statements) to **Amazon CloudWatch Logs**.

#### 1. Managing Log Groups
*   Each Lambda function (such as `Parse & Categorize Lambda`) has its own dedicated Log Group. 
*   We can access these logs to inspect the raw JSON data returned by Amazon Textract or Bedrock, making it easy to verify whether the AI is accurately categorizing expenses.

#### 2. Building a Monitoring Dashboard
We create a **CloudWatch Dashboard** to monitor the overall "health" of the FinVantage platform on a single screen. Important metrics to include:
*   **API Gateway:** Request count (Count), Error rate (5XX Errors).
*   **Lambda:** Execution duration (Duration), Invocations, and Throttles.
*   **RDS & ElastiCache:** CPU utilization (CPU Utilization), and Connection count (DatabaseConnections) to verify the effectiveness of the RDS Proxy.

> 📸 **[IMAGE INSERTION REMINDER]:** Take a screenshot of the **CloudWatch Dashboard** interface displaying charts (line charts or number widgets) for the Lambda and RDS metrics you just set up.
> *Markdown code:* `![CloudWatch Dashboard](../../../images/cloudwatch-dashboard.png)`