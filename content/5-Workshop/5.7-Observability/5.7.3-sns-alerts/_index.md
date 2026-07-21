---
title: "Automated Alerts (Amazon SNS)"
date: 2026-07-21
weight: 3
chapter: false
pre: " <b> 5.7.3. </b> "
---

### Setting up Alerts with Amazon SNS

Instead of staring at the CloudWatch screen 24/7, we use **Amazon SNS (Simple Notification Service)** combined with CloudWatch Alarms to let the system automatically sound the alarm when an incident occurs.

#### 1. Creating an Alert Topic
*   Provision an SNS Topic named `FinVantage-System-Alerts`.
*   Create a **Subscription**: Register a personal email (or a Telegram/Slack webhook) to this Topic to receive notifications.

#### 2. Attaching CloudWatch Alarms
We set up two classic monitoring alarms:
1.  **Technical Alert:** Set an Alarm if the `Worker Lambda` processing AI encounters more than 5 Errors within 5 minutes. If triggered, the Alarm pushes a message to the SNS Topic to email the DevOps team.
2.  **Billing Alert:** A unique characteristic of Serverless is paying per request volume. To prevent end-of-month AWS bills from skyrocketing due to attacks or coding bugs (infinite loops), we set an alarm as soon as the estimated budget exceeds `$10`.

> 📸 **[IMAGE INSERTION REMINDER]:** Take a screenshot of an alert email from AWS sent to your inbox, OR the CloudWatch interface showing a red Alarm state (In alarm).
> *Markdown code:* `![SNS and Email Alerts](../../../images/sns-email-alert.png)`