---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Deploying an Enterprise Asset Management System on AWS

## A Cloud-Based Workspace for Managing Enterprise Assets

### 1. Executive Summary

EAM Workspace is an Enterprise Asset Management system designed to help a company manage employees, departments, assets, assignments, maintenance requests, inventory sessions, reports, feedback, FAQ content, attendance records, login history, notifications, and support chat in one centralized workspace.

The system was developed as a team project by five members. It includes a React frontend, a Node.js/Express backend, a MySQL database managed through Prisma, and a deployment plan on AWS. The workshop proposed in this report focuses on deploying the full-stack application to AWS using a low-cost and practical architecture for an internal demo environment.

The target AWS architecture uses AWS Amplify Hosting for the frontend, an Application Load Balancer and AWS Elastic Beanstalk for the backend, Amazon RDS for MySQL for persistent data, Amazon S3 for file storage in the production-ready design, Amazon SES for outbound email, and Amazon CloudWatch for logging and monitoring.

### 2. Problem Statement

#### Current Problem

Many small and medium-sized companies still manage office assets manually using spreadsheets, chat messages, or disconnected internal files. This approach creates several problems:

- Asset information is scattered and difficult to update.
- Administrators cannot easily track who is using each asset.
- Assignment, return, transfer, maintenance, and inventory history are hard to audit.
- Employees do not have a clear self-service portal to view their assigned assets or submit support requests.
- Reporting is slow because data must be collected and cleaned manually.
- File attachments, asset images, and feedback records are difficult to organize.

#### Proposed Solution

EAM Workspace solves these problems by providing a centralized web application with two main portals:

- **Admin Portal**: used by administrators to manage employees, departments, asset categories, assets, assignments, maintenance requests, inventory sessions, locations, reports, feedback, FAQ content, attendance history, login history, and support chat.
- **Employee Portal**: used by employees to view assigned assets, check asset details, submit support requests, view FAQ content, update profile information, change password, check personal history, and interact with support.

The application is deployed to AWS so that the frontend, backend, database, and supporting services can run in a cloud environment that is easier to access, monitor, and extend.

#### Benefits

- Centralized asset lifecycle management from creation to assignment, maintenance, inventory, and reporting.
- Clear separation between administrator and employee workflows.
- Better security through authentication, role-based authorization, private database access, and controlled environment variables.
- Faster demo and deployment through managed AWS services.
- A clear upgrade path from an internal demo architecture to a more production-ready architecture.

### 3. Solution Architecture

The proposed AWS deployment architecture follows a simple full-stack web application model for an internal demo environment. The current deployment mode does not require Route 53 or a custom domain. Users access the default AWS Amplify Hosting URL, and frontend API calls are proxied through Amplify rewrite rules to the backend Application Load Balancer.

{{< mermaid >}}
flowchart LR
    User["User Browser"] --> Amplify["AWS Amplify Hosting\nReact Frontend"]
    Amplify --> Rewrite["/api Rewrite Rule"]
    Rewrite --> ALB["Application Load Balancer\nPublic Subnets"]
    ALB --> EB["AWS Elastic Beanstalk\nNode.js Backend"]
    EB --> RDS["Amazon RDS for MySQL\nPrivate Subnet"]
    EB --> S3["Amazon S3\nPrivate Bucket"]
    EB --> SES["Amazon SES\nEmail / OTP"]
    EB --> SSM["SSM Parameter Store\nRuntime Config"]
    EB --> Secrets["AWS Secrets Manager\nSecrets"]
    EB --> CW["Amazon CloudWatch\nLogs and Alarms"]
    CloudTrail["AWS CloudTrail"] --> Audit["Audit Trail"]
{{< /mermaid >}}

#### AWS Services Used

- **AWS Amplify Hosting**: hosts and builds the React frontend.
- **Application Load Balancer**: receives HTTP traffic from Amplify rewrite rules and forwards it to the backend.
- **AWS Elastic Beanstalk**: runs the Node.js/Express backend with a managed deployment workflow.
- **Amazon EC2**: provides the compute instance managed by Elastic Beanstalk.
- **Amazon RDS for MySQL**: stores application data such as users, employees, assets, assignments, maintenance requests, inventory sessions, and reports.
- **Amazon S3**: stores asset images and uploaded files in the production-ready design.
- **Amazon SES**: sends OTP and notification emails.
- **AWS Secrets Manager**: stores sensitive values such as application secrets or database credentials when moving beyond the demo setup.
- **AWS Systems Manager Parameter Store**: stores runtime configuration values.
- **Amazon CloudWatch Logs and Alarms**: collects backend logs and supports operational monitoring.
- **AWS CloudTrail**: records AWS account activity for audit purposes.
- **AWS Systems Manager Session Manager**: supports safer instance administration without opening public SSH access.

#### Application Components

- **Frontend**: React, Vite, Tailwind CSS, React Router, reusable UI components, Admin Portal and Employee Portal.
- **Backend**: Node.js, Express.js, Prisma ORM, JWT authentication, validation, centralized error handling, request logging, and REST API modules.
- **Database**: MySQL schema for users, employees, departments, assets, assignments, maintenance requests, inventory sessions, notifications, feedback, attendance, login history, and support chat.
- **Deployment**: AWS Amplify for frontend hosting, Elastic Beanstalk for backend hosting, RDS for database, and CloudWatch for logs.

### 4. Technical Implementation Plan

#### Phase 1: Requirement Analysis and UI Planning

- Analyze the asset management problem and define the core modules.
- Identify two user groups: administrators and employees.
- Design the main user flows for asset creation, assignment, return, maintenance, inventory, reporting, and employee self-service.
- Build reusable UI patterns for the Admin Portal.

#### Phase 2: Backend and Database Foundation

- Design the MySQL schema with Prisma.
- Implement authentication, authorization, account status checks, and password handling.
- Build REST APIs for employees, departments, categories, assets, assignments, maintenance requests, inventory, reports, notifications, feedback, FAQ, attendance, login history, and support chat.
- Add seed data for demo accounts and sample business data.

#### Phase 3: Frontend Development

- Build Admin Portal screens for asset and organization management.
- Build Employee Portal screens for self-service workflows.
- Integrate API calls with the backend.
- Add loading, empty, error, and toast states.
- Review responsive behavior and dark/light mode.

#### Phase 4: AWS Deployment

- Create an Amazon RDS for MySQL database in private subnets.
- Create network components such as public/private subnets, Internet Gateway, NAT Gateway, and security groups if they are not already available.
- Deploy the backend to AWS Elastic Beanstalk behind an Application Load Balancer.
- Configure environment variables such as `DATABASE_URL`, `JWT_SECRET`, `PORT`, `FRONTEND_ORIGIN`, and mail settings.
- Run Prisma migration and optional seed data.
- Deploy the frontend to AWS Amplify Hosting.
- Configure Amplify rewrite rules from `/api/<*>` to the Application Load Balancer DNS name.

#### Phase 5: Testing and Validation

- Verify `GET /api/health`.
- Test admin login and employee login.
- Test core CRUD workflows.
- Test asset assignment, return, maintenance request, inventory, and report views.
- Check CloudWatch Logs for backend errors.
- Confirm that CORS and Amplify rewrite rules work correctly.

### 5. Timeline and Milestones

| Period | Milestone | Expected Result |
| --- | --- | --- |
| Week 1 - Week 2 | Requirement analysis and UI planning | Main modules, roles, and navigation structure are defined. |
| Week 3 - Week 4 | Backend foundation and database schema | Authentication, Prisma schema, and core API structure are ready. |
| Week 5 - Week 7 | Admin Portal development | Dashboard, asset, employee, department, category, assignment, maintenance, inventory, and report screens are implemented. |
| Week 8 - Week 9 | Employee Portal and workflow integration | Employee dashboard, assigned assets, support requests, FAQ, profile, and history pages are integrated. |
| Week 10 | AWS architecture and deployment preparation | Deployment guide, environment variables, source bundle, and AWS service plan are prepared. |
| Week 11 | AWS deployment and validation | Frontend and backend are deployed, connected to RDS, and tested end-to-end. |
| Week 12 | Documentation and workshop finalization | Workshop content, testing evidence, clean-up steps, and final report are completed. |

### 6. Budget Estimation

The project is designed for an internal demo environment, so the first deployment prioritizes low cost over high availability. Final pricing should be verified with AWS Pricing Calculator before deployment because AWS prices vary by Region, instance type, storage size, and traffic volume.

| Service | Cost Optimization Choice |
| --- | --- |
| AWS Amplify Hosting | Use the default Amplify domain and deploy only the required branch. |
| AWS Elastic Beanstalk / EC2 | Use one small instance for the demo environment. |
| Application Load Balancer | Use one ALB for backend traffic. |
| Amazon RDS for MySQL | Use Single-AZ and a small dev/test instance class. |
| Amazon S3 | Store only required uploaded files and apply clean-up policies when needed. |
| Amazon SES | Use only for OTP and application email flows. |
| CloudWatch | Keep log retention limited for demo environments. |

Cost control actions:

- Use one AWS Region for all resources.
- Avoid Multi-AZ RDS during the demo phase.
- Avoid Route 53 and custom domain until production is required.
- Clean up Elastic Beanstalk, RDS, S3, ALB, and CloudWatch resources after the workshop.
- Do not keep unused deployment environments running.

### 7. Risk Assessment

| Risk | Impact | Probability | Mitigation |
| --- | --- | --- | --- |
| Wrong Amplify rewrite rule | Frontend cannot call backend APIs | Medium | Place `/api/<*>` rewrite above the SPA fallback rule and test `/api/health`. |
| Elastic Beanstalk port mismatch | Backend becomes unhealthy | Medium | Set `PORT=8080` and ensure the backend reads the port from environment variables. |
| RDS security group misconfiguration | Backend cannot connect to MySQL | Medium | Allow port `3306` only from the backend security group. |
| CORS error | Browser blocks API calls | Medium | Set `FRONTEND_ORIGIN` or `FRONTEND_ORIGINS` to the Amplify URL. |
| File upload persistence issue | Uploaded files may be lost when the instance is replaced | Medium | Use S3 private bucket for production-ready storage or clearly document local upload limitations in the demo. |
| Cost overrun | Unexpected AWS charges | Low to Medium | Use smallest demo resources, set budget alerts, and clean up resources after testing. |
| Incomplete test data | Demo flows cannot be shown smoothly | Medium | Run Prisma seed before demo and document demo accounts separately. |

### 8. Expected Outcomes

After completing this project and workshop, the expected outcomes are:

- A working Enterprise Asset Management application with Admin Portal and Employee Portal.
- A backend API that supports authentication, authorization, asset lifecycle workflows, reporting, notifications, feedback, attendance, and support chat.
- A MySQL database schema that stores the core business data of the system.
- A practical AWS deployment model using Amplify, ALB, Elastic Beanstalk, RDS, S3, SES, CloudWatch, Secrets Manager, and Parameter Store.
- A step-by-step workshop that another learner can follow to deploy and validate the system.
- A better understanding of full-stack deployment, cloud networking, environment variables, CORS, database connectivity, monitoring, and clean-up on AWS.

### 9. Future Improvements

- Move all uploaded files from local instance storage to Amazon S3.
- Add Route 53 and AWS Certificate Manager when a custom production domain is required.
- Enable RDS Multi-AZ for higher availability.
- Add Auto Scaling for the backend when traffic increases.
- Add Amazon ElastiCache for Redis if the application needs shared state for multiple backend instances.
- Add AWS WAF when the application becomes public-facing.
- Improve CI/CD and automated testing for both frontend and backend.
