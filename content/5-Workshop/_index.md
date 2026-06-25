---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Deploying EAM Workspace on AWS

#### Overview

In this workshop, you will deploy **EAM Workspace**, an Enterprise Asset Management system, to AWS. The application includes a React frontend, a Node.js/Express backend, and a MySQL database managed with Prisma.

The target architecture is designed for an internal demo environment. It uses AWS managed services to keep the deployment simple, practical, and cost-aware:

- **AWS Amplify Hosting** for the React frontend.
- **Application Load Balancer** as the public backend entry point.
- **AWS Elastic Beanstalk** for the Node.js/Express backend.
- **Amazon RDS for MySQL** for application data.
- **Amazon S3** for production-ready file storage design.
- **Amazon SES** for OTP and email flows.
- **Amazon CloudWatch** for logs and basic monitoring.

This workshop follows the demo deployment path: no Route 53, no custom domain, and no Amazon Cognito. Authentication is handled by the backend using JWT.

#### Architecture

{{< mermaid >}}
flowchart LR
    User["User Browser"] --> Amplify["AWS Amplify Hosting\nReact Frontend"]
    Amplify --> Rewrite["/api Rewrite"]
    Rewrite --> ALB["Application Load Balancer"]
    ALB --> EB["Elastic Beanstalk\nNode.js Backend"]
    EB --> RDS["Amazon RDS MySQL\nPrivate Subnet"]
    EB --> S3["Amazon S3\nPrivate Bucket"]
    EB --> SES["Amazon SES"]
    EB --> CW["CloudWatch Logs"]
{{< /mermaid >}}

#### Content

1. [Workshop overview](5.1-Workshop-overview/)
2. [Prerequisites](5.2-Prerequisites/)
3. [Prepare network and RDS](5.3-Network-RDS/)
4. [Deploy backend with Elastic Beanstalk](5.4-Backend-Elastic-Beanstalk/)
5. [Deploy frontend with Amplify Hosting](5.5-Frontend-Amplify/)
6. [Test, monitor, and troubleshoot](5.6-Test-Monitor/)
7. [Clean up resources](5.7-Cleanup/)
