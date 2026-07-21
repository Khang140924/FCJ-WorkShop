---
title: "Amazon API Gateway"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.5.1. </b> "
---

### Amazon API Gateway

### Objective
This page guides you on accessing **Amazon API Gateway Console** to verify REST API routing rules, Lambda integration bindings, CORS configuration, and the `prod` deployment stage for **FinVantage**.

### Overview
Amazon API Gateway serves as the single edge entry point accepting incoming HTTP requests from the React frontend, enforcing security filters, and proxying requests to downstream Lambda microservices.

### Service Role in FinVantage
*   **API Routing:** Maps HTTP methods (GET, POST, PUT, DELETE) directly to target AWS Lambda functions.
*   **CORS (Cross-Origin Resource Sharing):** Configured to allow the Amplify Frontend domain (`https://main.dp5hgt6k889yu.amplifyapp.com`) to issue secure cross-origin API calls without browser blockage.
*   **Cognito Authorizer:** Protects sensitive endpoints by validating JWT tokens passed in Authorization request headers. Invalid or expired tokens are rejected at the edge, saving Lambda execution costs.

---

### Verification Steps on AWS Console

**Step 1:** Log in to AWS Console → Search `API Gateway` → Select **API Gateway**.

**Step 2:** Select the active REST API: **`stcs2116b8`** (`finvantage-prod`).

**Step 3:** From the left menu, select **Resources** (or **Routes**):
*   Verify core system API endpoints:
    *   `GET /auth/health` - Auth service health check.
    *   `GET /auth/config` - Fetches Cognito auth parameters.
    *   `GET /auth/me` - Verifies active session token.
    *   `POST /invoices/import` - Receives metadata and returns presigned S3 upload URL.
    *   `POST /invoices/{id}/analyze` - Triggers AI analysis for specified invoice.
    *   `GET /invoices` & `POST /invoices` - List or create transactions manually.
    *   `GET /invoices/{id}`, `PUT /invoices/{id}`, `DELETE /invoices/{id}` - Invoice detail management.
    *   `GET /dashboard-summary` - Fetches aggregated spending metrics.
    *   `/budgets` & `/spending-plan` - Budget management and spending plans.
*   Click any method (e.g., `POST /invoices/import`), verifying **Integration type** displays `Lambda Function` bound to `finvantage-prod-importInvoice`.

---


**Step 4:** Click **Stages** on the left menu:
*   Select stage **`prod`**.
*   Note the active **Invoke URL**: `https://stcs2116b8.execute-api.ap-southeast-1.amazonaws.com/prod`.

---

### Common HTTP Status Codes
When invoking backend APIs, API Gateway and Lambda return standard status codes:
*   **`200 OK` (or `201 Created`):** Successful request execution.
*   **`401 Unauthorized`:** Missing or invalid JWT authorization token.
*   **`403 Forbidden`:** Request blocked due to permission failure or CORS origin mismatch.
*   **`404 Not Found`:** Target API route or database invoice ID does not exist.
*   **`500 Internal Server Error`:** Unhandled runtime exception in Lambda code execution.
*   **`502 Bad Gateway`:** Lambda returned non-conforming API Gateway response object or timed out.

### Summary
Amazon API Gateway is properly configured with `prod` stage routing, serving as the front door for FinVantage APIs.
