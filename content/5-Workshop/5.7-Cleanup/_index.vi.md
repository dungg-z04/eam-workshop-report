---
title: "Dá»n dáº¹p tÃ i nguyÃªn"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

## Dá»n dáº¹p tÃ i nguyÃªn

Sau khi hoÃ n thÃ nh workshop, cáº§n dá»n dáº¹p tÃ i nguyÃªn Ä‘á»ƒ trÃ¡nh phÃ¡t sinh chi phÃ­ AWS ngoÃ i dá»± kiáº¿n.


## BÆ°á»›c 1: XÃ³a Amplify app

1. Má»Ÿ AWS Amplify console.
2. Chá»n EAM frontend app.
3. XÃ³a app hoáº·c disconnect branch.
4. XÃ¡c nháº­n URL máº·c Ä‘á»‹nh cá»§a Amplify khÃ´ng cÃ²n serve á»©ng dá»¥ng.

## BÆ°á»›c 2: Terminate Elastic Beanstalk environment

1. Má»Ÿ Elastic Beanstalk.
2. Chá»n environment `eam-backend`.
3. Chá»n **Terminate environment**.
4. Chá» environment terminate hoÃ n toÃ n.
5. XÃ¡c nháº­n cÃ¡c EC2 instance liÃªn quan Ä‘Ã£ Ä‘Æ°á»£c xÃ³a.

Náº¿u Elastic Beanstalk táº¡o Application Load Balancer, target group vÃ  Auto Scaling resources, hÃ£y kiá»ƒm tra cÃ¡c tÃ i nguyÃªn Ä‘Ã³ Ä‘Ã£ Ä‘Æ°á»£c xÃ³a.

## BÆ°á»›c 3: XÃ³a Application Load Balancer náº¿u cáº§n

Náº¿u ALB Ä‘Æ°á»£c táº¡o thá»§ cÃ´ng:

1. Má»Ÿ EC2 console.
2. VÃ o **Load Balancers**.
3. XÃ³a EAM backend ALB.
4. VÃ o **Target Groups** vÃ  xÃ³a target group khÃ´ng cÃ²n dÃ¹ng.

## BÆ°á»›c 4: XÃ³a RDS database

1. Má»Ÿ RDS console.
2. Chá»n EAM MySQL database.
3. Chá»n **Delete**.
4. Vá»›i mÃ´i trÆ°á»ng demo, quyáº¿t Ä‘á»‹nh bá» qua hoáº·c giá»¯ final snapshot.
5. XÃ¡c nháº­n xÃ³a.


## BÆ°á»›c 5: Empty vÃ  xÃ³a S3 bucket

Náº¿u Ä‘Ã£ táº¡o S3 bucket:

1. Má»Ÿ S3 console.
2. Empty bucket.
3. XÃ³a bucket.
4. XÃ¡c nháº­n khÃ´ng cÃ²n file demo upload trong bucket.

## BÆ°á»›c 6: XÃ³a security group vÃ  network resource

XÃ³a cÃ¡c security group khÃ´ng cÃ²n dÃ¹ng:

- `eam-alb-sg`
- `eam-backend-sg`
- `eam-rds-sg`

Náº¿u báº¡n táº¡o VPC riÃªng chá»‰ cho workshop nÃ y, hÃ£y xÃ³a thÃªm:

- NAT Gateway
- Elastic IP gáº¯n vá»›i NAT Gateway
- Route tables
- Subnets
- Internet Gateway
- VPC

## BÆ°á»›c 7: Dá»n CloudWatch vÃ  secrets

Kiá»ƒm tra vÃ  xÃ³a cÃ¡c tÃ i nguyÃªn khÃ´ng cÃ²n dÃ¹ng:

- CloudWatch log groups
- CloudWatch alarms
- Secrets Manager secrets
- Parameter Store parameters
- CloudTrail trails chá»‰ táº¡o cho workshop

## Checklist dá»n dáº¹p cuá»‘i cÃ¹ng

- [ ] ÄÃ£ xÃ³a Amplify app.
- [ ] ÄÃ£ terminate Elastic Beanstalk environment.
- [ ] ÄÃ£ xÃ³a ALB vÃ  target groups náº¿u táº¡o thá»§ cÃ´ng.
- [ ] ÄÃ£ xÃ³a RDS database hoáº·c giá»¯ final snapshot.
- [ ] ÄÃ£ empty vÃ  xÃ³a S3 bucket.
- [ ] ÄÃ£ xÃ³a security group.
- [ ] ÄÃ£ xÃ³a network resource khÃ´ng cÃ²n dÃ¹ng.
- [ ] ÄÃ£ kiá»ƒm tra CloudWatch logs vÃ  alarms.
- [ ] ÄÃ£ xÃ³a secrets vÃ  parameters.

## Nháº¯c nhá»Ÿ vá» chi phÃ­

CÃ¡c tÃ i nguyÃªn thÆ°á»ng tiáº¿p tá»¥c phÃ¡t sinh chi phÃ­ lÃ :

- RDS database instances
- NAT Gateway
- Application Load Balancer
- EC2 instances
- Elastic IP addresses
- CloudWatch log retention

LuÃ´n kiá»ƒm tra AWS Billing console sau khi dá»n dáº¹p.
