---
title: "Sharing and Feedback"
date: 2026-07-06
weight: 7
chapter: false
pre: " <b> 7. </b> "
---


## 1. Overall Evaluation

### 1.1. Internship Environment

The program provided a professional learning environment with a clear direction. Instead of only learning cloud concepts in theory, I had to write weekly worklogs, study AWS materials, join events, read AWS Blogs, deploy a real project, and document the process in workshop format.

This structure helped me understand that working with cloud is not only about knowing service names. A learner also needs to understand what problem each service solves, where it belongs in the architecture, how it should be configured, and how to verify the result.

### 1.2. Mentor and Team Support

During the internship, I received useful support from the mentor and team admin. The mentor helped me organize the report content, present the AWS architecture, write workshop steps, draw the project architecture in a more reasonable way, and identify mistakes that my team and I had made during the process.

### 1.3. Relevance to My Major

The program was relevant to my Information Technology major because the internship tasks were directly connected to web application development and deployment. Through the EAM Workspace project, I worked with frontend, backend, database, authentication, OTP email, APIs, cloud hosting, and monitoring.

Before this program, when I ran a project locally, I mainly cared about whether the application worked on my machine. After deploying the project to AWS, I understood that a complete system requires many layers, including networking, compute, database, API gateway, email service, monitoring, security, and cost control.

### 1.4. Learning and Skill Development

During the program, I had the opportunity to study and practice several important AWS services, including:

- **IAM** for accounts, permissions, and credentials.
- **VPC, subnets, and Security Groups** for network access control.
- **Amazon RDS** for the MySQL database used by the backend.
- **Elastic Beanstalk** for deploying the Node.js backend.
- **API Gateway** as the intermediate layer between frontend and backend.
- **AWS Amplify Hosting** for deploying the frontend.
- **Amazon SES/SMTP** for sending OTP emails.
- **CloudWatch** for checking operational status and troubleshooting.
- **Billing and Cost Management** for tracking cloud spending.

Besides technical skills, I also practiced documentation, architecture explanation, screenshot annotation, and result verification. These are important skills when working on real projects.

### 1.5. Learning Culture and Community Spirit

One point I appreciated is that the program did not only focus on the project. It also encouraged students to read blogs, join events, and share what they learned. Reading AWS Blogs and joining technical sessions helped me see AWS from a broader perspective, beyond deploying a single web application.

Topics such as Amazon EKS, Istio Ambient Mesh, security automation, AI, and cloud operations helped me understand that AWS is a large ecosystem used in many real-world scenarios. This gave me more motivation to continue learning after the internship.

## 2. Personal Reflections

### 2.1. What I Was Most Satisfied With

The part I was most satisfied with was being able to view the project from a more practical deployment perspective. EAM Workspace was not only a local web application, but was deployed on AWS using the model:

**Amplify Hosting -> API Gateway -> Elastic Beanstalk -> Amazon RDS**

It also used **Amazon SES** for OTP email and health endpoint testing to confirm that the system worked correctly. This process helped me understand the role of each AWS service in a full-stack application architecture.

### 2.2. Challenges I Faced

The biggest challenge was that many parts had to be handled at the same time. When deploying to AWS, an issue could come from code, environment variables, security groups, endpoints, rewrite rules, SES credentials, or database configuration. Without experience, it was easy to debug in the wrong direction.

Writing the report in workshop format also took more time than I expected. Each step did not only need to work; it also needed a clear screenshot, a clear purpose, an explanation of the result, and enough detail for another reader to follow the process.

### 2.3. Would I Recommend This Program?

I would recommend this program to students who want to start learning AWS or understand how to deploy a web project to the cloud. It is suitable for students who already have basic programming knowledge and want to move toward deployment, operations, troubleshooting, and technical documentation.

However, to learn effectively, participants should be proactive in reading documentation, practicing by themselves, and noting the issues they encounter. AWS has many services and new concepts, so following steps without understanding the purpose would make it difficult to apply the knowledge to another project.

## 3. Expectations After the Program

After the internship, I want to continue learning AWS through more hands-on practice. Some topics I would like to study further include:

- Infrastructure as Code with AWS CDK, CloudFormation, or Terraform.
- Advanced VPC, private subnets, NAT Gateway, and VPC Endpoints.
- CloudWatch Logs, metrics, alarms, and dashboards.
- S3, CloudFront, custom domains, and HTTPS.
- IAM policies, Secrets Manager, and security best practices.
- AWS cost optimization for demo and small production environments.
- Containers and Kubernetes on AWS, especially Amazon EKS.

Overall, First Cloud AI Journey is a useful program for students who want to begin their AWS learning journey. It helped me understand that cloud is not only a place to deploy applications, but also a foundation for designing, operating, monitoring, and improving systems in a more professional way.
