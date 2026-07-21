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

> 📸 PHOTO TO ADD  
> Screenshot: Confirmation email dispatched by AWS SNS containing "Confirm subscription" link.  
> Suggested name: `finvantage-sns-subscription-email.png`  
> Caption: "Figure 5.7.3a. AWS SNS automated email subscription confirmation (Illustrative Example)."

---

#### 2. Configure CloudWatch Alarms Triggering SNS

Configure two critical monitoring alarms:

*   **Operational Error Alarm (Technical Alarm):**
    *   *Metric:* `AWS/Lambda` > `Errors` on core functions (`analyzeInvoice` or `ocrInvoice`).
    *   *Threshold:* Fires if error count exceeds `5` errors within a `5-minute` period.
    *   *Action:* Upon transitioning to **In Alarm** (Red), posts alert details to the SNS Topic to dispatch notification emails.
*   **Billing Cap Alarm (Cost Alarm):**
    *   *Metric:* `AWS/Billing` > `EstimatedCharges`.
    *   *Threshold:* Estimated monthly charges breach `$10` USD.
    *   *Purpose:* Prevents unexpected cloud bill spikes resulting from accidental infinite code loops or API spam attacks.

---

> 📸 PHOTO TO ADD  
> Screenshot: AWS Console → CloudWatch → Alarms page showing alarm states (OK / In Alarm).  
> Suggested name: `finvantage-cloudwatch-alarms.png`  
> Caption: "Figure 5.7.3b. CloudWatch Alarms management dashboard showing active alarm configurations (Illustrative Example)."

---

### Common Troubleshooting
*   **Issue: `Alarm stays in INSUFFICIENT_DATA state`**
    *   *Cause:* Insufficient metric data points collected during the evaluation window (e.g., zero Lambda errors generated). Normal behavior for newly created alarms.
    *   *Resolution:* Generate test traffic or verify evaluation period settings.

### Summary
Combining CloudWatch Alarms and Amazon SNS Alerts ensures rapid incident response, protecting FinVantage infrastructure availability.

---

### Report Screenshot Checklist
1.  `finvantage-sns-subscription-email.png` - AWS SNS email subscription confirmation.
2.  `finvantage-cloudwatch-alarms.png` - CloudWatch Alarms dashboard interface.