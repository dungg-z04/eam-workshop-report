---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Deploying EAM Workspace on AWS

#### Overview

This workshop guides the deployment of **EAM Workspace**, an Enterprise Asset Management system, to AWS as a full-stack demo. The application includes a React/Vite frontend, a Node.js/Express backend, Prisma ORM, and a MySQL database.

The deployment flow matches the project completed during the internship: the frontend runs on AWS Amplify Hosting, public API traffic goes through Amazon API Gateway, the backend runs on AWS Elastic Beanstalk, and application data is stored in Amazon RDS for MySQL.

Main services:

- **AWS Amplify Hosting** for the React frontend.
- **Amazon API Gateway HTTP API** for the `/api/*` route.
- **AWS Elastic Beanstalk** for the Node.js/Express backend.
- **Amazon RDS for MySQL** for application data.
- **Amazon S3** for production-ready file storage direction.
- **Amazon SES** for OTP and email flows.
- **Amazon CloudWatch** for logs and troubleshooting.

This workshop follows the demo deployment path: no Route 53, no custom domain, and no Amazon Cognito. Authentication is handled by the backend using JWT.

#### Architecture

{{< mermaid >}}
flowchart LR
    User["User Browser"] --> Amplify["AWS Amplify Hosting\nReact Frontend"]
    Amplify --> Rewrite["Rewrite /api/*"]
    Rewrite --> APIGW["Amazon API Gateway\nHTTP API"]
    APIGW --> EB["AWS Elastic Beanstalk\nNode.js Backend"]
    EB --> RDS["Amazon RDS MySQL"]
    EB --> S3["Amazon S3\nProduction-ready File Storage"]
    EB --> SES["Amazon SES"]
    EB --> CW["CloudWatch Logs"]
{{< /mermaid >}}

#### Content

1. [Workshop overview](5.1-Workshop-overview/)
2. [Prerequisites](5.2-Prerequisites/)
3. [Prepare network and RDS](5.3-Network-RDS/)
4. [Deploy backend with Elastic Beanstalk](5.4-Backend-Elastic-Beanstalk/)
5. [Connect API Gateway and Amplify Hosting](5.5-Frontend-Amplify/)
6. [Test, monitor, and troubleshoot](5.6-Test-Monitor/)
7. [Clean up resources](5.7-Cleanup/)
