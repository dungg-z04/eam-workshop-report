---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Triển khai EAM Workspace trên AWS

#### Tổng quan

Trong workshop này, chúng ta sẽ triển khai **EAM Workspace**, một hệ thống quản lý tài sản doanh nghiệp, lên AWS. Ứng dụng bao gồm frontend React, backend Node.js/Express và cơ sở dữ liệu MySQL được quản lý bằng Prisma.

Kiến trúc mục tiêu được thiết kế cho môi trường demo nội bộ. Kiến trúc sử dụng các dịch vụ managed của AWS để việc triển khai đơn giản, thực tế và kiểm soát chi phí tốt hơn:

- **AWS Amplify Hosting** cho frontend React.
- **Application Load Balancer** làm entry point public cho backend.
- **AWS Elastic Beanstalk** để chạy backend Node.js/Express.
- **Amazon RDS for MySQL** để lưu dữ liệu ứng dụng.
- **Amazon S3** cho thiết kế lưu trữ file sẵn sàng production.
- **Amazon SES** cho OTP và email flow.
- **Amazon CloudWatch** cho log và monitoring cơ bản.

{{% notice note %}}
Workshop này đi theo hướng triển khai demo: không dùng Route 53, không dùng custom domain và không dùng Amazon Cognito. Xác thực hiện do backend xử lý bằng JWT.
{{% /notice %}}

#### Kiến trúc

{{< mermaid >}}
flowchart LR
    User["Trình duyệt người dùng"] --> Amplify["AWS Amplify Hosting\nReact Frontend"]
    Amplify --> Rewrite["Rewrite /api"]
    Rewrite --> ALB["Application Load Balancer"]
    ALB --> EB["Elastic Beanstalk\nNode.js Backend"]
    EB --> RDS["Amazon RDS MySQL\nPrivate Subnet"]
    EB --> S3["Amazon S3\nPrivate Bucket"]
    EB --> SES["Amazon SES"]
    EB --> CW["CloudWatch Logs"]
{{< /mermaid >}}

#### Nội dung

1. [Tổng quan workshop](5.1-Workshop-overview/)
2. [Chuẩn bị](5.2-Prerequisites/)
3. [Chuẩn bị network và RDS](5.3-Network-RDS/)
4. [Triển khai backend bằng Elastic Beanstalk](5.4-Backend-Elastic-Beanstalk/)
5. [Triển khai frontend bằng Amplify Hosting](5.5-Frontend-Amplify/)
6. [Kiểm thử, monitoring và xử lý lỗi](5.6-Test-Monitor/)
7. [Dọn dẹp tài nguyên](5.7-Cleanup/)
