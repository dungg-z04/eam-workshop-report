---
title: "Chuáº©n bá»‹ network vÃ  RDS"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

## Chuáº©n bá»‹ network vÃ  RDS

á»ž bÆ°á»›c nÃ y, chÃºng ta sáº½ chuáº©n bá»‹ network baseline vÃ  táº¡o Amazon RDS for MySQL. Database khÃ´ng nÃªn public ra Internet.

## MÃ´ hÃ¬nh network má»¥c tiÃªu

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

## BÆ°á»›c 1: Chá»n hoáº·c táº¡o VPC

DÃ¹ng VPC cÃ³ sáºµn náº¿u VPC Ä‘Ã³ Ä‘Ã£ cÃ³:

- Internet Gateway.
- Ãt nháº¥t hai public subnet á»Ÿ hai Availability Zone.
- Ãt nháº¥t hai private subnet á»Ÿ hai Availability Zone.
- NAT Gateway náº±m trong public subnet.
- Route table Ä‘Æ°á»£c cáº¥u hÃ¬nh cho public vÃ  private routing.

Náº¿u AWS account chÆ°a cÃ³ VPC phÃ¹ há»£p, hÃ£y táº¡o VPC má»›i trong VPC console.

## BÆ°á»›c 2: Táº¡o security group

Táº¡o cÃ¡c security group riÃªng cho load balancer, backend vÃ  database.

| Security group | Inbound rule | Má»¥c Ä‘Ã­ch |
| --- | --- | --- |
| `eam-alb-sg` | HTTP `80` tá»« `0.0.0.0/0` | Cho phÃ©p user vÃ  Amplify rewrite traffic Ä‘i vÃ o ALB. |
| `eam-backend-sg` | HTTP tá»« `eam-alb-sg` | Chá»‰ cho ALB gá»i vÃ o backend. |
| `eam-rds-sg` | MySQL `3306` tá»« `eam-backend-sg` | Chá»‰ cho backend káº¿t ná»‘i database. |


## BÆ°á»›c 3: Táº¡o Amazon RDS for MySQL

Má»Ÿ Amazon RDS console vÃ  táº¡o database:

1. Chá»n **Create database**.
2. Chá»n **Standard create**.
3. Chá»n engine **MySQL**.
4. Chá»n template **Dev/Test** chi phÃ­ tháº¥p náº¿u cÃ³.
5. Äáº·t DB instance identifier, vÃ­ dá»¥ `eam-mysql-demo`.
6. Äáº·t master username, vÃ­ dá»¥ `asset_app`.
7. Äáº·t máº­t kháº©u máº¡nh vÃ  lÆ°u á»Ÿ nÆ¡i an toÃ n.
8. Chá»n instance class nhá» cho mÃ´i trÆ°á»ng demo.
9. Chá»n dung lÆ°á»£ng storage nhá» phÃ¹ há»£p Ä‘á»ƒ test.
10. á»ž **Connectivity**, chá»n VPC má»¥c tiÃªu.
11. Chá»n DB subnet group dÃ¹ng private subnet.
12. Äáº·t **Public access** lÃ  **No**.
13. Gáº¯n `eam-rds-sg`.
14. Báº­t storage encryption.
15. Äáº·t initial database name:

```text
enterprise_asset_management
```

Chá» database chuyá»ƒn sang tráº¡ng thÃ¡i **Available**.

## BÆ°á»›c 4: Ghi láº¡i thÃ´ng tin káº¿t ná»‘i

Sau khi RDS available, ghi láº¡i:

- RDS endpoint
- Port, thÆ°á»ng lÃ  `3306`
- Database name
- Username
- Password

Táº¡o backend `DATABASE_URL`:

```env
DATABASE_URL=mysql://asset_app:<password>@<rds-endpoint>:3306/enterprise_asset_management
```

## BÆ°á»›c 5: Kiá»ƒm tra báº£o máº­t

TrÆ°á»›c khi tiáº¿p tá»¥c, kiá»ƒm tra:

- RDS public access lÃ  **No**.
- Inbound rule cá»§a RDS chá»‰ cho `3306` tá»« backend security group.
- Backend security group chá»‰ nháº­n traffic tá»« ALB security group.
- ALB Ä‘Æ°á»£c gáº¯n vÃ o public subnet.

## Káº¿t quáº£ mong Ä‘á»£i

Káº¿t thÃºc bÆ°á»›c nÃ y, project cÃ³ má»™t MySQL database private sáºµn sÃ ng cho backend deployment.
