---
title: "AI Integration (Textract & Bedrock)"
date: 2026-07-20
weight: 3
chapter: false
pre: " <b> 5.5.3. </b> "
---

### AI Integration (Textract & Bedrock)

### Objective
This page guides you on verifying S3 trigger notifications firing the OCR Lambda, Textract `AnalyzeExpense` API integration, and configuring cross-account IAM AssumeRole access for **Amazon Bedrock** in **FinVantage**.

### Overview
This layer powers the core intelligence of FinVantage. The platform combines two specialized AWS AI services: Amazon Textract for raw OCR text extraction and Amazon Bedrock (Claude 3.5 Sonnet) for expense categorization and financial advice generation.

---

### 1. Advanced Invoice Extraction with Amazon Textract (OCR)

When the Frontend uploads a receipt image to S3, an S3 `ObjectCreated` event triggers the `finvantage-prod-ocrInvoice` Lambda function.
*   **Specialized API:** Lambda calls the `AnalyzeExpense` API of Amazon Textract (rather than standard `AnalyzeDocument`). Optimized by ML models, `AnalyzeExpense` automatically parses invoice structures, extracting Vendor, Total Amount, Date, and detailed LineItems.
*   **IAM Permissions:** The OCR Lambda execution role requires permissions to call `textract:AnalyzeExpense`.
*   **Caching Mechanism:** Raw extracted OCR text is cached in Valkey/Redis to prepare for AI analysis in downstream functions.

---

![Figure 5.5.3a. S3 Event Trigger configuration attached to OCR Lambda function.](../../../images/finvantage-s3-trigger-ocr.jpg)

---

### 2. Configure Cross-Account Amazon Bedrock Security (Cross-Account Role)

The primary FinVantage backend runs in the Primary AWS Account, but the Claude 3.5 Sonnet AI model resides in a separate AWS Account (Bedrock Account). To invoke the model, `analyzeInvoice` Lambda performs a role transition (`AssumeRole`) to obtain temporary security credentials.

Follow these verification steps to avoid `AccessDenied` errors:

**Step 1:** Log in to the AWS Console of the Primary Account → **Lambda** → Select **`finvantage-prod-analyzeInvoice`**.

**Step 2:** Open **Configuration** → **Permissions**. Click the **Execution role** link to open the IAM Role. Copy the **Role ARN** (e.g., `arn:aws:iam::111122223333:role/finvantage-prod-analyzeInvoice-role`).

**Step 3:** Log in to the AWS Console of the **Bedrock Account**.

**Step 4:** Open **IAM** → **Roles** → Select **`FinVantageBedrockInvokeRole`**.

**Step 5:** Open the **Trust relationships** tab → Click **Edit trust policy**.

**Step 6:** Verify or update the JSON Trust Policy granting permission to the primary Lambda execution role:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::111122223333:role/finvantage-prod-analyzeInvoice-role"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

---

![Figure 5.5.3b. Trust Relationship configuration on Bedrock Role granting access to primary Lambda role.](../../../images/finvantage-bedrock-trust-relationship.jpg)

---

**Step 7:** On `FinVantageBedrockInvokeRole` (Bedrock Account), open the **Permissions** tab:
*   Ensure the role is attached to a Permission Policy allowing Bedrock model invocation:
    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Action": [
            "bedrock:InvokeModel"
          ],
          "Resource": "arn:aws:bedrock:ap-southeast-1::foundation-model/anthropic.claude-3-5-sonnet-*"
        }
      ]
    }
    ```

**Step 8:** Return to the Primary AWS Account:
*   Open the **Execution role** of Lambda `finvantage-prod-analyzeInvoice` → Attach a policy granting permission to execute `sts:AssumeRole` targeting the ARN of `FinVantageBedrockInvokeRole`.

---

![Figure 5.5.3c. Policy granting sts:AssumeRole permission allowing primary Lambda to assume Bedrock Role across accounts.](../../../images/finvantage-lambda-sts-policy.jpg)

---

### Verification and Results
Once cross-account integration is established, uploading a receipt allows you to inspect **CloudWatch Logs** for `finvantage-prod-analyzeInvoice` to view JSON analysis returned by Bedrock:
*   Bedrock evaluates OCR text, categorizes expenses (`Dining` or `Transportation`), and outputs Vietnamese financial advice:
    `"ai_advice": "Expense of 50,000 VND at Phuc Long categorized under Dining. Consider reviewing your weekly food budget!"`

---

> 📸 PHOTO TO ADD  
> Screenshot: AWS Console → CloudWatch → Log groups → Select Log group for `ocrInvoice` or `analyzeInvoice`.  
> Content: Log execution entries recording Textract OCR success or Bedrock AI JSON output.  
> Suggested name: `finvantage-cloudwatch-ocr-logs.png`  
> Caption: "Figure 5.5.3d. CloudWatch Logs verifying successful Textract OCR and Bedrock AI analysis output."

---

### Common Troubleshooting
*   **Error: `AccessDeniedException: User: ... is not authorized to perform: sts:AssumeRole`**
    *   *Cause:* Principal ARN in Bedrock Trust policy is mistyped, or primary Lambda execution role lacks `sts:AssumeRole` permissions.
    *   *Resolution:* Audit role ARNs between both accounts following Steps 2 through 8.

### Summary
By configuring secure cross-account role delegation, FinVantage successfully integrates with Amazon Bedrock Claude 3.5 Sonnet for automated receipt analysis.

---

### Report Screenshot Checklist
1.  `finvantage-s3-trigger-ocr.png` - S3 event trigger on OCR Lambda.
2.  `finvantage-bedrock-trust-relationship.png` - Trust Relationship policy on Bedrock Account.
3.  `finvantage-lambda-sts-policy.png` - AssumeRole policy on Primary Account Lambda role.
4.  `finvantage-cloudwatch-ocr-logs.png` - Successful AI execution logs in CloudWatch Logs.