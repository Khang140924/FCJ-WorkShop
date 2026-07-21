---
title: "CloudFront Content Delivery Network"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.6.2. </b> "
---

### CloudFront Content Delivery Network (CDN)

### Objective
This page explains the CDN caching mechanisms provided by **Amazon CloudFront** under AWS Amplify Hosting, guiding you on using browser F12 Developer Tools to inspect and verify CloudFront operations for **FinVantage**.

### Overview
Amazon CloudFront is AWS's global Content Delivery Network (CDN). For the static FinVantage frontend, instead of forcing user browsers to fetch static assets directly from S3, CloudFront caches copies across hundreds of global edge locations, serving pages with minimal latency.

### Role of CloudFront in AWS Amplify Hosting
*   **Automated Deployment:** When deploying applications to AWS Amplify Hosting, Amplify automatically provisions a CloudFront Distribution running in the background. You do not need to manually configure CloudFront Distributions, Origin Access Control (OAC), or S3 Bucket Policies. AWS Amplify manages these components seamlessly.
*   **Decoupled Operation:** CloudFront CDN serving Frontend assets combined with API Gateway serving Backend microservices keeps FinVantage online 24/7. Even if your local machine or VS Code editor is powered off, the application runs continuously on the Cloud.
*   **Hard Refreshing:** When deploying new frontend builds, CloudFront or browser caches might retain old static files. Use `Ctrl + F5` (or `Cmd + Shift + R` on macOS) to bypass local caches and fetch fresh assets.

---

### Verify CloudFront via Browser F12 Developer Tools

Because CloudFront is managed automatically under Amplify, verify operations directly via your web browser:

**Step 1:** Open your web browser (Chrome, Edge, or Firefox) and navigate to the production app: `https://main.dp5hgt6k889yu.amplifyapp.com`.

**Step 2:** Press **`F12`** (or right-click → **Inspect**) to open **Developer Tools**.

**Step 3:** Switch to the **Network** tab → Reload the webpage.

**Step 4:** Click the primary HTML page request or static JS/CSS assets:
*   Inspect the **Response Headers** panel on the right.
*   Verify presence of the **`via`** header containing `1.1 <edge-location-code>.cloudfront.net (CloudFront)`.
*   Verify presence of the **`x-cache`** header displaying `Hit from cloudfront` (cached edge hit) or `Miss from cloudfront` (initial cache fill).

---

![Figure 5.6.2a. Inspecting CloudFront CDN Response Headers via F12 Developer Tools.](../../../images/finvantage-cloudfront-header.jpg)

---

![Figure 5.6.2b. AWS CloudFront Console Managed Response Headers Policies configuration (CORS & Security Headers).](../../../images/finvantage-cloudfront-policies.jpg)

---

### Common Troubleshooting
*   **Issue: `Frontend interface does not update after deployment`**
    *   *Cause:* CloudFront CDN or browser cache retention.
    *   *Resolution:* Perform a hard refresh (`Ctrl + F5`) or clear browser cache to force fetching updated assets from CloudFront edge locations.

### Summary
The underlying CloudFront CDN integrated into AWS Amplify Hosting is operational, delivering low-latency web asset distribution for FinVantage.
