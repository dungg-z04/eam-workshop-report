---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# SESSION POLICIES TRONG AMAZON EKS POD IDENTITY

Amazon EKS Pod Identity vá»«a bá»• sung tÃ­nh nÄƒng session policies, cho phÃ©p báº¡n thu háº¹p quyá»n IAM má»™t cÃ¡ch linh hoáº¡t vÃ  chÃ­nh xÃ¡c cho tá»«ng pod mÃ  khÃ´ng cáº§n táº¡o thÃªm nhiá»u IAM roles riÃªng biá»‡t. ÄÃ¢y lÃ  bÆ°á»›c tiáº¿n quan trá»ng giÃºp Ã¡p dá»¥ng nguyÃªn táº¯c least privilege hiá»‡u quáº£ hÆ¡n trong mÃ´i trÆ°á»ng Kubernetes quy mÃ´ lá»›n.

CÃ¡c Ä‘iá»ƒm chÃ­nh cáº§n náº¯m:

* Session policy lÃ  má»™t IAM policy inline Ä‘Æ°á»£c chá»‰ Ä‘á»‹nh khi táº¡o hoáº·c cáº­p nháº­t Pod Identity association.
* Quyá»n hiá»‡u quáº£ = intersection (giao) giá»¯a permissions cá»§a IAM role vÃ  session policy â†’ session policy chá»‰ cÃ³ thá»ƒ thu háº¹p, khÃ´ng thá»ƒ má»Ÿ rá»™ng quyá»n.
* GiÃºp trÃ¡nh tÃ¬nh tráº¡ng over-permissioning khi reuse chung má»™t IAM role cho nhiá»u workloads cÃ³ nhu cáº§u khÃ¡c nhau.
* Há»— trá»£ cáº£ same-account vÃ  cross-account (qua IAM role chaining).
* Giáº£m Ä‘Ã¡ng ká»ƒ sá»‘ lÆ°á»£ng IAM roles cáº§n quáº£n lÃ½, trÃ¡nh cháº¡m giá»›i háº¡n quota IAM trong cluster lá»›n.
* Cáº¥u hÃ¬nh dá»… dÃ ng qua AWS Management Console, AWS CLI hoáº·c AWS SDK khi táº¡o association giá»¯a Kubernetes ServiceAccount vÃ  IAM role.

TÃ­nh nÄƒng nÃ y Ä‘áº·c biá»‡t há»¯u Ã­ch khi báº¡n cÃ³ nhiá»u á»©ng dá»¥ng cháº¡y trÃªn cÃ¹ng má»™t IAM role nhÆ°ng cáº§n giá»›i háº¡n quyá»n khÃ¡c nhau (vÃ­ dá»¥: má»™t pod chá»‰ Ä‘á»c S3 bucket cá»¥ thá»ƒ, pod khÃ¡c chá»‰ gá»i má»™t sá»‘ API nháº¥t Ä‘á»‹nh).

...HÃ¬nh áº£nh...

...Link...

...HÆ°á»›ng dáº«n...
