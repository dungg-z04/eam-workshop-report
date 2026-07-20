---
title: "Worklog Tuần 12"
date: 2026-07-03
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

## Worklog Tuần 12

**Thời gian:** 03/07/2026 - 10/07/2026

Tuần 12 tập trung vào kiểm thử cuối, rà soát tài nguyên AWS, cleanup và tổng kết project.

### Mục tiêu tuần 12:

- Kiểm tra lại các luồng chính của EAM Workspace sau khi triển khai production.
- Rà soát tài nguyên AWS đã tạo, theo dõi chi phí và xác định tài nguyên cần cleanup.
- Ghi nhận lỗi kỹ thuật, kết quả kiểm thử và các điểm cần xử lý trong tuần.

### Các công việc cần triển khai trong tuần này:

| Ngày | Nội dung thực hiện | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| Thứ 6 | - Kiểm thử lại luồng đăng nhập, dashboard quản trị, danh sách tài sản và cổng nhân viên trên môi trường production.<br>- Kiểm tra API health qua API Gateway để xác nhận backend vẫn phản hồi ổn định. | 03/07/2026 | 03/07/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 7 | - Rà soát cấu hình Amplify rewrite cho `/api/*`, `/uploads/*` và fallback SPA.<br>- Kiểm tra lại biến môi trường frontend để tránh gọi nhầm endpoint backend. | 04/07/2026 | 04/07/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Chủ nhật | - Theo dõi trạng thái Elastic Beanstalk, phản hồi API và các lỗi có thể phát sinh khi chạy public.<br>- Kiểm tra lại cấu hình SES/SMTP để đảm bảo luồng email không bị sai thông tin xác thực. | 05/07/2026 | 05/07/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 2 | - Rà soát RDS, security group và DATABASE_URL để đảm bảo backend kết nối database đúng môi trường.<br>- Kiểm tra dữ liệu demo và các luồng nghiệp vụ chính sau khi seed database. | 06/07/2026 | 06/07/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 3 | - Theo dõi Billing and Cost Management để nắm chi phí phát sinh từ RDS, Elastic Beanstalk, API Gateway và Amplify.<br>- Xác định các tài nguyên cần dừng hoặc xóa sau khi hoàn tất phần demo. | 07/07/2026 | 07/07/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 4 | - Rà soát các tài nguyên AWS đã tạo, gồm Elastic Beanstalk environment, API Gateway, RDS, SES identity và Amplify app.<br>- Đối chiếu lại thứ tự cleanup để tránh xóa nhầm tài nguyên còn cần kiểm tra. | 08/07/2026 | 08/07/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 5 | - Kiểm tra lại các phần đã hoàn thành trong tuần 12 và xác định lỗi còn tồn tại.<br>- Chốt danh sách cấu hình quan trọng của production để phục vụ phần tổng kết project. | 09/07/2026 | 09/07/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 6 | - Tổng kết giai đoạn thực tập, kiểm tra lại repository và xác nhận các nội dung project đã sẵn sàng để bàn giao. | 10/07/2026 | 10/07/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 12:

- Hoàn tất kiểm thử cuối cho các luồng chính của EAM Workspace trên môi trường production.
- Xác định được các tài nguyên AWS cần cleanup và các điểm cần lưu ý về chi phí.
- Có thêm ghi chú kỹ thuật phục vụ kiểm thử và triển khai các tuần sau.
