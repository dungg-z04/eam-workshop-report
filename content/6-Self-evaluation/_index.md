---
title: "Self-Assessment"
date: 2026-07-05
weight: 6
chapter: false
pre: " <b> 6. </b> "
---

# Self-Assessment

During the internship period from **17/04/2026 to 10/07/2026** at **Amazon Web Services Vietnam Company Limited** in the **Workforce Bootcamp - First Cloud AI Journey** program, I had the opportunity to approach AWS in a more practical way through self-learning, events, AWS Blog reading, project deployment, and workshop documentation.

The project used in this report is **EAM Workspace - Enterprise Asset Management System**. Although I contributed to the frontend part of the project, the most important focus of the internship was learning how to bring a full-stack web application to AWS, understanding the role of each service in the deployment architecture, and documenting that process clearly.

## 1. Achievements

### 1.1. AWS Foundation Knowledge

At the beginning, I started with basic concepts such as **Cloud Computing**, **AWS Global Infrastructure**, **AWS Management Console**, **AWS Free Tier**, **AWS Budgets**, and cost control when using an AWS account.

Then I continued learning the main AWS service groups:

- **IAM**: users, groups, roles, policies, and the principle of least privilege.
- **Networking**: VPC, subnets, route tables, Internet Gateway, NAT Gateway, Security Groups, and Network ACLs.
- **Compute**: EC2, AMIs, instance types, Elastic IP, and how compute is used for backend workloads.
- **Database**: Amazon RDS for MySQL, endpoints, backups, database engines, and backend connectivity.
- **Storage**: Amazon S3, object storage, file upload, and future storage options for images/documents.
- **Deployment**: AWS Amplify Hosting, Elastic Beanstalk, API Gateway, and cloud deployment steps.
- **Monitoring/Security**: CloudWatch, CloudTrail, WAF, KMS, Secrets Manager, and system protection concepts.

Through this process, I understood that AWS is not only a place to rent servers. It is an ecosystem of services for building, deploying, monitoring, and protecting applications.

### 1.2. Applying AWS to EAM Workspace

The AWS deployment part was where I learned the most. Instead of only reading documentation, I saw how each AWS service was used in the project architecture:

- **AWS Amplify Hosting** was used to build and host the React/Vite frontend.
- **Amazon API Gateway** was used to create a public endpoint and route `/api/*` requests to the backend.
- **AWS Elastic Beanstalk** was used to deploy the Node.js/Express backend.
- **Amazon RDS for MySQL** was used to store the system's business data.
- **Amazon SES** was used for email/OTP through SMTP credentials.
- **CloudWatch** was used to check status, logs, and deployment issues.

This helped me understand the relationship between frontend, backend, database, and AWS services. A local application is not enough to be considered complete; when deploying to AWS, environment variables, endpoints, permissions, networking, database connections, build settings, rewrite rules, and backend health status must also be considered.

### 1.3. Deployment and Troubleshooting Skills

During deployment, I encountered and learned about practical issues such as:

- How to configure environment variables for Elastic Beanstalk.
- How to use Amazon SES SMTP username and password.
- How to test the backend health endpoint through API Gateway.
- How to configure Amplify rewrites so the frontend can call the API.
- How to identify whether an issue comes from the frontend, API Gateway, backend, or database.
- How to document deployment steps with screenshots and clear explanations.

These experiences helped me build a layered troubleshooting mindset. When a feature does not work, I need to check not only the code, but also AWS configuration, endpoints, networking, credentials, and deployment status.

### 1.4. Reading AWS Documentation and Summarizing Knowledge

During the internship, I read and summarized AWS Blog articles related to EKS, Istio Ambient Mesh, EKS Control Plane Egress, and AWS Continuum. Reading technical blogs helped me become more familiar with how AWS presents solutions, architectures, and operational problems in real environments.

The events I joined also expanded my view of AWS in different areas such as security, AI, containers, recruitment, workflow automation, and how enterprises apply cloud to operations.

From that, I realized that learning AWS is not only about using the console. It also requires reading documentation, selecting key ideas, understanding use cases, and connecting them back to the project.

### 1.5. Workshop and Report Writing Skills

One area where I improved clearly was turning a technical process into documentation. When writing the workshop for deploying EAM Workspace to AWS, I had to present each step in a clear order:

- The goal of each deployment step.
- The AWS service being used.
- The required configuration.
- The screenshot that should be captured.
- The expected result after each step.
- Common issues and how to verify them.

This helped me understand that good technical documentation should not only say what was done. It should also explain why it was done, where it was configured, how to verify it, and what the correct result should look like.

## 2. Self-Evaluation Table

| No. | Criteria | Description | Self-rating |
| --- | --- | --- | --- |
| 1 | AWS foundation | Understand core concepts of IAM, VPC, EC2, RDS, S3, CloudWatch, and AWS cost control | Fair |
| 2 | AWS deployment | Able to deploy a demo frontend, backend, API Gateway, RDS, and SES setup for the internship project | Fair |
| 3 | Cloud architecture understanding | Understand the user flow from Amplify to API Gateway, Elastic Beanstalk, and RDS | Fair |
| 4 | Deployment troubleshooting | Able to check endpoints, environment variables, health checks, rewrite rules, and database connections | Fair |
| 5 | AWS documentation reading | Able to read AWS Blog/documentation and rewrite the content in a clearer way | Good |
| 6 | Workshop writing | Able to describe deployment steps, add screenshots, and record validation results | Good |
| 7 | Cloud self-learning | Proactively learn AWS services based on project needs | Good |
| 8 | Teamwork | Coordinate with the team to understand frontend, backend, database, and deployment content | Fair |
| 9 | Progress management | Maintain worklog, proposal, blogs, events, workshop, and self-assessment in stages | Fair |
| 10 | Overall | Complete an individual report connected to the project and AWS learning process | Good |

## 3. Strengths

- I was proactive in learning AWS services needed for the project.
- I could connect AWS knowledge with the EAM Workspace deployment architecture.
- I could read technical documentation/blogs and turn them into clearer report content.
- I understood the basic full-stack deployment flow on AWS, including frontend, API, backend, and database.
- I improved my ability to write workshop steps, describe screenshots, and present validation results.

## 4. Areas For Improvement

- I need more practice with AWS CLI and Infrastructure as Code to reduce manual console configuration.
- I need to improve my ability to read CloudWatch Logs and debug backend issues in the cloud environment.
- I need deeper understanding of advanced networking such as private subnets, NAT Gateway, VPC Endpoints, and security best practices.
- I need to learn more about secret management, detailed IAM permissions, and separating dev/staging/production environments.
- I need to practice AWS cost optimization when designing deployment architectures.

## 5. Lessons Learned

Through the internship, I realized that AWS is not only a tool for deploying applications. It is also an approach to building systems that can be operated more reliably. When moving the project to AWS, I had to think more about architecture, access control, database connectivity, endpoints, monitoring, and scalability.

I also learned that cloud learning should go together with practice. If I only read documentation, services such as Amplify, API Gateway, Elastic Beanstalk, RDS, and SES may feel separate. When they are placed into a real project, the role of each service becomes much clearer.

Most importantly, writing the workshop helped me turn deployment experience into documentation. This is important in cloud work because every configuration step should be recorded clearly so that others can check, repeat, or improve it later.

## 6. Direction After The Internship

After the internship, I would like to continue learning AWS in more practical directions:

- Practice infrastructure deployment with AWS CDK or Terraform.
- Study VPC, private subnets, load balancers, security groups, and IAM policies in more depth.
- Add CloudWatch Logs, metrics, and alarms for the backend.
- Learn more about S3 upload, CloudFront, custom domains, and HTTPS.
- Practice database backup/restore and AWS cost optimization for demo environments.
- Continue improving EAM Workspace toward a more production-ready architecture.

Overall, the internship at AWS helped me gain a more practical view of cloud computing. I did not only learn AWS services separately, but also understood how to combine them to deploy a complete web system that can be tested and documented clearly.
