---
title: "Week 7 Worklog"
date: 2026-06-15
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Research the theoretical overview of the Serverless Architecture model.
* Learn the operational principles of AWS Lambda, Amazon API Gateway, Amazon SQS, and SNS.
* Practice initializing a Lambda function and setting up automated event-based triggers (Event Triggers).
* Deploy and configure a REST API via API Gateway to create a secure connection port for the Backend application.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Research theory on Serverless Architecture on the AWS platform. <br> - Watch in-depth lectures on Serverless Services and Message Queue. | 15/06/2026   | 15/06/2026      | YouTube AWS Study Group |
| 3   | - Learn about AWS Lambda, Triggers, Amazon SQS, SNS, and API Gateway. <br> - Read guides on packaging source code, managing environment variables, and configuring Runtime. | 16/06/2026   | 16/06/2026      | Platform Bootcamp |
| 4   | - **Practice:** Initialize a basic Lambda function and configure a compatible Runtime environment. <br> - Configure a REST API on Amazon API Gateway to create an Endpoint to receive user requests. | 17/06/2026   | 17/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - **Practice:** Set up Triggers so the Lambda function runs automatically when an event occurs (e.g., a new image file is uploaded to an S3 Bucket). | 18/06/2026   | 18/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Practice:** Initialize an Amazon SQS queue to test the mechanism of sending and receiving messages between two independent services. | 19/06/2026   | 19/06/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Week 7 Achievements:

* Mastered the Serverless design mindset: Understood the benefits of not having to manage server infrastructure, with the system automatically scaling based on requests and billing only for actual execution time.

* Clearly distinguished asynchronous message passing mechanisms: Amazon SQS (Pull queue model to decouple systems) and Amazon SNS (Pub/Sub model to Push notifications to multiple destinations).

* Understood how API Gateway acts as an outer protection layer, securely receiving and routing internet traffic to internal processing functions.

* Successfully initialized an AWS Lambda Function, configured a compatible Runtime, and wrote a short logical processing script.

* Successfully configured a REST API on Amazon API Gateway, integrated with the Lambda function to receive HTTP methods (GET/POST) and return results to the Client.

* Practiced setting up Triggers to automate processes upon events on Amazon S3.

* Successfully deployed an Amazon SQS queue, preventing data bottlenecks when communicating between independent services.

* Learned the mindset of building Event-driven Architectures and Microservices, helping minimize interdependency (Loose Coupling) for Backend services.

* Recognized how Serverless optimizes enterprise costs: Replacing 24/7 EC2 servers with AWS Lambda for short-term or low-frequency tasks.