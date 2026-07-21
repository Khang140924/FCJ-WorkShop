---
title: "AI Integration (Textract & Bedrock)"
date: 2026-07-20
weight: 3
chapter: false
pre: " <b> 5.5.3. </b> "
---

### Automation with Artificial Intelligence

This is the most valuable feature of FinVantage. We use the `Parse & Categorize Lambda` function combined simultaneously with two AWS AI services.

#### 1. Text Extraction with Amazon Textract (OCR)
As soon as the invoice file (image/PDF) lands in S3, it wakes up the `Parse & Categorize Lambda`. 
*   The Lambda will call the API of **Amazon Textract** (`AnalyzeDocument`).
*   Textract uses Machine Learning to recognize handwriting, tables, and extract raw information fields (For example: "Milk tea", "50,000 VND", "12/07/2026").

#### 2. Intelligent Categorization with Amazon Bedrock (LLM)
The raw data from Textract does not yet have statistical meaning. The `Parse & Categorize Lambda` continues to aggregate that text and send a Prompt to **Amazon Bedrock** (using models like Claude 3).
*   **Example Prompt:** *"Based on the content of this invoice: [Textract Data], categorize the expense into one of the categories (Food & Beverage, Shopping, Transportation) and output in JSON format."*
*   Bedrock returns an accurate JSON result. Afterward, the Lambda saves this final result into Amazon RDS (via RDS Proxy).

> 📸 **[IMAGE INSERTION REMINDER]:** You can take a screenshot of the Python/Node.js code block calling `boto3.client('bedrock-runtime')` inside AWS Lambda, OR capture a log of the returned JSON result from Bedrock on CloudWatch.
> *Markdown code:* `![Amazon Bedrock Integration Code](../../../images/bedrock-integration.png)`