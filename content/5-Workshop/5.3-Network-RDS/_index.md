---
title: "Prepare network and RDS"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

## Prepare Network and RDS

This step prepares the MySQL database for the backend. For a demo environment, the default VPC or an existing VPC can be used as long as the Elastic Beanstalk backend can connect to Amazon RDS through port `3306`.

## Target Connection Model

{{< mermaid >}}
graph LR
    APIGW["Amazon API Gateway"] --> EB["Elastic Beanstalk Backend"]
    EB --> SGBackend["Backend Security Group"]
    SGBackend --> RDS["Amazon RDS MySQL"]
    RDS --> SGRDS["RDS Security Group"]
{{< /mermaid >}}

## Step 1: Choose a VPC

Use one VPC for Elastic Beanstalk and RDS. The VPC should have:

- Subnets for the Elastic Beanstalk environment.
- A subnet group for RDS.
- Suitable Internet routing so the backend can receive public requests through Elastic Beanstalk.
- Separate security groups for backend and database.

For a short demo workshop, the setup can be simpler than a production multi-subnet architecture.

![VPC used by Elastic Beanstalk and RDS](/eam-workshop-report/images/5-Workshop/5.3-Network-RDS/5.3.1-vpc-subnets.png)

*Figure 5.3.1. VPC used by Elastic Beanstalk and RDS.*

The VPC and CIDR in this view should match the environment used by the backend and database. Elastic Beanstalk and RDS should be in the same VPC or have suitable routing for secure connectivity.

## Step 2: Create Security Groups

Create or verify these security groups:

| Security group | Inbound rule | Purpose |
| --- | --- | --- |
| `eam-backend-sg` | HTTP from the Internet or the selected Elastic Beanstalk configuration | Allow API Gateway to call the backend endpoint. |
| `eam-rds-sg` | MySQL `3306` from `eam-backend-sg` | Allow only the backend to connect to the database. |

The most important rule is that RDS should not open `3306` to the entire Internet. Only the backend security group should be allowed to access the database.

![Elastic Beanstalk backend security group](/eam-workshop-report/images/5-Workshop/5.3-Network-RDS/5.3.2-backend-security-group.png)

*Figure 5.3.2. Elastic Beanstalk backend security group.*

On the backend security group screen, record the Security group ID because it will be used as the source for the RDS inbound rule.

![RDS security group allowing backend MySQL access](/eam-workshop-report/images/5-Workshop/5.3-Network-RDS/5.3.3-rds-security-group.png)

*Figure 5.3.3. RDS security group allowing backend access to port 3306.*

On the RDS security group screen, ensure that the MySQL/Aurora `3306` inbound rule allows only the backend security group as the source, not `0.0.0.0/0`.

## Step 3: Create Amazon RDS for MySQL

Open the Amazon RDS console and create the database:

1. Choose **Create database**.
2. Choose **Standard create**.
3. Select **MySQL** as the engine.
4. Choose a **Dev/Test** or low-cost template.
5. Set the DB instance identifier, for example `eam-mysql-demo`.
6. Set the master username, for example `asset_app`.
7. Set a strong password and store it safely.
8. Choose a small instance class for the demo environment.
9. Choose a suitable storage size for testing.
10. In **Connectivity**, select the target VPC.
11. Choose an appropriate DB subnet group.
12. If possible, set **Public access** to **No**.
13. Attach `eam-rds-sg`.
14. Enable storage encryption if needed.
15. Set the initial database name:

```text
enterprise_asset_management
```

Wait until the database status becomes **Available**.

![RDS database in Available status](/eam-workshop-report/images/5-Workshop/5.3-Network-RDS/5.3.4-rds-available.png)

*Figure 5.3.4. RDS database in Available status.*

When the database status is `Available`, RDS is ready to accept connections. Continue with backend configuration only after this status is stable.

## Step 4: Record Connection Information

After RDS is available, record:

- RDS endpoint
- Port, usually `3306`
- Database name
- Username
- Password

Create the backend `DATABASE_URL`:

```env
DATABASE_URL=mysql://asset_app:<password>@<rds-endpoint>:3306/enterprise_asset_management
```

![RDS connectivity and security information](/eam-workshop-report/images/5-Workshop/5.3-Network-RDS/5.3.5-rds-connectivity.png)

*Figure 5.3.5. RDS connectivity and security information.*

In the Connectivity & security section, collect the correct endpoint, port, VPC, and security group. These values are used to create the Elastic Beanstalk `DATABASE_URL`.

## Step 5: Security Check

Before continuing, check:

- RDS does not expose the database port to the entire Internet.
- The RDS inbound rule allows `3306` only from the backend security group.
- Backend and RDS are in the same VPC or have suitable routing.
- Database username/password are stored safely and are not committed to source code.

## Expected Result

At the end of this step, the project has a MySQL database ready for the Elastic Beanstalk backend through `DATABASE_URL`.
