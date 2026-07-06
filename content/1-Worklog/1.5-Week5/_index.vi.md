---
title: "Worklog Tuần 5"
date: 2026-05-15
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

## Worklog Tuần 5

**Thời gian:** 15/05/2026 - 21/05/2026

Tuần này đi sâu vào các nghiệp vụ xoay quanh vòng đời sử dụng tài sản. Các luồng bàn giao, thu hồi, điều chuyển và bảo trì được xây dựng để hệ thống không chỉ lưu danh sách tài sản mà còn theo dõi được quá trình sử dụng thực tế.

### Mục tiêu tuần 5:

- Xây dựng giao diện và form cho nghiệp vụ bàn giao tài sản.
- Bổ sung luồng thu hồi, điều chuyển và bảo trì.
- Kiểm thử các thay đổi với dữ liệu mẫu để phát hiện lỗi trạng thái.

### Các công việc cần triển khai trong tuần này:

| Ngày | Nội dung thực hiện | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| Thứ 6 | - Xây dựng giao diện quản lý bàn giao tài sản và danh sách tài sản có thể bàn giao.<br>- Tìm hiểu CloudWatch Logs phục vụ troubleshooting.<br>&emsp; + Ghi lại các khái niệm chính để dùng khi viết báo cáo. | 15/05/2026 | 15/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 7 | - Tạo form chọn tài sản và nhân viên nhận tài sản.<br>- Tìm hiểu CloudWatch Metrics và dashboard giám sát.<br>&emsp; + Xem phần nào có thể áp dụng vào EAM Workspace. | 16/05/2026 | 16/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Chủ nhật | - Hiển thị trạng thái bàn giao và lịch sử sử dụng tài sản.<br>- Tìm hiểu CloudTrail và audit hoạt động tài khoản.<br>&emsp; + Thực hành đọc tài liệu và ghi chú các bước cần dùng khi triển khai. | 17/05/2026 | 17/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 2 | - Xây dựng luồng thu hồi tài sản và cập nhật trạng thái sau thu hồi.<br>- Tìm hiểu SNS và SQS cho messaging.<br>&emsp; + So sánh với nhu cầu triển khai frontend/backend của project. | 18/05/2026 | 18/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 3 | - Bổ sung chức năng điều chuyển tài sản giữa nhân viên/phòng ban.<br>- Tìm hiểu Step Functions và cách điều phối workflow.<br>&emsp; + Xem ví dụ luồng nhiều bước có thể áp dụng cho quy trình bàn giao hoặc bảo trì tài sản. | 19/05/2026 | 19/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 4 | - Phát triển màn hình bảo trì tài sản, trạng thái xử lý và ghi chú bảo trì.<br>- Tìm hiểu AWS Backup và bảo vệ dữ liệu.<br>&emsp; + Ghi lại các khái niệm chính để dùng khi viết báo cáo. | 20/05/2026 | 20/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 5 | - Kiểm thử các luồng bàn giao, thu hồi, điều chuyển và bảo trì với dữ liệu mẫu.<br>- Tìm hiểu monitoring, backup và messaging có thể hỗ trợ hệ thống EAM như thế nào.<br>&emsp; + Xem phần nào có thể áp dụng vào EAM Workspace. | 21/05/2026 | 21/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 5:

- Giao diện bàn giao tài sản đã hỗ trợ chọn tài sản, chọn nhân viên và theo dõi trạng thái xử lý.
- Các luồng thu hồi, điều chuyển và bảo trì giúp dữ liệu tài sản phản ánh đúng hơn vòng đời sử dụng.
- Kiến thức về CloudWatch, CloudTrail, SNS, SQS và Step Functions giúp hiểu rõ hơn bài toán giám sát và workflow.

### Kế hoạch tuần tiếp theo

- Hoàn thiện kiểm kê, báo cáo và các trạng thái dữ liệu.




