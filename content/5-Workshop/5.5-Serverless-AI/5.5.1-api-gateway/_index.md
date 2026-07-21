---
title: "API Gateway"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.5.1. </b> "
---

### Provisioning Amazon API Gateway

**Amazon API Gateway** acts as the sole "receptionist" for the entire backend system. All requests from the Frontend (users) must pass through this gateway before being routed to the corresponding Lambda functions.

#### 1. Building the REST API
We provision a REST API with a clear Endpoint structure:
*   `POST /invoice/import`: Receives the invoice file. Points to `Import Lambda`.
*   `POST /payment/create`: Creates a manual transaction. Points to `Payment Lambda`.
*   `GET /analytics/summary`: Retrieves spending statistics. Points to `Analysis Lambda`.

#### 2. Integrating Authentication (Cognito Authorizer)
To ensure that only logged-in users can call the API, we attach a **Cognito Authorizer** to the API Gateway.
*   When a request arrives, API Gateway will check the `JWT Token` in the Header. 
*   If the token is valid, it allows the request to proceed to the Lambda function. If not, it immediately returns a `401 Unauthorized` error, helping to protect Lambda from spam calls (saving execution costs).

> 📸 **[IMAGE INSERTION REMINDER]:** Take a screenshot of the **Resources** interface in API Gateway, showing the directory tree of API endpoints (e.g., `/invoice`, `/payment`) and the Integration Request flow pointing to the Lambda functions.
> *Markdown code:* `![Amazon API Gateway Configuration](../../../images/api-gateway-routes.png)`