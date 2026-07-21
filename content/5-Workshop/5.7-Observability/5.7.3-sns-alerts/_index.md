---
title: "Amazon SNS Alerts"
date: 2026-07-21
weight: 3
chapter: false
pre: " <b> 5.7.3. </b> "
---

### Amazon SNS Alerts (Proposed Automated Alerting Extension)

> ⚠️ **IMPORTANT NOTE:**  
> **Proposed Architectural Extension (Not deployed in current production).**  
> To simplify configuration and prevent spam notifications during development testing, automated alerting via Amazon SNS and CloudWatch Alarms is omitted in the lab deployment. The section below describes theoretical alerting architecture for production operations.

---

### Objective
This page introduces automated alerting architectures combining **Amazon SNS (Simple Notification Service)** and **CloudWatch Alarms** to dispatch emergency notifications to DevOps teams when system metrics breach threshold limits in **FinVantage**.

### Overview
Rather than requiring operators to manually refresh CloudWatch Dashboards 24/7, active monitoring triggers automated alarms. When application health metrics cross safety thresholds, CloudWatch fires SNS notifications to dispatch alert emails or webhook messages to Slack/Telegram.

---

### Theoretical Alerting System Setup

#### 1. Initialize Amazon SNS Topic

*   **Create SNS Topic:** Provision a Standard notification topic named `FinVantage-System-Alerts`.
*   **Configure Subscription:** 
    *   Create a new Subscription bound to the Topic.
    *   *Protocol:* Select `Email`.
    *   *Endpoint:* Enter the DevOps email address (e.g., `admin@finvantage.com`).
    *   *Confirmation:* AWS dispatches a confirmation email. The subscriber must click **Confirm Subscription** in their inbox to activate notification routing.

---

![Figure 5.7.3a. Amazon SNS topic finvantage-alert-topic details and email subscription configuration.](../../../images/finvantage-sns-subscription-email.jpg)

---

#### 2. Configure CloudWatch Alarms Triggering SNS Notifications

We configure two critical monitoring alarms to protect system health:

*   **Operational Error Alarm (Technical Alarm):**
    *   *Metric:* `AWS/Lambda` > `Errors` for core Lambda functions (`analyzeInvoice`, `ocrInvoice`).
    *   *Trigger Threshold:* Greater than `5` execution errors within a `5-minute` window.
    *   *Action:* Transitions state to **In Alarm** (Red) and publishes a detailed payload to the SNS Topic to alert DevOps.
*   **Budget Overrun Alarm (Billing Alarm):**
    *   *Metric:* `AWS/Billing` > `EstimatedCharges`.
    *   *Trigger Threshold:* Estimated monthly charges exceed `$10` USD.
    *   *Purpose:* Prevents infinite execution loops or DDoS API spamming from creating unexpected cloud billing charges.

---

![Figure 5.7.3b. Active CloudWatch alarm finvantage-lambda-errors monitoring backend function execution failures.](../../../images/finvantage-cloudwatch-alarms.jpg)  
> Caption: "Figure 5.7.3b. CloudWatch Alarms management dashboard showing active alarm configurations (Illustrative Example)."

---

### Common Troubleshooting
*   **Issue: `Alarm stays in INSUFFICIENT_DATA state`**
    *   *Cause:* Insufficient metric data points collected during the evaluation window (e.g., zero Lambda errors generated). Normal behavior for newly created alarms.
    *   *Resolution:* Generate test traffic or verify evaluation period settings.

### Summary
Combining CloudWatch Alarms and Amazon SNS Alerts ensures rapid incident response, protecting FinVantage infrastructure availability.
