---
title: "NAT Gateway & Private Subnets"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---

### 1. Setting up Private Subnets

This is a highly secured and isolated area with no Public IPs assigned. Sensitive data (such as the Database storing card/spending information) will be located here.
*   **Private Subnet 1 (Database):** CIDR `10.0.10.0/24` (AZ `us-east-1a`)
*   **Private Subnet 2 (Database):** CIDR `10.0.20.0/24` (AZ `us-east-1b`)

### 2. Provisioning the NAT Gateway

Lambda functions located in the Private Subnet (e.g., `Analysis Lambda`) need to call out to the Internet to communicate with Amazon Bedrock AI. Since they do not have Public IPs, they must go through an intermediary gateway, which is the NAT Gateway.
*   **Placement:** The NAT Gateway must be placed in a **Public Subnet**.
*   **Elastic IP:** Allocate a static IP address (Elastic IP) for the NAT Gateway so it can represent the outbound traffic from the Private Subnets.

> 📸 **[IMAGE INSERTION REMINDER]:** Take a screenshot of the detailed configuration of the newly created NAT Gateway, highlighting the Subnet (located in the Public tier) and the Elastic IP in red.
> *Markdown code:* `![NAT Gateway Configuration](../../../images/nat-gateway-config.png)`