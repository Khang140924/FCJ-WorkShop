---
title: "Content Delivery (CloudFront)"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.6.2. </b> "
---

### Global Content Delivery Network (CDN)

Since the S3 Bucket containing the Frontend has its Public Access blocked, users cannot access it directly. We use **Amazon CloudFront** to act as the bridging proxy for content delivery.

#### 1. Provisioning CloudFront Distribution
CloudFront caches the web interface from S3 and stores it across hundreds of Edge Locations globally. Consequently, users in Vietnam or the US can load the FinVantage page in milliseconds.

#### 2. Securing the Origin with OAC (Origin Access Control)
This is a core security technique to connect CloudFront with the secured S3 bucket:
*   In the Origin configuration of CloudFront, set up **Origin Access Control (OAC)**.
*   CloudFront will provide a JSON Policy snippet. Copy this Policy snippet and paste it into the **Bucket Policy** of the S3 bucket.
*   **Significance:** The S3 Bucket will now exclusively open its doors to traffic coming from this CloudFront distribution. All other requests (including copying the S3 link directly into a browser) will be rejected with a `403 Access Denied` error.

> 📸 **[IMAGE INSERTION REMINDER]:** Take a screenshot of the CloudFront Origin configuration interface, highlighting the **Origin access control settings (recommended)** option being enabled.
> *Markdown code:* `![CloudFront OAC Configuration](../../../images/cloudfront-oac.png)`