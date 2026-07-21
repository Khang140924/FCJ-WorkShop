---
title: "Prerequisites & Environment Setup"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

### Prerequisites & Permissions Setup

Welcome! Before we start building VPC networks or writing backend code for **FinVantage**, the first critical step is preparing your local development environment and configuring AWS access permissions.

Because our production application utilizes a multi-account architecture (Frontend hosted on AWS Amplify, Lambda backend assuming an IAM role to call Bedrock in another AWS account), configuring settings correctly from the start will prevent unexpected `AccessDenied` or connectivity errors.

---

### 1. AWS Account Requirements

To deploy the FinVantage system, we require:
*   **Backend Account (Primary Account):** Where we deploy VPC, RDS PostgreSQL, ElastiCache Valkey, API Gateway, and AWS Lambda functions.
*   **Bedrock Account (Cross Account):** Where AI models are enabled and contains the IAM Role `FinVantageBedrockInvokeRole` for cross-account AssumeRole delegation.
*   **Primary AWS Region:** Ensure Singapore (`ap-southeast-1`) region is used for the primary account to minimize latency for South East Asia users.

---

![Lambda VPC configuration in AWS Console](../../images/finvantage-lambda-vpc.png)

---

### 2. Enable Amazon Bedrock Model Access

Amazon Bedrock locks all foundation models by default. Since FinVantage uses **Claude 3.5 Sonnet** (Model ID: `global.anthropic.claude-sonnet-4-6`), we must request model access:
1.  Log in to the AWS Console of the Bedrock Account.
2.  Navigate to **Amazon Bedrock** → Select **Model access** from the left navigation panel.
3.  Click **Modify model access** → Check **Claude 3.5 Sonnet** (or Claude 3 Haiku depending on configuration).
4.  Click **Save changes** and wait until the access status changes to **Access granted** (green).

---

![Model Access interface in Amazon Bedrock console](../../images/finvantage-bedrock-models.png)

---

### 3. Local Development Tools Setup

Install the following essential tools on your local development machine:

1.  **Node.js (v20.x or newer):** Primary execution runtime for Lambda functions and React/Vite frontend.
2.  **npm (bundled with Node.js):** Package manager.
3.  **AWS CLI:** For managing local AWS authentication credentials.
4.  **Serverless Framework (installed globally via npm):** Tool for packaging and deploying serverless cloud resources.
5.  **Git:** Code version control.
6.  **VS Code:** Primary code editor.

Verification commands after installation:
```bash
# Check Node.js & npm version
node -v
npm -v

# Check AWS CLI version
aws --version

# Check Serverless Framework version
serverless -v
```

---

### 4. Configure AWS CLI Credentials

To grant Serverless Framework permission to deploy cloud resources to your AWS account, configure credentials locally:
1.  Obtain Access Key ID and Secret Access Key from an IAM User with Administrator privileges in the AWS Console.
2.  Open your terminal and run: `aws configure`.
3.  Provide Access Key ID, Secret Access Key, and default region `ap-southeast-1`.
4.  Run the following command to verify caller identity:
    ```bash
    aws sts get-caller-identity
    ```

---

### 5. Source Code Preparation

Project setup steps:
1.  Clone the FinVantage GitHub repository to your local machine.
2.  Navigate to the backend directory and run: `npm install` to install dependencies.
3.  Copy `.env.example` to `.env` and fill in real environment variables (`REDIS_URL`, DB credentials, `BEDROCK_ROLE_ARN`...).

> ⚠️ **Security Warning:** Never commit `.env` files containing real secrets, passwords, `.serverless/`, or `node_modules/` to GitHub repository.

---

### 6. Pre-deployment Checklist

Before configuring AWS resources in the next chapters, verify that:
*   `BEDROCK_ROLE_ARN` in `.env` correctly points to `FinVantageBedrockInvokeRole`.
*   `AWS_REGION` is set to `ap-southeast-1`.
*   `USE_MOCK_AI` is set to `false` when testing real Bedrock integration on Cloud.

Now that our environment is ready, let's proceed to VPC network setup in the next chapter!
