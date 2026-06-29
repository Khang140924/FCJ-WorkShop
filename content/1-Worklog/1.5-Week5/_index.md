---
title: "Week 5 Worklog"
date: 2026-06-01
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

* Research the foundational theory of Amazon Virtual Private Cloud (Amazon VPC).
* Understand the components of AWS network architecture, including: Subnets (Public and Private), Route Tables, Internet Gateway (IGW), and NAT Gateway.
* Research multi-layer network security mechanisms through Network Access Control Lists (NACLs) and Security Groups.
* Practice designing and initializing a custom VPC network system, logically allocating network ranges for Web and Database applications via the console.
* Complete practical bonus tasks to accumulate AWS Credits for system testing.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Research the core theory of the isolated virtual network service Amazon VPC <br> - Watch the visual lecture series on Networking & VPC | 01/06/2026   | 01/06/2026      | YouTube AWS Study Group |
| 3   | - Learn the operational mechanics of Subnet, Route Table, Internet Gateway, and NAT Gateway <br> - Read network configuration guides and IP address allocation (CIDR Block) schemas | 02/06/2026   | 02/06/2026      | Platform Bootcamp |
| 4   | - **Practice:** <br>&emsp; + Establish a custom VPC network system <br>&emsp; + Separate Public and Private network zones from scratch | 03/06/2026   | 03/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - **Practice:** <br>&emsp; + Configure multi-layer network security rules by combining Network ACLs and Security Groups | 04/06/2026   | 04/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Advanced Practice (Earn AWS Credit):** <br>&emsp; + Task 1: Launch EC2 Instance (Earn $20 credit) <br>&emsp; + Task 2: Amazon Bedrock Playground (Earn $20 credit) | 05/06/2026   | 05/06/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Week 5 Achievements:

* Mastered the concept of Amazon VPC, understanding how to establish an independent and secure network partition on the AWS global cloud infrastructure.

* Clearly distinguished the differences between a Public Subnet (hosting Web Servers, directly connected to the Internet via an Internet Gateway) and a Private Subnet (completely isolated, used to host Databases or sensitive Backend logic).

* Understood the two-layer network security mechanism: NACLs (Subnet-level firewall - Stateless) and Security Groups (Instance-level firewall - Stateful) for maximum data traffic control.

* Successfully initialized a custom Amazon VPC network with standard CIDR block IP addressing, stably distributing Public and Private Subnets across multiple Availability Zones.

* Accurately configured an Internet Gateway and a NAT Gateway in the Public Subnet, allowing Backend servers in the Private Subnet to safely download software updates from the Internet one-way.

* Successfully completed 2 practical bonus tasks, including launching a virtual server (Task 1: Launch EC2 Instance) and getting familiar with the AI testing environment (Task 2: Amazon Bedrock Playground), successfully accumulating a total of $40 AWS Credit.

* Acquired the comprehensive system design mindset of a Backend Engineer: building secure applications by placing the public interface in the Public Subnet to welcome users, while keeping the entire Backend source code and Database strictly hidden in the Private Subnet.

* Improved the ability to read and comprehend Architecture Diagrams and successfully translated the design schema into actual running resources on the Cloud.