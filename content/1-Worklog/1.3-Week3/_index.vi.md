---
title: "Worklog Tuần 3"
date: 2026-05-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

## Worklog Tuần 3

**Thời gian:** 01/05/2026 - 07/05/2026

Tuần này bắt đầu chuyển từ phần giao diện tĩnh sang luồng có kết nối API. Trọng tâm là đăng nhập, lưu token, kiểm tra người dùng hiện tại và chuẩn bị lớp service để các màn hình admin có thể dùng chung.

### Mục tiêu tuần 3:

- Kết nối form đăng nhập với backend API.
- Xử lý token, protected route và trạng thái đăng nhập trên frontend.
- Tạo service layer cho các nhóm API chính.

### Các công việc cần triển khai trong tuần này:

| Ngày | Nội dung thực hiện | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| Thứ 6 | - Kết nối form đăng nhập với API backend và xử lý phản hồi đăng nhập.<br>- Tìm hiểu Amazon S3 và static website hosting.<br>&emsp; + Ghi lại các khái niệm chính để dùng khi viết báo cáo. | 01/05/2026 | 01/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 7 | - Lưu token đăng nhập và gắn token vào các request tiếp theo.<br>- Tìm hiểu Amazon RDS, DB instance, endpoint, backup và database engine.<br>&emsp; + Xem phần nào có thể áp dụng vào EAM Workspace. | 02/05/2026 | 02/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Chủ nhật | - Tạo API kiểm tra user hiện tại và đồng bộ trạng thái đăng nhập trên frontend.<br>- Tìm hiểu DynamoDB và các trường hợp dùng NoSQL.<br>&emsp; + Thực hành đọc tài liệu và ghi chú các bước cần dùng khi triển khai. | 03/05/2026 | 03/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 2 | - Xây dựng protected route theo trạng thái đăng nhập và quyền truy cập.<br>- Tìm hiểu CloudWatch metrics, logs và alarms.<br>&emsp; + So sánh với nhu cầu triển khai frontend/backend của project. | 04/05/2026 | 04/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 3 | - Bắt đầu tạo service frontend riêng cho từng nhóm API.<br>- Tìm hiểu CloudFront và CDN cho ứng dụng web.<br>&emsp; + Xem cách CDN giúp frontend tải nhanh hơn và giảm tải cho origin. | 05/05/2026 | 05/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 4 | - Bổ sung loading state và empty state cho các danh sách dữ liệu.<br>- Tìm hiểu Route 53, DNS, hosted zone và record.<br>&emsp; + Ghi lại các khái niệm chính để dùng khi viết báo cáo. | 06/05/2026 | 06/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 5 | - Rà lại luồng đăng nhập, token và gọi API để chuẩn bị xây dựng CRUD admin.<br>- Tìm hiểu AWS CLI.<br>&emsp; + Thực hành: xem cách cài đặt, cấu hình và gọi dịch vụ AWS bằng dòng lệnh. | 07/05/2026 | 07/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 3:

- Luồng đăng nhập cơ bản đã có thể gọi backend, lưu token và dùng token cho các request tiếp theo.
- Protected route giúp giới hạn truy cập vào các màn hình cần đăng nhập.
- Các trạng thái loading và empty state bắt đầu được bổ sung để giao diện phản hồi tốt hơn khi gọi API.

### Kế hoạch tuần tiếp theo

- Hoàn thiện các màn hình CRUD admin cho danh mục, phòng ban, nhân viên và tài sản.




