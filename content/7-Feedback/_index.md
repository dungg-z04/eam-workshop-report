---
title: "Sharing and Feedback"
date: 2026-07-05
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

# Sharing and Feedback

After participating in the **Workforce Bootcamp - First Cloud AI Journey** program at AWS, I had the opportunity to approach cloud computing in a more practical way. Before the program, I mainly knew AWS through concepts or separate documentation. After the program, I understood better how AWS services can work together to deploy a complete web application.

The part I appreciated most was that the program did not only require theoretical learning. It connected AWS learning with a project, blogs, events, workshop writing, and an individual report. Because of that, the learning process had a clearer direction: which service to learn, where it is used in the project, how to verify the result, and how to document the process.

## 1. Overall Evaluation

The First Cloud AI Journey program gave me a fairly complete path to start learning AWS, beginning with foundation topics such as AWS accounts, IAM, networking, compute, database, storage, monitoring, and cost awareness. These topics were then applied to the EAM Workspace project through frontend deployment, backend deployment, API Gateway, database setup, and email service configuration.

One strong point of the program is that the learning process was connected to real implementation. During the project deployment, I needed to understand:

- Why the frontend can be hosted with AWS Amplify.
- Why the backend needs a managed runtime environment such as Elastic Beanstalk.
- Why API Gateway is placed between the frontend and backend.
- Why the database is managed with Amazon RDS.
- Why OTP email requires SES/SMTP and separate credentials.
- Why CloudWatch/logging is important when checking deployment issues.

Because of this, I did not only remember AWS service names. I also understood the role of each service in a specific architecture.

## 2. AWS Learning Experience

During the program, I found that AWS learning becomes more effective when it is divided into smaller topics and connected with practice. For example, IAM helped me understand access control, VPC and Security Groups helped me understand networking, RDS helped me understand database endpoints and connection strings, and Elastic Beanstalk/Amplify helped me understand application deployment.

Reading Cloud Journey materials, AWS Blogs, and event content also helped me see AWS from different perspectives. AWS is not only used for deploying web apps. It is also related to security, AI/ML, containers, data analytics, automation, and operating systems at larger scale.

This motivated me to keep learning because AWS is a broad field with many possible directions after the internship.

## 3. AWS Deployment Experience

Deploying EAM Workspace to AWS was the part where I learned the most. When running the project locally, I mainly needed to make sure the application worked on my machine. When deploying to AWS, I had to care about more layers:

- Whether the frontend build output directory is correct.
- Whether Amplify rewrites `/api/*` to API Gateway correctly.
- Whether API Gateway points to the correct Elastic Beanstalk backend.
- Whether the backend reads the environment variables correctly.
- Whether RDS allows the backend to connect.
- Whether SES credentials match the SMTP username and password.
- Whether the health endpoint returns the expected result.

These issues helped me understand the difference between developing an application and deploying an application. A complete project needs code, configuration, cloud services, testing, and documentation.

## 4. Mentor and Program Support

I appreciated the mentor's support during both report writing and deployment. The mentor helped guide how to divide content, describe architecture, write workshop steps, add screenshot explanations, and verify configured AWS components.

One useful point was that the mentor often guided me to check the issue myself instead of only giving the answer directly. When I encountered deployment issues, environment variable issues, SES/SMTP issues, or API endpoint issues, this approach helped me practice checking each layer of the system and understand the cause more clearly.

The program also gave me opportunities to join events and read technical blogs. This helped me expand my knowledge beyond the project, especially in topics such as EKS, service mesh, security automation, AI, and how AWS is used in real-world problems.

## 5. Most Satisfying Part

The most satisfying part was that after the program, I did not only have a team project, but also a complete individual report in workshop format. This report records my AWS learning process, project work, cloud deployment, blog reading, event participation, and self-assessment.

I was also satisfied because I understood more clearly how a web application can be deployed on AWS using the model:

**Amplify Hosting -> API Gateway -> Elastic Beanstalk -> RDS**, with **SES** for email and **CloudWatch** for operational checking.

This knowledge is practical because it can be applied to many other web projects in the future.

## 6. Difficulties During The Program

Some difficulties I encountered included:

- At first, I was not familiar with organizing the report as a Hugo workshop.
- I was not used to writing worklog, proposal, blogs, events, workshop, and self-assessment in parallel.
- During AWS deployment, many parts had to be checked at the same time, such as endpoints, rewrite rules, environment variables, RDS connection, and SES credentials.
- Some issues were not in the code but in AWS service configuration, so it took time to identify the correct cause.
- Capturing workshop screenshots and writing explanations for each image took more time than expected.

However, these difficulties helped me become more careful. In cloud deployment, each configuration step should be documented clearly so it can be checked or repeated later.

## 7. Suggestions For The Program

I think the program could support students better by adding:

- A sample AWS deployment checklist for full-stack web projects, including frontend, backend, database, API Gateway, email, and monitoring.
- A dedicated session on reading logs and debugging AWS issues, especially CloudWatch, Elastic Beanstalk health, and API Gateway.
- A sample workshop template for AWS deployment so students can understand what to write, which screenshots to capture, and how to explain each step.
- A short guide on managing environment variables, secrets, and credentials safely during deployment.
- Small hands-on labs for IAM, VPC, RDS, and Elastic Beanstalk before students deploy their real projects.
- A cleanup checklist for AWS resources to avoid unexpected costs after the report is completed.

These additions would help students feel more confident when deploying projects and reduce the time spent on basic configuration issues.

## 8. Expectations After The Program

After the program, I would like to continue learning AWS with more hands-on practice. The topics I want to study further include:

- AWS CDK or Terraform for infrastructure as code.
- Advanced VPC, private subnets, NAT Gateway, and VPC Endpoints.
- CloudWatch Logs, metrics, alarms, and dashboards.
- S3, CloudFront, custom domains, and HTTPS.
- IAM policies, Secrets Manager, and security best practices.
- AWS cost optimization for demo and small production environments.

Overall, First Cloud AI Journey is a useful program for students who want to start with AWS. The program helped me understand that cloud is not only a place to deploy applications, but also a foundation for designing, operating, monitoring, and improving systems in a more professional way.
