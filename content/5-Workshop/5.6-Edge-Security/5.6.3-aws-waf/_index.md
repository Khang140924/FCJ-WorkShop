---
title: "Web Application Firewall (WAF)"
date: 2026-07-20
weight: 3
chapter: false
pre: " <b> 5.6.3. </b> "
---

### Blocking Malicious Traffic Flows

**AWS WAF (Web Application Firewall)** is an iron shield attached directly to CloudFront (or API Gateway). It continuously scans incoming requests (HTTP/HTTPS) trying to enter the system to detect abnormal signs.

#### Setting up Protection Rules (Web ACL Rules)
We configure a Web ACL (Access Control List) and apply the following Rules to protect the FinVantage system:
1.  **Rate-based Rule (DDoS/Spam Protection):** Limits the number of requests from a single IP (e.g., maximum 500 requests / 5 minutes). If exceeded, that IP will be temporarily blocked, helping protect the API and Database from overload.
2.  **AWS Managed Rules (Core Rule Set):** Enables built-in AWS rulesets to block the most common security vulnerabilities from the OWASP Top 10 (such as SQL Injection, Cross-Site Scripting - XSS, and unauthorized port scanning).

> 📸 **[IMAGE INSERTION REMINDER]:** Take a screenshot of the AWS WAF Traffic chart (Overview tab), or the list of rules (Rules tab) activated within the Web ACL.
> *Markdown code:* `![AWS WAF Firewall Configuration](../../../images/aws-waf-rules.png)`