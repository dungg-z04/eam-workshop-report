---
title: "Worklog Tuần 2"
date: 2026-04-24
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

## Worklog Tuần 2

**Thời gian:** 24/04/2026 - 30/04/2026

Sau khi đã hiểu phạm vi project, tuần này tập trung vào việc dựng nền móng frontend. Các phần layout, route và component cơ bản được chuẩn bị trước để những màn hình nghiệp vụ ở các tuần sau có thể phát triển đồng bộ hơn.

### Mục tiêu tuần 2:

- Khởi tạo project frontend bằng React + Vite và cấu hình TailwindCSS.
- Tạo layout admin ban đầu gồm sidebar, navbar và vùng nội dung chính.
- Xây dựng các component dùng lại và API client skeleton.

### Các công việc cần triển khai trong tuần này:

| Ngày | Nội dung thực hiện | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| Thứ 6 | - Khởi tạo project frontend React + Vite và kiểm tra cấu trúc thư mục.<br>- Tìm hiểu IAM User, IAM Group, IAM Policy và IAM Role.<br>&emsp; + Ghi lại các khái niệm chính để dùng khi viết báo cáo. | 24/04/2026 | 24/04/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 7 | - Cấu hình TailwindCSS và tạo các style token ban đầu cho giao diện quản trị.<br>- Tìm hiểu phân quyền tối thiểu và IAM Role for EC2.<br>&emsp; + Xem phần nào có thể áp dụng vào EAM Workspace. | 25/04/2026 | 25/04/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Chủ nhật | - Tạo cấu trúc thư mục `components`, `pages`, `layouts`, `services` và `routes`.<br>- Tìm hiểu Amazon VPC, Internet Gateway, NAT Gateway và Network ACL.<br>&emsp; + Thực hành đọc tài liệu và ghi chú các bước cần dùng khi triển khai. | 26/04/2026 | 26/04/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 2 | - Xây dựng layout admin ban đầu gồm sidebar, navbar và vùng nội dung chính.<br>- Tìm hiểu Security Group và cách bảo vệ EC2/RDS.<br>&emsp; + So sánh với nhu cầu triển khai frontend/backend của project. | 27/04/2026 | 27/04/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 3 | - Tạo màn hình đăng nhập cơ bản và cấu hình React Router.<br>- Tìm hiểu EC2, EBS volume, key pair và Elastic IP.<br>&emsp; + Xem vai trò của từng thành phần khi triển khai backend lên máy chủ AWS. | 28/04/2026 | 28/04/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 4 | - Tạo các component nền tảng như Button, Input, Form Field, Table, Card và Empty State.<br>- Tìm hiểu AWS Cloud9.<br>&emsp; + Thực hành: xem cách tạo môi trường phát triển trên cloud. | 29/04/2026 | 29/04/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 5 | - Tạo API client skeleton để chuẩn hóa cách gọi backend API.<br>- Tìm hiểu IAM, VPC và EC2 sẽ được dùng như thế nào khi triển khai backend.<br>&emsp; + Ghi lại các khái niệm chính để dùng khi viết báo cáo. | 30/04/2026 | 30/04/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 2:

- Hoàn thành cấu trúc thư mục frontend theo hướng dễ mở rộng, gồm components, pages, layouts, services và routes.
- Có bộ component nền tảng để dùng cho các màn hình quản trị như Button, Input, Table, Card và Empty State.
- Hiểu rõ hơn cách IAM, VPC và EC2 liên quan đến nhu cầu triển khai backend sau này.

### Kế hoạch tuần tiếp theo

- Kết nối đăng nhập với backend API và xây dựng protected routes.




