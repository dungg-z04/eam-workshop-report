---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Triá»ƒn khai EAM Workspace trÃªn AWS

#### Tá»•ng quan

Trong workshop nÃ y, chÃºng ta sáº½ triá»ƒn khai **EAM Workspace**, má»™t há»‡ thá»‘ng quáº£n lÃ½ tÃ i sáº£n doanh nghiá»‡p, lÃªn AWS. á»¨ng dá»¥ng bao gá»“m frontend React, backend Node.js/Express vÃ  cÆ¡ sá»Ÿ dá»¯ liá»‡u MySQL Ä‘Æ°á»£c quáº£n lÃ½ báº±ng Prisma.

Kiáº¿n trÃºc má»¥c tiÃªu Ä‘Æ°á»£c thiáº¿t káº¿ cho mÃ´i trÆ°á»ng demo ná»™i bá»™. Kiáº¿n trÃºc sá»­ dá»¥ng cÃ¡c dá»‹ch vá»¥ managed cá»§a AWS Ä‘á»ƒ viá»‡c triá»ƒn khai Ä‘Æ¡n giáº£n, thá»±c táº¿ vÃ  kiá»ƒm soÃ¡t chi phÃ­ tá»‘t hÆ¡n:

- **AWS Amplify Hosting** cho frontend React.
- **Application Load Balancer** lÃ m entry point public cho backend.
- **AWS Elastic Beanstalk** Ä‘á»ƒ cháº¡y backend Node.js/Express.
- **Amazon RDS for MySQL** Ä‘á»ƒ lÆ°u dá»¯ liá»‡u á»©ng dá»¥ng.
- **Amazon S3** cho thiáº¿t káº¿ lÆ°u trá»¯ file sáºµn sÃ ng production.
- **Amazon SES** cho OTP vÃ  email flow.
- **Amazon CloudWatch** cho log vÃ  monitoring cÆ¡ báº£n.

Workshop nÃ y Ä‘i theo hÆ°á»›ng triá»ƒn khai demo: khÃ´ng dÃ¹ng Route 53, khÃ´ng dÃ¹ng custom domain vÃ  khÃ´ng dÃ¹ng Amazon Cognito. XÃ¡c thá»±c hiá»‡n do backend xá»­ lÃ½ báº±ng JWT.

#### Kiáº¿n trÃºc

{{< mermaid >}}
flowchart LR
    User["TrÃ¬nh duyá»‡t ngÆ°á»i dÃ¹ng"] --> Amplify["AWS Amplify Hosting\nReact Frontend"]
    Amplify --> Rewrite["Rewrite /api"]
    Rewrite --> ALB["Application Load Balancer"]
    ALB --> EB["Elastic Beanstalk\nNode.js Backend"]
    EB --> RDS["Amazon RDS MySQL\nPrivate Subnet"]
    EB --> S3["Amazon S3\nPrivate Bucket"]
    EB --> SES["Amazon SES"]
    EB --> CW["CloudWatch Logs"]
{{< /mermaid >}}

#### Ná»™i dung

1. [Tá»•ng quan workshop](5.1-Workshop-overview/)
2. [Chuáº©n bá»‹](5.2-Prerequisites/)
3. [Chuáº©n bá»‹ network vÃ  RDS](5.3-Network-RDS/)
4. [Triá»ƒn khai backend báº±ng Elastic Beanstalk](5.4-Backend-Elastic-Beanstalk/)
5. [Triá»ƒn khai frontend báº±ng Amplify Hosting](5.5-Frontend-Amplify/)
6. [Kiá»ƒm thá»­, monitoring vÃ  xá»­ lÃ½ lá»—i](5.6-Test-Monitor/)
7. [Dá»n dáº¹p tÃ i nguyÃªn](5.7-Cleanup/)
