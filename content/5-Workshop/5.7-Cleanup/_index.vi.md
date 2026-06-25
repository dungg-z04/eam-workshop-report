---
title: "Dọn dẹp tài nguyên"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

## Dọn dẹp tài nguyên

Sau khi hoàn thành workshop, cần dọn dẹp tài nguyên để tránh phát sinh chi phí AWS ngoài dự kiến.

{{% notice warning %}}
Trước khi xóa tài nguyên, hãy export dữ liệu, screenshot, log hoặc bằng chứng demo cần dùng cho báo cáo.
{{% /notice %}}

## Bước 1: Xóa Amplify app

1. Mở AWS Amplify console.
2. Chọn EAM frontend app.
3. Xóa app hoặc disconnect branch.
4. Xác nhận URL mặc định của Amplify không còn serve ứng dụng.

## Bước 2: Terminate Elastic Beanstalk environment

1. Mở Elastic Beanstalk.
2. Chọn environment `eam-backend`.
3. Chọn **Terminate environment**.
4. Chờ environment terminate hoàn toàn.
5. Xác nhận các EC2 instance liên quan đã được xóa.

Nếu Elastic Beanstalk tạo Application Load Balancer, target group và Auto Scaling resources, hãy kiểm tra các tài nguyên đó đã được xóa.

## Bước 3: Xóa Application Load Balancer nếu cần

Nếu ALB được tạo thủ công:

1. Mở EC2 console.
2. Vào **Load Balancers**.
3. Xóa EAM backend ALB.
4. Vào **Target Groups** và xóa target group không còn dùng.

## Bước 4: Xóa RDS database

1. Mở RDS console.
2. Chọn EAM MySQL database.
3. Chọn **Delete**.
4. Với môi trường demo, quyết định bỏ qua hoặc giữ final snapshot.
5. Xác nhận xóa.

{{% notice warning %}}
Xóa RDS sẽ xóa database của ứng dụng. Hãy giữ final snapshot nếu cần bảo toàn dữ liệu.
{{% /notice %}}

## Bước 5: Empty và xóa S3 bucket

Nếu đã tạo S3 bucket:

1. Mở S3 console.
2. Empty bucket.
3. Xóa bucket.
4. Xác nhận không còn file demo upload trong bucket.

## Bước 6: Xóa security group và network resource

Xóa các security group không còn dùng:

- `eam-alb-sg`
- `eam-backend-sg`
- `eam-rds-sg`

Nếu bạn tạo VPC riêng chỉ cho workshop này, hãy xóa thêm:

- NAT Gateway
- Elastic IP gắn với NAT Gateway
- Route tables
- Subnets
- Internet Gateway
- VPC

## Bước 7: Dọn CloudWatch và secrets

Kiểm tra và xóa các tài nguyên không còn dùng:

- CloudWatch log groups
- CloudWatch alarms
- Secrets Manager secrets
- Parameter Store parameters
- CloudTrail trails chỉ tạo cho workshop

## Checklist dọn dẹp cuối cùng

- [ ] Đã xóa Amplify app.
- [ ] Đã terminate Elastic Beanstalk environment.
- [ ] Đã xóa ALB và target groups nếu tạo thủ công.
- [ ] Đã xóa RDS database hoặc giữ final snapshot.
- [ ] Đã empty và xóa S3 bucket.
- [ ] Đã xóa security group.
- [ ] Đã xóa network resource không còn dùng.
- [ ] Đã kiểm tra CloudWatch logs và alarms.
- [ ] Đã xóa secrets và parameters.

## Nhắc nhở về chi phí

Các tài nguyên thường tiếp tục phát sinh chi phí là:

- RDS database instances
- NAT Gateway
- Application Load Balancer
- EC2 instances
- Elastic IP addresses
- CloudWatch log retention

Luôn kiểm tra AWS Billing console sau khi dọn dẹp.
