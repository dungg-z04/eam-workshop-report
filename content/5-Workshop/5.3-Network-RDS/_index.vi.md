---
title: "Chuẩn bị network và RDS"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

## Chuẩn bị network và RDS

Ở bước này, chúng ta sẽ chuẩn bị network baseline và tạo Amazon RDS for MySQL. Database không nên public ra Internet.

## Mô hình network mục tiêu

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

## Bước 1: Chọn hoặc tạo VPC

Dùng VPC có sẵn nếu VPC đó đã có:

- Internet Gateway.
- Ít nhất hai public subnet ở hai Availability Zone.
- Ít nhất hai private subnet ở hai Availability Zone.
- NAT Gateway nằm trong public subnet.
- Route table được cấu hình cho public và private routing.

Nếu AWS account chưa có VPC phù hợp, hãy tạo VPC mới trong VPC console.

## Bước 2: Tạo security group

Tạo các security group riêng cho load balancer, backend và database.

| Security group | Inbound rule | Mục đích |
| --- | --- | --- |
| `eam-alb-sg` | HTTP `80` từ `0.0.0.0/0` | Cho phép user và Amplify rewrite traffic đi vào ALB. |
| `eam-backend-sg` | HTTP từ `eam-alb-sg` | Chỉ cho ALB gọi vào backend. |
| `eam-rds-sg` | MySQL `3306` từ `eam-backend-sg` | Chỉ cho backend kết nối database. |

{{% notice warning %}}
Không mở port MySQL `3306` cho `0.0.0.0/0`. RDS cần nằm private.
{{% /notice %}}

## Bước 3: Tạo Amazon RDS for MySQL

Mở Amazon RDS console và tạo database:

1. Chọn **Create database**.
2. Chọn **Standard create**.
3. Chọn engine **MySQL**.
4. Chọn template **Dev/Test** chi phí thấp nếu có.
5. Đặt DB instance identifier, ví dụ `eam-mysql-demo`.
6. Đặt master username, ví dụ `asset_app`.
7. Đặt mật khẩu mạnh và lưu ở nơi an toàn.
8. Chọn instance class nhỏ cho môi trường demo.
9. Chọn dung lượng storage nhỏ phù hợp để test.
10. Ở **Connectivity**, chọn VPC mục tiêu.
11. Chọn DB subnet group dùng private subnet.
12. Đặt **Public access** là **No**.
13. Gắn `eam-rds-sg`.
14. Bật storage encryption.
15. Đặt initial database name:

```text
enterprise_asset_management
```

Chờ database chuyển sang trạng thái **Available**.

## Bước 4: Ghi lại thông tin kết nối

Sau khi RDS available, ghi lại:

- RDS endpoint
- Port, thường là `3306`
- Database name
- Username
- Password

Tạo backend `DATABASE_URL`:

```env
DATABASE_URL=mysql://asset_app:<password>@<rds-endpoint>:3306/enterprise_asset_management
```

## Bước 5: Kiểm tra bảo mật

Trước khi tiếp tục, kiểm tra:

- RDS public access là **No**.
- Inbound rule của RDS chỉ cho `3306` từ backend security group.
- Backend security group chỉ nhận traffic từ ALB security group.
- ALB được gắn vào public subnet.

## Kết quả mong đợi

Kết thúc bước này, project có một MySQL database private sẵn sàng cho backend deployment.
