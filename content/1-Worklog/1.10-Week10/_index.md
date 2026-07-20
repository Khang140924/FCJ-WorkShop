---
title: "Week 10 Worklog"
date: 2026-07-06
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:

* Implement the Backend source code for the FinVantage project based on the Serverless Architecture model.
* Configure centralized connections from the source code to the AWS ecosystem (S3, Textract) and the Database module via the AWS SDK.
* Fully program the data processing API flow: Receive files, store on S3, extract data via Textract, and store results in the Database.
* Use Git for source code version control, package, and push complete commits to the GitHub online repository.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Begin the source code implementation phase for the Backend module of the FinVantage project. <br> - Deploy the directory structure according to the Serverless model. | 06/07/2026   | 06/07/2026      | Project Team |
| 3   | - Write configuration modules for secure connections from the source code to core services via the AWS SDK. | 07/07/2026   | 07/07/2026      | AWS Documentation |
| 4   | - **Practice:** Program the API to receive files from the Client and automatically upload invoice data to a secure Amazon S3 Bucket. | 08/07/2026   | 08/07/2026      | VS Code / Local Environment |
| 5   | - **Practice:** Program the processing flow to call the Amazon Textract API to read, extract invoice information, and standardize data into JSON format. <br> - Write functions to connect with the Database to permanently store the extracted results. | 09/07/2026   | 09/07/2026      | VS Code / Local Environment |
| 6   | - Use Git for version control and push the entire module source code to the GitHub repository with the commit "Complete Backend Serverless: API, S3, Textract, Database". | 10/07/2026   | 10/07/2026      | GitHub |


### Week 10 Achievements:

* Profoundly consolidated the Serverless Backend architecture, clearly understanding how to organize source code to optimize performance when running on a cloud environment instead of traditional servers.

* Mastered the Data Flow of an automated document processing system: From receiving files, storing, extracting data using AI, to saving the final results into the database.

* Successfully completed and pushed the entire module source code to GitHub, making the official commit "Complete Backend Serverless: API, S3, Textract, Database".

* Successfully implemented the API to receive files from the Client and automatically upload invoice data to a secure Amazon S3 Bucket.

* Programmed the processing flow to call the Amazon Textract API to automatically read and extract information from invoices, then standardize the data in JSON format.

* Successfully wrote functions to connect and interact with the Database to permanently store the extracted results, ready to provide data for the Generative AI module (Amazon Bedrock).

* Accumulated valuable practical experience in transforming infrastructure architecture diagrams into executable source code lines in reality.

* Enhanced teamwork skills via Git/GitHub, knowing how to break down tasks and create clear, professional commits matching enterprise environment standards.