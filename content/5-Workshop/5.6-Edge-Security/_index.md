---
title: "Edge & Security Layer"
date: 2026-07-20
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

### Setting up the Edge Protection Layer

Securing the internal infrastructure (Private Subnets) is not enough. A financial system like FinVantage needs protection right from the very first touchpoint with users on the Internet. The Edge Security layer helps us solve three major problems:

1.  **Global Delivery:** Blazing-fast loading of the application interface (Frontend) regardless of where users are located globally.
2.  **Traffic Filtering & Attack Prevention:** Blocking denial-of-service (DDoS) attacks or malicious code (SQL Injection, XSS) targeting the API.
3.  **Identity Management:** Securely authenticating users and issuing valid tokens before granting access to personal data.

In this section, we will practice configuring the edge security service chain, including: Amazon S3 (Static Hosting), Amazon CloudFront, AWS WAF, and Amazon Cognito.