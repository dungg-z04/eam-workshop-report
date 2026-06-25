---
title: "Workshop overview"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

## Workshop overview

The goal of this workshop is to deploy EAM Workspace to AWS and validate the end-to-end flow from the browser to the database.

EAM Workspace has two main user experiences:

- **Admin Portal**: manage employees, departments, categories, assets, assignments, maintenance requests, inventory sessions, locations, reports, feedback, FAQ content, attendance history, login history, and support chat.
- **Employee Portal**: view assigned assets, submit support requests, read FAQ content, update profile information, change password, and review personal history.

The backend exposes REST APIs under the `/api` prefix. The frontend calls the backend through the relative path `/api`, and AWS Amplify rewrites those API requests to the Application Load Balancer DNS name.

## Target result

After completing the workshop, you should have:

- A React frontend hosted on AWS Amplify Hosting.
- A Node.js/Express backend running on AWS Elastic Beanstalk.
- A MySQL database running on Amazon RDS.
- A working `/api/health` endpoint.
- A browser flow that can log in and call backend APIs through the Amplify URL.
- CloudWatch Logs available for backend troubleshooting.

## Deployment flow

{{< mermaid >}}
flowchart TD
    A["Prepare AWS account and source code"] --> B["Create network and RDS MySQL"]
    B --> C["Package backend source bundle"]
    C --> D["Create Elastic Beanstalk environment"]
    D --> E["Run Prisma migration"]
    E --> F["Deploy frontend to Amplify"]
    F --> G["Add /api rewrite rule"]
    G --> H["Test login and core workflows"]
    H --> I["Check CloudWatch Logs and clean up"]
{{< /mermaid >}}

## AWS services in scope

| Service | Purpose |
| --- | --- |
| AWS Amplify Hosting | Host and build the React frontend. |
| Application Load Balancer | Public entry point for backend requests. |
| AWS Elastic Beanstalk | Run and manage the Node.js backend. |
| Amazon RDS for MySQL | Store application data. |
| Amazon S3 | Production-ready storage target for uploaded files. |
| Amazon SES | Send OTP and email notifications. |
| Amazon CloudWatch | Store logs and support monitoring. |

## Demo limitations

This workshop is intentionally scoped for a demo environment:

- RDS can use Single-AZ to reduce cost.
- Backend can run with one instance.
- Amplify uses the default domain.
- No Route 53 custom domain is required.
- Uploads may use local storage in the current codebase, while S3 is documented as the production-ready improvement.
