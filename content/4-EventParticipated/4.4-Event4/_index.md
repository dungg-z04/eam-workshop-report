---
title: "Event 4: AWS Security, Monitoring and Cloud Practitioner Sharing"
date: 2026-07-11
weight: 4
chapter: false
pre: " <b> 4.4. </b> "
---

## Event Information

| Item | Details |
| --- | --- |
| Date | July 11, 2026 |
| Location | 26th floor, Bitexco Financial Tower |
| Participation format | In person |
| Role | Attendee |
| Main topics | AWS Security Agent, web application security, SLA, monitoring, CloudWatch, SNS, AWS Cloud Practitioner, and AWS certification learning path |

## Overview

The **AWS Security, Monitoring and Cloud Practitioner Sharing** event focused on web application security, system monitoring, and AWS certification orientation for students and beginners in cloud computing. The event included three main parts: securing web applications with AWS Security Agent, monitoring systems from SLA to real user experience, and preparing for the AWS Certified Cloud Practitioner exam.

The session helped me understand that a cloud system is not complete just because it can be deployed. It also needs proper monitoring, early security risk detection, and a response process when incidents occur.

For the EAM Workspace project, the event was directly relevant because the system also needs web application protection, backend status checks, API health testing, login error monitoring, alert configuration, and a clear understanding of the AWS services used in the deployment architecture.

## Main Content

### 1. Securing Your Web Apps With AWS Security Agent

The first session focused on web application security with AWS Security Agent. The speaker started by explaining several limitations of traditional security testing. Manual penetration testing can take a lot of time, cost more, depend heavily on the tester's experience, and may not provide consistent coverage across the entire system.

AWS Security Agent was introduced as a new approach to application security. With support from Amazon Bedrock, an agent can reason, plan, and perform security-related tasks such as design review, source code review, secret exposure detection, and simulated attack testing against a running application.

An important point is that Security Agent can support multiple stages of the software development lifecycle. During design, it can analyze architecture documents or Infrastructure as Code to check security alignment. During development, it can review Pull Requests and warn about insecure patterns. During testing, it can support automated penetration testing and provide evidence for engineers to verify.

However, the session also emphasized that Security Agent does not fully replace humans. It may still struggle with complex authentication flows, business logic issues that require deep context, or large testing scopes. Therefore, teams need to define the testing scope clearly, monitor cost, and combine agent output with human review for important decisions.

This session helped me understand that modern application security should be integrated earlier into the development process instead of being performed only at the end of a project. This aligns with the shift-left security mindset and helps reduce risk before a system reaches production.

### 2. SLA and Monitoring - From SLA to Monitoring What Really Matters

The second session focused on SLA and monitoring in system operations. The speaker used a practical scenario: the AWS Console may show that resources are healthy, servers are still running, and CPU or memory metrics look normal, but users may still be unable to log in. This shows that monitoring should not stop at infrastructure metrics; it should also measure real user experience.

SLA, or Service Level Agreement, was explained as a service commitment between a provider and customers. SLA helps define expectations, increase accountability, and support risk management. However, AWS SLA mainly applies to AWS-managed cloud services, while the final user experience still depends on how the application is designed, deployed, and operated.

One useful model from this session was the **Monitoring Pyramid**. The lower layer includes infrastructure metrics such as CPU, memory, disk, network, EC2, RDS, or ALB status. The next layer includes application metrics such as latency, error rate, and request count. Above that are business metrics such as login success rate, successful transactions, or failed requests. The highest layer is customer experience, meaning whether users can actually log in, perform actions, and complete business workflows.

The demo showed that a health check endpoint can return `200 OK` and ALB targets can remain healthy, while the login endpoint still fails if the backend cannot connect to the database. The key message was that healthy infrastructure does not always mean happy user experience.

The speaker also explained an alerting flow from custom metrics to alerts. For example, a system can record `LoginFailure` or `LoginSuccessRate`, create a CloudWatch Alarm with a suitable threshold, and send notifications through Amazon SNS to email or chat channels when the threshold is exceeded.

I connected this directly to EAM Workspace. Checking `/api/health` is necessary after deployment, but it is not enough. The system should also verify important user flows such as login, asset listing, asset assignment, support request creation, and email OTP delivery.

### 3. Inside The Exam: AWS Cloud Practitioner

The third session focused on the **AWS Certified Cloud Practitioner** certification, a foundational certification for beginners learning AWS. The speaker introduced the exam structure, major knowledge domains, and a practical learning approach to avoid being overwhelmed by the large number of AWS services.

The AWS Certified Cloud Practitioner exam includes 65 questions, a 90-minute duration, and a passing score of 700 out of 1000. The certification is valid for three years. The exam focuses on cloud concepts, the shared responsibility model, security, core AWS services, billing, pricing, and support.

The main exam domains include:

- **Cloud Concepts**: cloud concepts, benefits of the AWS Cloud, and deployment models.
- **Security and Compliance**: Shared Responsibility Model, IAM, security groups, network ACLs, AWS Shield, AWS WAF, and AWS Artifact.
- **Cloud Technology and Services**: compute, storage, database, networking, and services such as EC2, Lambda, S3, RDS, DynamoDB, VPC, and Route 53.
- **Billing, Pricing and Support**: Cost Explorer, AWS Budgets, pricing models, and AWS Support plans.

A useful learning tip was to study AWS services by keyword and use case. When learning a service, learners should connect it to a real scenario. For example, decoupling microservices can be associated with Amazon SQS, cost management can be associated with Cost Explorer or AWS Budgets, and relational databases can be associated with Amazon RDS.

The speaker also emphasized reviewing incorrect answers in mock exams. Doing many practice tests is less important than understanding why one answer is correct and why the others are wrong. Hands-on practice with AWS Free Tier services such as EC2, S3, IAM, and RDS also helps make theory easier to understand.

This session helped me understand the role of AWS Cloud Practitioner in a cloud learning path. It is a suitable first step for organizing foundational knowledge before moving on to deeper certifications such as Solutions Architect, Developer, or SysOps Administrator.

## Lessons Learned

- Web application security should be integrated throughout the software development lifecycle, from design and coding to runtime testing.
- AI agents can support design review, code review, and penetration testing, but humans still need to control scope, cost, and final decisions.
- Monitoring is not only about CPU, memory, or server status; it should also measure real user experience.
- Healthy infrastructure does not always mean happy user experience; systems need business-related metrics such as login success rate, error rate, or OTP success rate.
- CloudWatch, custom metrics, CloudWatch Alarm, and SNS can be combined to build early alerting flows for user-impacting issues.
- AWS Cloud Practitioner is a suitable foundational certification for organizing AWS knowledge before learning deeper certification paths.
- AWS services should be learned together with real use cases so they are easier to understand, remember, and apply to projects.

## Conclusion

The AWS Security, Monitoring and Cloud Practitioner Sharing event provided useful knowledge about web application security, system monitoring, and AWS certification planning. The three sessions complemented one another and helped me understand that an effective cloud system needs more than a successful deployment. It also needs security, meaningful monitoring, and operations based on user experience.

These lessons can be applied directly to the EAM Workspace project, especially in API health checks, login error monitoring, alert configuration, web application protection, and understanding the role of each AWS service in the deployment architecture.

## Event Images

Some images captured during the event:

<div class="event-gallery event-gallery-compact">
  <img src="/eam-workshop-report/images/4-EventParticipated/4.4-Event4/1784259526237_64486502297271719_8743030703712121879_f013b97836efa82730a725e22d470514.jpg" alt="AWS Security, Monitoring and Cloud Practitioner Sharing">
  <img src="/eam-workshop-report/images/4-EventParticipated/4.4-Event4/1784259526320_64486502297271719_8743030703712121879_b294dc252bc3541b272e973dd6a59c9f.jpg" alt="AWS Security, Monitoring and Cloud Practitioner Sharing">
  <img src="/eam-workshop-report/images/4-EventParticipated/4.4-Event4/1784259526349_64486502297271719_8743030703712121879_93c10150d149f5b0b3fe189ca88a9bf4.jpg" alt="AWS Security, Monitoring and Cloud Practitioner Sharing">
  <img src="/eam-workshop-report/images/4-EventParticipated/4.4-Event4/1784259526441_64486502297271719_8743030703712121879_1c55ea8f67e8b9373d603e8bdbee1a42.jpg" alt="AWS Security, Monitoring and Cloud Practitioner Sharing">
  <img src="/eam-workshop-report/images/4-EventParticipated/4.4-Event4/1784259526559_64486502297271719_8743030703712121879_d54d53cee3548cb6e264a2e0cfa016be.jpg" alt="AWS Security, Monitoring and Cloud Practitioner Sharing">
  <img src="/eam-workshop-report/images/4-EventParticipated/4.4-Event4/1784259526599_64486502297271719_8743030703712121879_290eb3a4e9e1b8040a7ff79de5a858f4.jpg" alt="AWS Security, Monitoring and Cloud Practitioner Sharing">
  <img src="/eam-workshop-report/images/4-EventParticipated/4.4-Event4/1784259526617_64486502297271719_8743030703712121879_12bc9fb98e59012a5daab6aab04adb17.jpg" alt="AWS Security, Monitoring and Cloud Practitioner Sharing">
</div>
