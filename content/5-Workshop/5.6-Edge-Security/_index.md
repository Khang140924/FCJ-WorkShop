---
title: "Edge Security, Authentication and Hosting"
date: 2026-07-20
weight: 6
chapter: true
pre: " <b> 5.6. </b> "
---

### Edge Security, Authentication, and Hosting Layer

Welcome! Having constructed backend business microservices and AI capabilities in preceding chapters, our goal in this chapter is bringing the FinVantage React Frontend online, configuring Cognito user authentication, and establishing edge protection perimeters.

A financial management application must be protected and accelerated right at the global edge locations. Edge infrastructure resolves three primary requirements:

1.  **High-Speed Web Hosting & Caching:** Distributes the React/Vite Frontend to global users with minimal latency via AWS global CDN edge networks.
2.  **User Identity Governance:** Manages user registration, login authentication, and JWT session issuing via Amazon Cognito as the primary Identity Provider.
3.  **Traffic Filtering & DDoS Mitigation (Proposed):** Integrates AWS WAF to filter malicious payloads (SQL Injection, XSS) and rate-limit API calls.

---

### Chapter Roadmap

We will proceed through 4 detailed hands-on lessons:

1.  **Lesson 5.6.1. AWS Amplify Hosting:** Package static React frontend assets, deploy to Amplify Hosting, verify build logs, and configure URL rewrites/redirects (SPA fallback & reverse proxy).
2.  **Lesson 5.6.2. CloudFront CDN:** Inspect how AWS Amplify Hosting integrates CloudFront CDN to cache and distribute static web assets.
3.  **Lesson 5.6.3. AWS WAF (Proposed Security Extension):** Explore web application firewall security concepts protecting API endpoints.
4.  **Lesson 5.6.4. Amazon Cognito:** Verify User Pool configuration (`ap-southeast-1_HQYkeSq33`), Hosted UI settings, Callback URLs, and active user account lists.

Let's begin with AWS Amplify Hosting in the next lesson!