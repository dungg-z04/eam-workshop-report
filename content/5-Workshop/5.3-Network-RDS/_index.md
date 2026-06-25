---
title: "Prepare network and RDS"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

## Prepare network and RDS

In this step, you will prepare the network baseline and create an Amazon RDS for MySQL database. The database should not be publicly accessible.

## Target network layout

{{< mermaid >}}
flowchart LR
    Internet["Internet"] --> IGW["Internet Gateway"]
    IGW --> Public["Public Subnets\n2 Availability Zones"]
    Public --> ALB["Application Load Balancer"]
    Public --> NAT["NAT Gateway"]
    NAT --> Private["Private Subnets\n2 Availability Zones"]
    Private --> EB["Elastic Beanstalk Instance"]
    Private --> RDS["RDS MySQL"]
{{< /mermaid >}}

## Step 1: Select or create a VPC

Use an existing VPC if it already has:

- An Internet Gateway.
- At least two public subnets across two Availability Zones.
- At least two private subnets across two Availability Zones.
- A NAT Gateway in a public subnet.
- Route tables configured for public and private routing.

If your account does not have a suitable VPC, create one using the VPC console.

## Step 2: Create security groups

Create separate security groups for the load balancer, backend, and database.

| Security group | Inbound rule | Purpose |
| --- | --- | --- |
| `eam-alb-sg` | HTTP `80` from `0.0.0.0/0` | Allow users and Amplify rewrite traffic to reach the ALB. |
| `eam-backend-sg` | HTTP from `eam-alb-sg` | Allow only ALB traffic to reach the backend. |
| `eam-rds-sg` | MySQL `3306` from `eam-backend-sg` | Allow only backend traffic to reach the database. |

{{% notice warning %}}
Do not open MySQL port `3306` to `0.0.0.0/0`. RDS should stay private.
{{% /notice %}}

## Step 3: Create Amazon RDS for MySQL

Open the Amazon RDS console and create a database:

1. Choose **Create database**.
2. Select **Standard create**.
3. Choose **MySQL** as the engine.
4. Choose a low-cost **Dev/Test** template if available.
5. Set DB instance identifier, for example `eam-mysql-demo`.
6. Set master username, for example `asset_app`.
7. Set a strong password and store it securely.
8. Choose a small instance class for demo usage.
9. Set storage to a small size suitable for testing.
10. In **Connectivity**, select the target VPC.
11. Select a DB subnet group that uses private subnets.
12. Set **Public access** to **No**.
13. Attach `eam-rds-sg`.
14. Enable storage encryption.
15. Set the initial database name:

```text
enterprise_asset_management
```

Wait until the database status becomes **Available**.

## Step 4: Record connection information

After RDS is available, record:

- RDS endpoint
- Port, usually `3306`
- Database name
- Username
- Password

Build the backend `DATABASE_URL`:

```env
DATABASE_URL=mysql://asset_app:<password>@<rds-endpoint>:3306/enterprise_asset_management
```

## Step 5: Validate security

Before continuing, check:

- RDS public access is **No**.
- RDS inbound rule only allows `3306` from the backend security group.
- Backend security group only allows traffic from the ALB security group.
- ALB is attached to public subnets.

## Expected result

At the end of this step, the project has a private MySQL database ready for the backend deployment.
