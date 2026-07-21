---
title: "Amazon Cognito"
date: 2026-07-20
weight: 4
chapter: false
pre: " <b> 5.6.4. </b> "
---

### Amazon Cognito User Pool

### Objective
This page guides you on accessing **Amazon Cognito Console** to verify User Pool ID **`ap-southeast-1_HQYkeSq33`**, inspect App client settings (Client ID), Hosted UI configuration, Callback URLs, and active user accounts for **FinVantage**.

### Overview
Amazon Cognito provides user identity, authentication, and authorization services. FinVantage uses Cognito as the central Identity Provider to manage login flows and issue JWT tokens for authenticating API requests sent to backend microservices.

### Actual FinVantage Configuration Parameters

*   **User Pool ID:** `ap-southeast-1_HQYkeSq33` (Singapore Region).
*   **App client settings:**
    *   **Client ID:** Client identifier binding React frontend interactions.
    *   **Client Secret:** Stored securely for server-side session authentication.
*   **Hosted UI configuration:**
    *   **Allowed callback URLs:**
        *   Production: `https://main.dp5hgt6k889yu.amplifyapp.com/auth/callback`
        *   Local test: `http://localhost:5173/auth/callback`
    *   **Allowed sign-out URLs:**
        *   Production: `https://main.dp5hgt6k889yu.amplifyapp.com`
        *   Local test: `http://localhost:5173`
    *   **OAuth 2.0 Grant Types:** `Authorization code grant` (Most secure code exchange pattern).
    *   **OAuth 2.0 Scopes:** `openid`, `email`, `profile`.

---

### Verification Steps on AWS Console

#### 1. Verify User Pool and App Client Settings

**Step 1:** Log in to AWS Console → Search `Cognito` → Select **Amazon Cognito**.

**Step 2:** From User pools, select **`ap-southeast-1_HQYkeSq33`**.

**Step 3:** Switch to **App integration** → Scroll down to **App clients and analytics**:
*   Confirm the App client binding the Frontend. Copy the **Client ID**.
*   Click the app client name to view Hosted UI settings.

**Step 4:** Under **Hosted UI settings**, click **Edit** to verify **Callback URLs** and **Sign-out URLs** match configuration requirements.

---

![Figure 5.6.4a. Hosted UI and Callback URL configuration for Amazon Cognito User Pool.](../../../images/finvantage-cognito-config.jpg)

---

#### 2. Inspect Active User Accounts

**Step 1:** On the User Pool detail page, click **Users**.

**Step 2:** Inspect registered user accounts:
*   Confirm user account **Status** displays `Confirmed`.
*   **OTP Verification Trigger:** Upon user registration, Cognito automatically dispatches confirmation OTP emails before setting status to Confirmed.

---

![Figure 5.6.4b. Active registered user account list on Amazon Cognito User Pool.](../../../images/finvantage-cognito-users.jpg)

---

> ⚠️ **Important Security Note:** Mask (blur) private personal email addresses when collecting screenshots for documentation.

### Summary
Amazon Cognito User Pool is operational, issuing secure JWT tokens, hosting standardized login interfaces, and managing user access.
