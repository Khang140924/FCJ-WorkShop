---
title: "Live Demo & Conclusion"
date: 2026-07-20
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

### System Experience & Architectural Evaluation

#### 1. Live Demo Scenario
The FinVantage system is ready for real-world operation. The test scenario includes:
1. Accessing the application interface via the CloudFront domain and logging in through Amazon Cognito.
2. Uploading a real invoice image (e.g., a supermarket or restaurant receipt).
3. The system displays a "Processing" status. Behind the scenes, the file enters S3, waking up Textract to scan the text, Bedrock to analyze it, and SQS to manage the queue.
4. Refreshing the page to witness the invoice intelligently parsed by AI, automatically labeled as "Food & Beverage", and neatly saved into the MySQL database.

> 📸 **[IMAGE INSERTION REMINDER]:** Take a screenshot of your FinVantage application interface (on the browser) displaying the result of an invoice successfully recognized and categorized by AI.
> *Markdown code:* `![Live Demo Result Interface](../../images/live-demo-result.png)`

#### 2. Lessons Learned (Reflection)
Implementing a Serverless + AI architecture brings valuable technical insights:
*   **The "Cold Start" Pain:** Lambda functions within a Private VPC initially take a few extra seconds to initialize network interfaces (ENIs). Combining Amazon ElastiCache (for caching) and designing asynchronous processing workflows using SQS successfully hid this latency from the user experience.
*   **The Power of RDS Proxy:** Connecting Lambda directly to a traditional RDS is "suicidal" during traffic surges. The presence of RDS Proxy acts as a perfect shock absorber, seamlessly handling connection pool multiplexing.
*   **Operating Artificial Intelligence:** Leveraging Textract (OCR) combined with Bedrock (LLM) is far more efficient than training custom models from scratch, optimizing Time-to-Market.