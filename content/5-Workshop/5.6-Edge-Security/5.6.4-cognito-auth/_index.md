---
title: "Identity Authentication (Cognito)"
date: 2026-07-20
weight: 4
chapter: false
pre: " <b> 5.6.4. </b> "
---

### Identity Management & Session Control

To ensure that each user's financial data is strictly private to them, FinVantage uses **Amazon Cognito** for secure and professional identity management.

#### 1. Initializing the Cognito User Pool
*   Create a **User Pool** to store user account information (Email, Password).
*   Enforce a strong password policy (uppercase letters, numbers, special characters).
*   Enable Email verification (sending OTP codes during registration or password recovery).

#### 2. Integrating JWT Tokens with API Gateway
The system's authentication workflow proceeds as follows:
1.  The user enters their Email/Password on the web interface.
2.  The Frontend sends this information to Amazon Cognito.
3.  Cognito validates the credentials and returns a **JSON Web Token (JWT)**.
4.  When the user wants to view spending reports, the Frontend attaches this JWT Token to the request Header.
5.  **API Gateway** (via the Cognito Authorizer configured in Section 5.5) verifies the token's validity before allowing the request to invoke the Lambda function.


> *Markdown code:* ![Amazon Cognito User Pool](../../../images/cognito-user-pool.png)