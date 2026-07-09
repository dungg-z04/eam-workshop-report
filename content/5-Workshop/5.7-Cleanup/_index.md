---
title: "Clean up resources"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

After completing the workshop for deploying **EAM Workspace** on AWS, unused resources should be cleaned up to avoid unexpected AWS charges. In this workshop, the main resources include **AWS Amplify Hosting**, **Amazon API Gateway**, **AWS Elastic Beanstalk**, **Amazon RDS for MySQL**, **Amazon SES**, security groups, and related logs/metrics.

Before deleting resources, capture the important screens for the report. These screenshots show that the project was deployed, tested, and has a clear cleanup plan.

### Workshop Summary

In this workshop, EAM Workspace was deployed as a full-stack web application on AWS:

- The React/Vite frontend was built and hosted with **AWS Amplify Hosting**.
- Frontend `/api/*` requests were routed to **Amazon API Gateway**.
- API Gateway forwarded requests to the backend running on **AWS Elastic Beanstalk**.
- The backend connected to **Amazon RDS for MySQL** for business data.
- Email/OTP functionality used **Amazon SES** through SMTP credentials.
- Deployment results were validated with the health endpoint, login page, dashboard, and key business screens.

After testing and capturing screenshots, the demo resources can be cleaned up in the order below.

## Step 1: Record Resources To Clean Up

Before deleting anything, record the names of resources created during the workshop:

| Resource Group | Name or Item To Check |
| --- | --- |
| Amplify app | Frontend app `quanlidoanhnghiep` or deployment branch `aws-architecture` |
| API Gateway | HTTP API `eam-backend-http-api` |
| Elastic Beanstalk | Backend environment, for example `eam-backend-prod-v8` |
| RDS | MySQL database used by EAM Workspace |
| SES | Email identity and SMTP credential used for email |
| CloudWatch | Logs/metrics related to Elastic Beanstalk or API |
| EC2/Security Group | Security groups for Elastic Beanstalk and RDS |

This list helps avoid deleting resources that do not belong to the workshop.

## Step 2: Delete or Disconnect the AWS Amplify App

AWS Amplify Hosting is used to build and publish the frontend. If the demo frontend is no longer needed, the app can be deleted or the deployment branch can be disconnected.

Steps:

1. Open the **AWS Amplify** console.
2. Select the frontend app, for example `quanlidoanhnghiep`.
3. Select the deployment branch, for example `aws-architecture`.
4. Go to **App settings** or **General settings** and delete the app.

![Amplify app cleanup](/eam-workshop-report/images/5-Workshop/5.7-Cleanup/5.7.1-amplify-cleanup.png)

*Figure 5.7.1. AWS Amplify app `quanlidoanhnghiep` and branch `aws-architecture`.*

## Step 3: Delete Amazon API Gateway

API Gateway is the public endpoint layer used by the frontend to call the backend. If the API is no longer used, delete it so the endpoint no longer receives requests.

Steps:

1. Open the **Amazon API Gateway** console.
2. Select the project HTTP API, for example `eam-backend-http-api`.
3. Check the `ANY /{proxy+}` route and the integration pointing to the Elastic Beanstalk backend.
4. Choose **Delete** if the API is no longer needed.
5. Check the API list again to confirm deletion.

After API Gateway is deleted, URLs in the form `https://...execute-api.ap-southeast-1.amazonaws.com/...` will no longer work.

![API Gateway cleanup](/eam-workshop-report/images/5-Workshop/5.7-Cleanup/5.7.2-api-gateway-cleanup.png)

*Figure 5.7.2. HTTP API `eam-backend-http-api` in Amazon API Gateway before deletion.*

## Step 4: Terminate the Elastic Beanstalk Environment

Elastic Beanstalk manages the Node.js/Express backend environment. It may create EC2 instances, load balancers, Auto Scaling resources, and security groups, so it should be terminated when no longer used.

Steps:

1. Open the **Elastic Beanstalk** console.
2. Select the backend environment, for example `eam-backend-prod-v8`.
3. Choose **Actions** -> **Terminate environment**.
4. Enter the environment name if AWS asks for confirmation.
5. Wait until the environment is fully terminated.
6. Check the EC2 console to make sure instances created by Elastic Beanstalk are stopped/deleted.

If Elastic Beanstalk cannot terminate because of dependencies, check related security groups, load balancers, or EC2 resources.

![Elastic Beanstalk cleanup](/eam-workshop-report/images/5-Workshop/5.7-Cleanup/5.7.3-eb-cleanup.png)

*Figure 5.7.3. Elastic Beanstalk environment `eam-backend-prod-v8` before termination. The screenshot shows that the backend environment was healthy, had its own domain, and could continue generating cost if left running.*

## Step 5: Delete or Stop Amazon RDS for MySQL

Amazon RDS is an important resource because database instances can continue to generate cost while running. Before deleting it, decide whether the demo data still needs to be kept.

Steps:

1. Open the **Amazon RDS** console.
2. Select the MySQL database used by EAM Workspace.
3. Create a snapshot first if the data must be kept.
4. Select database `eam-mysql` -> **Actions** -> **Delete**.
5. Confirm that the database changes to deleting/deleted status.
6. After RDS is deleted, check related security groups because they may no longer have dependencies and can be removed.

![RDS cleanup](/eam-workshop-report/images/5-Workshop/5.7-Cleanup/5.7.4-rds-cleanup.png)

*Figure 5.7.4. Amazon RDS database `eam-mysql` before cleanup. This resource needs careful attention because a database instance can still incur cost while it remains available.*

## Step 6: Check Amazon SES

Amazon SES is used to verify an email identity and create SMTP credentials for email/OTP. SES usually does not generate large costs if email volume is low, but the configuration should still be reviewed.

Steps:

1. Open the **Amazon SES** console.
2. Check the verified email identity.
3. Check the SMTP credential/IAM user created for SES.
4. If it is no longer used, delete the IAM user or credential related to SMTP.

![SES cleanup](/eam-workshop-report/images/5-Workshop/5.7-Cleanup/5.7.5-ses-cleanup.png)

*Figure 5.7.5. Verified Amazon SES email identity in the Singapore region.*

## Step 7: Delete Security Groups and Dependent Resources

After Elastic Beanstalk and RDS are deleted, check security groups that are no longer used.

Steps:

1. Open the **EC2** console.
2. Go to **Security Groups**.
3. Find security groups related to the Elastic Beanstalk backend and RDS.
4. Delete a security group only when no resources depend on it.
5. If AWS reports a dependency error, check EC2 instances, load balancers, RDS, or network interfaces.

Do not delete default security groups or security groups that are not related.

## Step 8: Check CloudWatch and Billing

After the main resources are cleaned up, check logs and costs.

Steps:

1. Open the **CloudWatch** console.
2. Check log groups related to Elastic Beanstalk or the backend.
3. Delete unused log groups or reduce retention if logs should be kept.
4. Open **Billing and Cost Management**.
5. Check Cost Explorer or Bills to confirm there are no unexpected costs.

The resources that should be checked most carefully for cost are RDS databases, EC2/Elastic Beanstalk, load balancers, NAT Gateways, Elastic IPs, and CloudWatch Logs.

![Billing check](/eam-workshop-report/images/5-Workshop/5.7-Cleanup/5.7.6-billing-check.png)

*Figure 5.7.6. Billing and Cost Management used to review costs after the AWS deployment.*

After cleaning up the main resources, verify cost status:

1. Open **Billing and Cost Management**.
2. Check **Cost summary** for the current month cost and end-of-month forecast.
3. Review **Cost breakdown** by service to identify any service that is still generating charges.
4. Pay special attention to Amazon RDS, EC2, Elastic Load Balancing, VPC, API Gateway, Amplify, and CloudWatch.
5. If the cost still increases unexpectedly after cleanup, return to each service and check for remaining resources.

## Final Cleanup Checklist

- Resource list recorded.
- Amplify app/branch screenshot captured before deletion or disconnect.
- Unused API Gateway deleted.
- Elastic Beanstalk environment terminated.
- RDS database deleted or stopped according to demo needs.
- SES identity and SMTP credential checked.
- Security groups without dependencies deleted.
- CloudWatch log groups checked.
- Billing/Cost Explorer checked after cleanup.
