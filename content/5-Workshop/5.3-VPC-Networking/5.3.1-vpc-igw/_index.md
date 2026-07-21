---
title: "Create or Verify VPC"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---

### Create or Verify VPC and Internet Gateway

### Objective
This page guides you on accessing the **VPC Console** on AWS to verify the configuration of the custom Virtual Private Cloud (VPC) and Internet Gateway (IGW) provisioned for **FinVantage**.

### Overview
To build a resilient and secure cloud application on AWS, confirming that the base VPC network functions properly is the very first step. FinVantage uses a dedicated private IPv4 CIDR block to prevent address conflicts with external systems.

### Core Service Roles in FinVantage
*   **Amazon VPC:** Acts as a secure network perimeter enveloping the Lambda backend, PostgreSQL database, and Valkey cache. Unwanted external connection attempts are blocked at this perimeter.
*   **Internet Gateway (IGW):** Serves as an egress/ingress gateway for resources in Public Subnets (e.g., enabling NAT Gateway to route outbound web traffic or fetch dependencies).

---

### Verification Steps on AWS Console

> ⚠️ **Note:** Your production FinVantage VPC network resources have been pre-provisioned. Use these steps to verify parameters and collect configuration screenshots for documentation.

Follow these verification steps:

**Step 1:** Log in to the AWS Console, search for `VPC` and select **VPC**. Ensure the top-right Region is set to **Singapore (`ap-southeast-1`)**.

**Step 2:** From the left navigation menu, click **Your VPCs**. 
*   Locate the VPC for FinVantage (Name tag `FinVantage-VPC` or `finvantage-prod-vpc`).
*   Verify that the **State** column shows `Available`.
*   Note the **IPv4 CIDR block** (e.g., default `10.0.0.0/16`).

---


**Step 3:** Select the FinVantage VPC and check the **Details** tab below:
*   Ensure **DNS resolution** is set to `Enabled`.
*   Ensure **DNS hostnames** is set to `Enabled`. 
*   *Note:* Enabling DNS attributes allows internal AWS service domain name resolution inside the VPC.

**Step 4:** From the left menu, click **Internet gateways**:
*   Locate the Internet Gateway attached to your VPC (`FinVantage-IGW` or `finvantage-prod-igw`).
*   Verify that the **State** column shows `Attached`.
*   Ensure the **VPC ID** column matches the FinVantage VPC ID verified in Step 2.

---

![Figure 5.3.1b. Internet Gateway successfully attached to the FinVantage VPC.](../../../images/finvantage-igw.jpg)

---

### Integration with Other Services
An attached Internet Gateway does not route traffic automatically. In subsequent lessons, we will associate it with Public Subnet Route Tables to enable internet access for edge components.

### Common Troubleshooting
*   **Issue: `DNS resolution fails inside VPC`**
    *   *Cause:* DNS resolution or DNS hostnames is disabled in VPC attributes.
    *   *Resolution:* Go to **Your VPCs** → Select FinVantage VPC → Click **Actions** → **Edit VPC settings** → Enable **Enable DNS hostnames** and **Enable DNS resolution** → Click **Save**.

### Summary
The VPC and Internet Gateway are operating properly, establishing a foundation for subnet creation in the next lesson.
