---
title: "Workshop overview"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

## Workshop Overview

The goal of this workshop is to deploy EAM Workspace to AWS and validate the end-to-end flow from the browser to the database. The content follows the deployment model used in the project: Amplify Hosting for the frontend, API Gateway for the `/api` route, Elastic Beanstalk for the backend, and RDS MySQL for data.

EAM Workspace has two main user experiences:

- **Admin Portal**: manages employees, departments, categories, assets, assignments, returns, maintenance, inventory, reports, feedback, FAQ content, attendance, login history, and support chat.
- **Employee Portal**: allows employees to view assigned assets, submit support requests, read FAQ content, update profile information, change password, and view personal history.

The backend exposes REST APIs under the `/api` prefix. The frontend calls APIs through the relative `/api` path, Amplify rewrites the request to API Gateway, and API Gateway forwards it to the Elastic Beanstalk backend.

## Target Outcomes

After completing the workshop, the system will have:

- A React frontend hosted on AWS Amplify Hosting.
- A Node.js/Express backend running on AWS Elastic Beanstalk.
- An Amazon API Gateway HTTP API as the backend entry point.
- A MySQL database running on Amazon RDS.
- A working `/api/health` endpoint through both API Gateway and the Amplify domain.
- Admin login, user login, and main workflows validated in the browser.
- CloudWatch Logs available for backend troubleshooting.

## Deployment Flow

The workshop deployment flow is organized from the data layer, backend, API entry point, and finally the frontend. This order makes it possible to verify each component separately before connecting everything into a complete system.

First, the AWS environment, source code, and required configuration variables are prepared. Amazon RDS for MySQL is then configured as the main application database. After the database is ready, the Node.js/Express backend is packaged and deployed to AWS Elastic Beanstalk, with environment variables such as `DATABASE_URL`, `JWT_SECRET`, SES SMTP settings, and CORS origins configured.

After the backend is healthy and the `/api/health` endpoint returns a successful response, Amazon API Gateway is created as the public entry point for the backend. The React/Vite frontend is deployed to AWS Amplify Hosting, and rewrite rules are configured so `/api/*` and `/uploads/*` requests from the Amplify domain are forwarded to API Gateway. Finally, the system is validated through the main workflows, including admin login, employee login, asset management, asset assignment, API requests in DevTools, and inactive account login blocking.

{{< mermaid >}}
graph TD
    A["Prepare AWS account, source code, and environment variables"] --> B["Create or configure RDS MySQL"]
    B --> C["Package the backend source bundle"]
    C --> D["Deploy backend to Elastic Beanstalk"]
    D --> E["Configure environment properties and test health"]
    E --> F["Create API Gateway HTTP API"]
    F --> G["Deploy frontend to Amplify Hosting"]
    G --> H["Add /api/* and /uploads/* rewrite rules to API Gateway"]
    H --> I["Test login, upload, and main workflows"]
    I --> J["Check CloudWatch Logs and clean up resources"]
{{< /mermaid >}}

## AWS Services in Scope

| Service | Purpose |
| --- | --- |
| AWS Amplify Hosting | Host and build the React/Vite frontend. |
| Amazon API Gateway | Provide a public HTTP API for the `/api/*` path. |
| AWS Elastic Beanstalk | Run and manage the Node.js backend. |
| Amazon RDS for MySQL | Store application data. |
| Amazon S3 | Production-ready direction for file upload storage. |
| Amazon SES | Send OTP and notification emails when mail configuration is enabled. |
| Amazon CloudWatch | Store logs and support monitoring. |

## Step 1: Review the Deployment Architecture

Before configuring each service, review the overall connection flow of the system.

![Workshop architecture overview for EAM Workspace](/eam-workshop-report/images/5-Workshop/5.1-Workshop-overview/5.1.1-architecture-overview.png)

*Figure 5.1.1. Workshop architecture overview.*

This diagram confirms the main architecture components: the frontend is served through Amplify, API requests go through API Gateway, the backend runs on Elastic Beanstalk, and data is stored in Amazon RDS for MySQL.

## Step 2: Identify the AWS Services Used

After reviewing the architecture, map each component in the diagram to the AWS services used in the workshop.

![AWS services overview used in the workshop](/eam-workshop-report/images/5-Workshop/5.1-Workshop-overview/5.1.2-aws-services-overview.png)

*Figure 5.1.2. AWS services overview used in the workshop.*

Use this service list to match the workshop scope with Amplify, API Gateway, Elastic Beanstalk, RDS, SES, and CloudWatch.

## Demo Environment Limits

This workshop is scoped for a demo environment:

- RDS can use Single-AZ to reduce cost.
- The backend can run with one small Elastic Beanstalk environment.
- Amplify uses the default domain.
- Route 53 custom domain is not required.
- File upload can go through the backend for the demo; S3 is documented as the production-ready direction.
