---
title: "Amazon RDS Proxy Configuration"
date: 2026-07-20
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

### Solving the Serverless Connection Pool Problem

AWS Lambda functions can scale up to thousands of instances within seconds. If each Lambda function opens a direct connection to MySQL, the Database will immediately exhaust its Connection Pool and crash.

To solve this, FinVantage uses **Amazon RDS Proxy**.
*   **Functionality:** RDS Proxy sits between Lambda and RDS. It maintains a small number of persistent connections to the Database and multiplexes these connections across thousands of running Lambda functions.
*   **Configuration:** 
    *   Provision an RDS Proxy and point the Target to the newly created MySQL instance.
    *   Store the RDS login credentials (Username/Password) in **AWS Secrets Manager**. RDS Proxy will automatically retrieve the information from Secrets Manager to log in, saving us from having to hard-code passwords into the Lambda source code.

> 📸 **[IMAGE INSERTION REMINDER]:** Take a screenshot of the RDS Proxy configuration interface, showing the Target database and Secrets Manager being linked.
> *Markdown code:* `![Amazon RDS Proxy](../../../images/rds-proxy-config.png)`