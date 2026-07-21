---
title: "Frontend Hosting (Amazon S3)"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.6.1. </b> "
---

### Deploying Static Website Hosting

Instead of maintaining a server solely to run the web interface, the Serverless architecture leverages **Amazon S3** to store static files (HTML, CSS, JS) of the Frontend (e.g., ReactJS or VueJS source code after being `build`).

#### 1. Initializing S3 Bucket for Frontend
*   Create a new Bucket with the project's domain name (e.g., `app.finvantage.com`).
*   Unlike older guides that often require opening Public Access for S3, we apply modern security thinking: **Keep the Block all public access settings enabled**.
*   No one from the Internet can directly access this S3 link to download our source code.

#### 2. Configuring Static Distribution
*   Upload the entire `build/` or `dist/` directory of the Frontend source code to the Bucket.
*   Set the homepage file to `index.html` and the error document also to `index.html` (to support Client-side routing for SPA frameworks like React/Vue).

> 📸 **[IMAGE INSERTION REMINDER]:** Take a screenshot of the directory containing the static files (index.html, static/css, static/js) successfully uploaded to the Amazon S3 Bucket.
> *Markdown code:* `![Upload Frontend to S3](../../../images/s3-frontend-files.png)`