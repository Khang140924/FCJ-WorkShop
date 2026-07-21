---
title: "AWS Amplify Hosting"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.6.1. </b> "
---

### AWS Amplify Hosting

### Objective
This page guides you on compiling local React/Vite frontend code, configuring build environment variables, deploying static web builds to **AWS Amplify Hosting**, verifying build deployment history, and checking Rewrites and Redirects for **FinVantage**.

### Overview
AWS Amplify Hosting is a fully managed hosting service optimized for Single Page Applications (SPAs). Amplify automatically provisions an underlying CloudFront CDN distribution, manages HTTPS certificates, and provides flexible URL routing rules.

### Service Role in FinVantage
*   **Web Hosting:** Hosts the React/Vite web application interface for online user access at `https://main.dp5hgt6k889yu.amplifyapp.com`.
*   **SPA Fallback:** Enables client-side React Router navigation. When users open nested routes like `/invoices` or `/settings`, Amplify redirects requests to `/index.html` with a 200 rewrite, enabling client-side routing without 404 errors.
*   **Reverse Proxy:** Safely proxies `/auth` requests to the backend authentication API.

---

### Frontend Build and Deployment Process (Manual Deployment)

Before uploading code to Amplify Hosting, compile the project locally:

**Step 1: Configure Build Environment Variables**
Open the Frontend source code in VS Code. Create a `.env` file (or specify environment variables during build) containing backend API Gateway endpoints:
```bash
VITE_API_BASE_URL=https://stcs2116b8.execute-api.ap-southeast-1.amazonaws.com/prod
VITE_AUTH_MODE=cognito
```
> ⚠️ **Security Warning:** Never put sensitive database passwords or secret keys into `VITE_*` environment variables, as client-side bundlers embed these variables directly into public JavaScript bundles.

**Step 2: Install Dependencies and Build Project**
Execute the following commands in your frontend terminal:
```bash
npm install
npm run build
```
The compiled static bundle is generated inside `frontend/dist/`.

**Step 3: Compress Distribution Archive**
*   Open the `dist/` directory.
*   Select all internal contents (`index.html`, `assets/` folder...) and compress them into a `.zip` archive.
*   > ⚠️ **Important:** `index.html` and `assets/` must reside directly at the root of the ZIP file. If you zip the parent `dist/` folder itself, Amplify will fail to parse web root files, leading to 404 blank pages.

**Step 4: Manual Deploy to AWS Amplify**
Upload the ZIP archive to the `FinVantage` application inside the Amplify Console.

---

### Verification Steps on AWS Console

#### 1. Verify Frontend Deployment History

**Step 1:** Log in to AWS Console → Search `Amplify` → Select **AWS Amplify**.

**Step 2:** Select application **FinVantage** → Select branch **main**.

**Step 3:** Inspect deployment details:
*   **Deployment status:** Verify status displays `Succeed` or `Successful`.
*   **Production URL:** Click the production URL (`https://main.dp5hgt6k889yu.amplifyapp.com`) to open the live web app and verify HTTP 200 asset loading.

---

![Figure 5.6.1a. Successful frontend deployment history on AWS Amplify Hosting.](../../../images/finvantage-amplify-deployments.jpg)

---

#### 2. Verify Rewrites and Redirects Rules (SPA Fallback & Proxy)

**Step 1:** From the left menu of the FinVantage app, select **Rewrites and redirects** under App settings.

**Step 2:** Verify routing rules strictly follow this order:
1.  **Source address:** `</auth>` & `</auth/<*>>` → **Target address:** Backend API endpoint → **Type:** `200 (Rewrite)` serving as API proxy.
2.  **Source address:** `</**>` → **Target address:** `/index.html` → **Type:** `200 (Rewrite)` serving as SPA fallback.

*Note:* The `/auth` rule must precede the wildcard `</**>` rule so API requests are routed correctly before falling back to `index.html`.

---

![Figure 5.6.1b. Rewrites and redirects rule configuration supporting SPA fallback and reverse proxy.](../../../images/finvantage-amplify-redirects.jpg)

---

### Summary
AWS Amplify Hosting has successfully deployed the frontend application, synchronized with backend API Gateways, and established secure SPA fallback routing.

---

### Report Screenshot Checklist
1.  `finvantage-amplify-deployments.png` - Successful frontend deployment history.
2.  `finvantage-amplify-redirects.png` - Amplify Rewrites and redirects table configuration.