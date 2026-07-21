---
title: "AWS WAF (Web Application Firewall)"
date: 2026-07-20
weight: 3
chapter: false
pre: " <b> 5.6.3. </b> "
---

### AWS WAF (Proposed Security Extension)

> ⚠️ **IMPORTANT NOTE:**  
> **Proposed Architectural Extension (Not deployed in current production).**  
> AWS WAF incurs fixed recurring monthly costs (~$5.00/month per Web ACL plus ~$1.00/month per rule, excluding request volume charges). For workshop testing and lab environments, WAF is omitted to optimize costs. The section below describes theoretical edge firewall design patterns for commercial production deployment.

---

### Objective
This page outlines theoretical design patterns for integrating **AWS WAF (Web Application Firewall)** to protect API Gateway and CloudFront distributions against web exploits in **FinVantage**.

### Overview
AWS WAF is a web application firewall deployed at cloud edge locations. Attaching WAF directly to Amazon API Gateway or CloudFront Distributions inspects inbound HTTP/HTTPS request payloads, blocking malicious traffic before requests reach Lambda backends.

### Proposed Web ACL Protection Rules

For commercial deployment, FinVantage configures a **Web ACL (Web Access Control List)** containing:

1.  **Rate-based Rules:** 
    *   *Function:* Limits maximum requests originating from a single IP within a 5-minute evaluation window (e.g., max 300 requests / 5 minutes).
    *   *Purpose:* Mitigates brute-force login attempts, DDoS floods, and automated malicious scraping scripts.
2.  **AWS Managed Rule Groups:**
    *   *Function:* Enables pre-configured rule packages maintained by AWS security experts (e.g., Core Rule Set, SQL database protection).
    *   *Purpose:* Protects against OWASP Top 10 vulnerabilities, including SQL Injection (SQLi), Cross-Site Scripting (XSS), and vulnerability scanners.

---


### Common Troubleshooting with WAF
*   **Issue: `Legitimate users encounter HTTP 403 Forbidden`**
    *   *Cause:* Overly strict WAF rules (False Positives) or rapid image uploads triggering Rate-based limits.
    *   *Resolution:* Whitelist trusted IP ranges or adjust Rate-based Rule evaluation thresholds to accommodate normal user behavior.

### Summary
AWS WAF provides a robust edge security perimeter, protecting FinVantage during commercial scale-out.
