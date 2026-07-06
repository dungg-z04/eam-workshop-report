---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Deploying an Enterprise Asset Management System 

## A Cloud-Based Workspace for Managing Enterprise Assets

### 1. Executive Summary

The project topic is **EAM Workspace**, a web-based Enterprise Asset Management system deployed on AWS. The system focuses on the problem of managing office assets in a company, where information about devices, users, assignments, maintenance, and inventory needs to be tracked clearly, centrally, and accessibly.

EAM Workspace helps a company manage employees, departments, assets, assignments, maintenance requests, inventory sessions, reports, feedback, FAQ content, attendance records, login history, notifications, and support chat in one centralized workspace. Instead of storing information separately in spreadsheets, chat messages, or internal files, the system brings the main business workflows into one application with clear access control for administrators and employees.

The system was developed as a team project by five members. It includes a React frontend, a Node.js/Express backend, a MySQL database managed through Prisma, and an AWS deployment plan. This report focuses on building the UI, integrating APIs, learning AWS services, deploying the full-stack demo, and documenting the workshop during the internship period from **17/04/2026 to 10/07/2026**.

In the demo deployment, the AWS architecture uses AWS Amplify Hosting for the frontend, Amazon API Gateway as the public API layer, AWS Elastic Beanstalk for the Node.js backend, Amazon RDS for MySQL for business data, Amazon SES for outbound email, and Amazon CloudWatch for logging/monitoring. Services such as Amazon S3, AWS Secrets Manager, AWS Systems Manager Parameter Store, and AWS CloudTrail are included as future production-ready extensions.

### 2. System Purpose

EAM Workspace is used to help a company manage the full asset lifecycle, from creating and categorizing assets to assigning them to employees, recording maintenance, running inventory sessions, returning assets, and generating reports. It is suitable for companies that manage many office devices such as laptops, monitors, printers, peripheral devices, or assets that must be tracked by department and user.

For administrators, the system helps track asset lists, asset status, current users, assignment history, maintenance requests, inventory data, and summary reports. For employees, the system provides a self-service portal to view assigned assets, submit support requests, update profile information, and follow activities related to their assets.

The main goal of the project is not only to build a functional asset management web application, but also to practice deploying a full-stack system on AWS, configuring frontend-backend-database connectivity, testing a public environment, and controlling cost after deployment.

### 3. Problem Statement

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

The application is deployed to AWS so that the frontend, backend, database, and supporting services can run in a cloud environment that is easier to access, monitor, and extend. During the internship, AWS self-learning was carried out alongside product development, covering AWS accounts, IAM, networking, compute, database, storage, deployment, monitoring, and cost optimization.

#### Benefits

- Centralized asset lifecycle management from creation to assignment, maintenance, inventory, and reporting.
- Clear separation between administrator and employee workflows.
- Better security through authentication, role-based authorization, private database access, and controlled environment variables.
- Faster demo and deployment through managed AWS services.
- A clear upgrade path from an internal demo architecture to a more production-ready architecture.

### 4. Solution Architecture

The proposed AWS deployment architecture follows a simple full-stack web application model for an internal demo environment. The current deployment mode does not require Route 53 or a custom domain. Users access the default AWS Amplify Hosting URL, and frontend API calls are rewritten through `/api/*` to Amazon API Gateway. API Gateway then forwards requests to the backend running on AWS Elastic Beanstalk, and the backend connects to Amazon RDS for MySQL.

{{< mermaid >}}
flowchart LR
    User["User Browser"] --> Amplify["AWS Amplify Hosting\nReact Frontend"]
    Amplify --> Rewrite["Amplify Rewrite Rule\n/api/*"]
    Rewrite --> APIGW["Amazon API Gateway\nHTTP API"]
    APIGW --> EB["AWS Elastic Beanstalk\nNode.js Backend"]
    EB --> RDS["Amazon RDS for MySQL\nPrivate Subnet"]
    EB --> S3["Amazon S3\nProduction Extension"]
    EB --> SES["Amazon SES\nEmail / OTP"]
    EB --> SSM["SSM Parameter Store\nProduction Extension"]
    EB --> Secrets["AWS Secrets Manager\nProduction Extension"]
    EB --> CW["Amazon CloudWatch\nLogs and Alarms"]
    CloudTrail["AWS CloudTrail\nProduction Extension"] --> Audit["Audit Trail"]
{{< /mermaid >}}

#### AWS Services Used

- **AWS Amplify Hosting**: hosts and builds the React frontend from the deployment branch.
- **Amazon API Gateway HTTP API**: receives `/api/*` requests from Amplify and forwards them to the backend.
- **AWS Elastic Beanstalk**: runs the Node.js/Express backend with a managed deployment workflow.
- **Amazon EC2**: provides the compute instance managed by Elastic Beanstalk.
- **Amazon RDS for MySQL**: stores application data such as users, employees, assets, assignments, maintenance requests, inventory sessions, and reports.
- **Amazon S3**: stores asset images and uploaded files in the production-ready extension design.
- **Amazon SES**: sends OTP and notification emails.
- **AWS Secrets Manager**: planned for storing sensitive values such as application secrets or database credentials when moving beyond the demo setup.
- **AWS Systems Manager Parameter Store**: planned for storing runtime configuration values.
- **Amazon CloudWatch Logs and Alarms**: collects backend logs and supports operational monitoring.
- **AWS CloudTrail**: planned for recording AWS account activity for audit purposes.
- **AWS Systems Manager Session Manager**: planned for safer instance administration without opening public SSH access.

#### Application Components

- **Frontend**: React, Vite, Tailwind CSS, React Router, reusable UI components, Admin Portal and Employee Portal.
- **Backend**: Node.js, Express.js, Prisma ORM, JWT authentication, validation, centralized error handling, request logging, and REST API modules.
- **Database**: MySQL schema for users, employees, departments, assets, assignments, maintenance requests, inventory sessions, notifications, feedback, attendance, login history, and support chat.
- **Deployment**: AWS Amplify for frontend hosting, API Gateway for the API entry point, Elastic Beanstalk for backend hosting, RDS for database, and CloudWatch for logs.

### 5. Technical Implementation Plan

#### Phase 1: Requirement Analysis and UI Planning

- Analyze the asset management problem and define the core modules.
- Identify two user groups: administrators and employees.
- Design the main user flows for asset creation, assignment, return, maintenance, inventory, reporting, and employee self-service.
- Build reusable UI patterns for the Admin Portal.
- Study AWS fundamentals such as account setup, cost management, IAM, Regions, Availability Zones, and basic cloud concepts.

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
- Continue AWS self-learning on compute, storage, database, networking, and deployment services to prepare for the deployment phase.

#### Phase 4: AWS Deployment

- Create or reuse an Amazon RDS for MySQL database for the application.
- Configure security groups so the backend can access RDS through port `3306`.
- Deploy the backend to AWS Elastic Beanstalk with a Linux-compatible source bundle.
- Configure environment variables such as `DATABASE_URL`, `JWT_SECRET`, `PORT`, `FRONTEND_ORIGIN`, and mail settings.
- Run Prisma migration and optional seed data.
- Deploy the frontend to AWS Amplify Hosting.
- Configure Amazon API Gateway HTTP API to proxy requests to the Elastic Beanstalk backend.
- Configure Amplify rewrite rules from `/api/*` to the API Gateway endpoint and the SPA fallback to `index.html`.

#### Phase 5: Testing and Validation

- Verify `GET /api/health`.
- Test admin login and employee login.
- Test core CRUD workflows.
- Test asset assignment, return, maintenance request, inventory, and report views.
- Check CloudWatch Logs for backend errors.
- Confirm that CORS, API Gateway routes/stages/integration, and Amplify rewrite rules work correctly.
- Test image/avatar upload, inactive account handling, and the main demo flows.

### 6. Timeline and Milestones

| Period | Milestone | Expected Result |
| --- | --- | --- |
| Week 1 | Project orientation and AWS fundamentals | Frontend role, local environment, and basic AWS concepts are prepared. |
| Week 2 | React app and admin layout setup | Routes, sidebar, layout, and reusable base components are created. |
| Week 3 | Login, token handling, and API layer | Protected routes, token handling, and service layer are ready for backend integration. |
| Week 4 | Core admin CRUD screens | Asset, employee, department, form, and table screens are implemented. |
| Week 5 | Asset workflow development | Assignment, return, transfer, and maintenance workflows are developed. |
| Week 6 | Inventory, reporting, and data states | Inventory, reports, charts, empty states, and data states are completed. |
| Week 7 | UI experience refinement | Responsive layout, dark mode, loading states, toasts, and UI error handling are improved. |
| Week 8 | User portal and extended modules | Employee dashboard, assigned assets, FAQ, feedback, Excel import, and floor map are completed. |
| Week 9 | AWS deployment preparation | Production build, environment configuration, deployment documentation, and integration issues are reviewed. |
| Week 10 | AWS deployment | RDS, Elastic Beanstalk, API Gateway, and Amplify are deployed; the health endpoint and login flow are tested. |
| Week 11 | Production testing and workshop documentation | Integration issues are fixed, key screens are tested, workshop screenshots are captured, and deployment guidance is expanded. |
| Week 12 | Final report completion | The Hugo site, self-evaluation, sharing/feedback, cleanup section, and final submission materials are reviewed. |

### 7. Budget Estimation

The project is designed for an internal demo environment, so the first deployment prioritizes low cost over high availability. Final pricing should be verified with AWS Pricing Calculator before deployment because AWS prices vary by Region, instance type, storage size, and traffic volume.

| Service | Cost Optimization Choice |
| --- | --- |
| AWS Amplify Hosting | Use the default Amplify domain and deploy only the required branch. |
| Amazon API Gateway | Use a simple HTTP API for the `/api/*` route. |
| AWS Elastic Beanstalk / EC2 | Use one small instance for the demo environment. |
| Amazon RDS for MySQL | Use Single-AZ and a small dev/test instance class. |
| Amazon S3 | Store only required uploaded files and apply clean-up policies when needed. |
| Amazon SES | Use only for OTP and application email flows. |
| CloudWatch | Keep log retention limited for demo environments. |

Cost control actions:

- Use one AWS Region for all resources.
- Avoid Multi-AZ RDS during the demo phase.
- Avoid Route 53 and custom domain until production is required.
- Clean up Elastic Beanstalk, API Gateway, RDS, S3, and CloudWatch resources after the workshop.
- Do not keep unused deployment environments running.

### 8. Risk Assessment

| Risk | Impact | Probability | Mitigation |
| --- | --- | --- | --- |
| Wrong Amplify rewrite rule | Frontend cannot call backend APIs or static assets get MIME type errors | Medium | Place `/api/*` rewrite above the SPA fallback, avoid rewriting static assets incorrectly, and test `/api/health`. |
| Incorrect API Gateway route or stage | API returns 404 even when the backend is running | Medium | Check routes, integration, stage, and parameter mapping before testing the frontend. |
| Elastic Beanstalk port mismatch | Backend becomes unhealthy | Medium | Set `PORT=8080` and ensure the backend reads the port from environment variables. |
| RDS security group misconfiguration | Backend cannot connect to MySQL | Medium | Allow port `3306` only from the backend security group. |
| CORS error | Browser blocks API calls | Medium | Set `FRONTEND_ORIGIN` or `FRONTEND_ORIGINS` to the Amplify URL. |
| Missing or incorrect production environment variables | Login, upload, or health check fails | Medium | Standardize `DATABASE_URL`, `JWT_SECRET`, `FRONTEND_ORIGIN`, OTP/mail config, and validate each layer after deployment. |
| File upload persistence issue | Uploaded files may be lost when the instance is replaced | Medium | Use S3 private bucket for production-ready storage or clearly document local upload limitations in the demo. |
| Cost overrun | Unexpected AWS charges | Low to Medium | Use smallest demo resources, set budget alerts, and clean up resources after testing. |
| Incomplete test data | Demo flows cannot be shown smoothly | Medium | Run Prisma seed before demo and document demo accounts separately. |

### 9. Expected Outcomes

After completing this project and workshop, the expected outcomes are:

- A working Enterprise Asset Management application with Admin Portal and Employee Portal.
- A backend API that supports authentication, authorization, asset lifecycle workflows, reporting, notifications, feedback, attendance, and support chat.
- A MySQL database schema that stores the core business data of the system.
- A practical AWS deployment model using Amplify, API Gateway, Elastic Beanstalk, RDS, SES, and CloudWatch, with future extension directions for S3, Secrets Manager, and Parameter Store.
- A step-by-step workshop that another learner can follow to deploy and validate the system.
- A better understanding of full-stack deployment, cloud networking, environment variables, CORS, database connectivity, monitoring, and clean-up on AWS.

### 10. Future Improvements

- Move all uploaded files from local instance storage to Amazon S3.
- Add Route 53 and AWS Certificate Manager when a custom production domain is required.
- Enable RDS Multi-AZ for higher availability.
- Add Auto Scaling for the backend when traffic increases.
- Add Amazon ElastiCache for Redis if the application needs shared state for multiple backend instances.
- Add AWS WAF when the application becomes public-facing.
- Improve CI/CD and automated testing for both frontend and backend.
