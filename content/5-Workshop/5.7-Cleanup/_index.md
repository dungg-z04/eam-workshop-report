---
title: "Clean up resources"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

## Clean up resources

Clean up resources after the workshop to avoid unexpected AWS charges.


## Step 1: Delete Amplify app

1. Open the AWS Amplify console.
2. Select the EAM frontend app.
3. Delete the app or disconnect the branch.
4. Confirm that the Amplify default URL no longer serves the application.

## Step 2: Terminate Elastic Beanstalk environment

1. Open Elastic Beanstalk.
2. Select the `eam-backend` environment.
3. Choose **Terminate environment**.
4. Wait until the environment is fully terminated.
5. Confirm that related EC2 instances are removed.

If Elastic Beanstalk created the Application Load Balancer, target group, and Auto Scaling resources, verify that they are also removed.

## Step 3: Delete Application Load Balancer if needed

If the ALB was created manually:

1. Open the EC2 console.
2. Go to **Load Balancers**.
3. Delete the EAM backend ALB.
4. Go to **Target Groups** and delete unused target groups.

## Step 4: Delete RDS database

1. Open the RDS console.
2. Select the EAM MySQL database.
3. Choose **Delete**.
4. For demo environments, decide whether to skip or keep a final snapshot.
5. Confirm deletion.


## Step 5: Empty and delete S3 bucket

If an S3 bucket was created:

1. Open the S3 console.
2. Empty the bucket.
3. Delete the bucket.
4. Confirm that no uploaded demo files remain.

## Step 6: Delete security groups and network resources

Delete security groups that are no longer used:

- `eam-alb-sg`
- `eam-backend-sg`
- `eam-rds-sg`

If you created a dedicated VPC only for this workshop, also delete:

- NAT Gateway
- Elastic IP attached to NAT Gateway
- Route tables
- Subnets
- Internet Gateway
- VPC

## Step 7: Clean CloudWatch and secrets

Review and delete unused:

- CloudWatch log groups
- CloudWatch alarms
- Secrets Manager secrets
- Parameter Store parameters
- CloudTrail trails created only for the workshop

## Final cleanup checklist

- [ ] Amplify app deleted.
- [ ] Elastic Beanstalk environment terminated.
- [ ] ALB and target groups deleted if created manually.
- [ ] RDS database deleted or final snapshot kept.
- [ ] S3 bucket emptied and deleted.
- [ ] Security groups removed.
- [ ] Unused VPC resources removed.
- [ ] CloudWatch logs and alarms reviewed.
- [ ] Secrets and parameters removed.

## Cost reminder

The most common resources that continue generating cost are:

- RDS database instances
- NAT Gateway
- Application Load Balancer
- EC2 instances
- Elastic IP addresses
- CloudWatch log retention

Always check the AWS Billing console after cleanup.
