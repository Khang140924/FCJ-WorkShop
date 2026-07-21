---
title: "Resource Cleanup"
date: 2026-07-20
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

### Infrastructure Teardown (FinOps Mindset)

In a Cloud environment, forgetting to shut down resources after completing a lab is the leading cause of unexpected and massive bills (especially with NAT Gateways, Multi-AZ RDS, and hourly-billed ElastiCache clusters).

Here is the safe teardown sequence to avoid "Resource in use" errors:

1.  **Delete the Edge Layer:** Disable and then delete the CloudFront Distribution. Delete the rules in AWS WAF.
2.  **Clean up Storage:** Access Amazon S3, click "Empty bucket" (clearing all invoice files and Frontend code inside) before you can "Delete bucket".
3.  **Terminate Compute & AI:** Delete REST APIs in API Gateway. Delete all AWS Lambda functions, SQS queues, and disconnect Amazon Bedrock.
4.  **Remove the Data Layer:** Delete the RDS Proxy first. Next, delete the Amazon ElastiCache Cluster. Finally, proceed to delete the Amazon RDS Database (you can skip taking a final snapshot to save time).
5.  **Clean up Network Infrastructure (VPC):** Critically important: Delete the **NAT Gateway** first and **Release Elastic IP** back to AWS. Once internal services are cleared out, delete the VPC (AWS will automatically remove the attached Subnets, IGW, and Route Tables).
6.  **Delete Permissions:** Access the IAM Console to delete the custom roles created (Core-Lambda-Role, AI-Processing-Role).

Upon completing this process, your AWS account will return to a clean state, marking the complete success of the FinVantage Workshop!