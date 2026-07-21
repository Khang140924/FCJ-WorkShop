---
title: "Resource Cleanup"
date: 2026-07-20
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

### Resource Cleanup

### Objective
This page guides you through safely destroying all AWS resources provisioned throughout the FinVantage Workshop in proper order, avoiding unexpected charges and preventing `Resource in use` deletion errors.

### Why Cleanup is Mandatory
In Cloud environments, the following infrastructure components incur **hourly recurring charges** even when idle:
*   **NAT Gateway:** ~$0.045/hour (~$32/month).
*   **RDS PostgreSQL Instance:** Depending on instance class (~$15–$70/month).
*   **ElastiCache Valkey/Redis:** Depending on node type (~$12–$50/month).
*   **RDS Proxy:** ~$0.015/vCPU/hour.

> ⚠️ **Warning:** Forgetting to tear down these resources after completing the Lab is the leading cause of unexpected AWS monthly bill spikes.

---

### Safe Destruction Order

Follow this sequence to prevent resource dependency errors:

#### Step 1: Destroy Backend Serverless Compute (Lambda, API Gateway)
*   If deployed via **Serverless Framework**, execute in your terminal:
    ```bash
    npx serverless remove --stage prod
    ```
    This command automatically removes: Lambda functions, API Gateway REST APIs, linked CloudWatch Log Groups, and auto-generated IAM roles.
*   If deployed manually, tear down in sequence: API Gateway → Lambda Functions → CloudWatch Log Groups.

#### Step 2: Destroy Data & Cache Layer (Database & Cache)
*   **Amazon RDS Proxy:** Go to RDS Console → Proxies → Select FinVantage Proxy → **Delete**.
*   **Amazon ElastiCache:** Go to ElastiCache Console → Select Valkey/Redis cluster → **Delete** (Skip final snapshot for lab environments).
*   **Amazon RDS PostgreSQL:** Go to RDS Console → Databases → Select database → **Delete**. Disable Deletion Protection first if active. Skip final snapshot for lab testing.
*   **DB Subnet Group:** Delete DB Subnet Group after database deletion completes.

#### Step 3: Destroy S3 Receipt Bucket
*   Go to S3 Console → Select `finvantage-invoices-hieu-2026-395840094907`.
*   Click **Empty bucket** (empties all stored receipt objects first).
*   After the bucket is empty, click **Delete bucket**.

#### Step 4: Destroy Frontend Hosting (Amplify)
*   Go to Amplify Console → Select FinVantage app → **App settings** → **General** → Click **Delete app**.

#### Step 5: Destroy Amazon Cognito User Pool
*   Go to Cognito Console → User pools → Select `ap-southeast-1_HQYkeSq33` → Click **Delete user pool**.

#### Step 6: Destroy Secrets Manager Secrets
*   Go to Secrets Manager Console → Delete secrets: `finvantage/prod/app-auth` and `finvantage/prod/redis-url`.
*   *Note:* AWS Secrets Manager defaults to a 7-day recovery window. Select `Schedule deletion` with minimum allowable days.

#### Step 7: Destroy Network Infrastructure (VPC)
*   **NAT Gateway:** Delete NAT Gateway first → Wait until status transitions to `Deleted` (1-2 minutes).
*   **Elastic IP:** Go to EC2 Console → Elastic IPs → Release Elastic IP allocated to the NAT Gateway.
*   **VPC:** Once sub-resources are deleted, go to VPC Console → Select FinVantage VPC → **Delete VPC**. AWS automatically deletes associated Subnets, Internet Gateways, Route Tables, and Security Groups.

#### Step 8: Destroy IAM Cross-Account Roles
*   Go to IAM Console (Primary Account) → Roles → Delete Lambda execution roles.
*   Go to IAM Console (Bedrock Account) → Roles → Delete `FinVantageBedrockInvokeRole`.

---

> ⚠️ **Final Verification:** After cleanup, open **AWS Billing Console** → **Bills** to confirm no active services continue billing charges. Check region `ap-southeast-1` specifically.

### Conclusion
By completing this tear-down workflow, your AWS account is restored to a clean state, marking the successful completion of the FinVantage Workshop! 🎉
