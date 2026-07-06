---
title: "Worklog Tuần 6"
date: 2026-05-22
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

## Worklog Tuần 6

**Thời gian:** 22/05/2026 - 28/05/2026

Sau các luồng nghiệp vụ chính, tuần này tập trung vào kiểm kê và báo cáo. Phần này giúp hệ thống có khả năng tổng hợp tình trạng tài sản, hiển thị số liệu và hỗ trợ người quản trị theo dõi dữ liệu ở mức tổng quan.

### Mục tiêu tuần 6:

- Xây dựng màn hình kiểm kê tài sản và quản lý phiên kiểm kê.
- Bổ sung báo cáo, biểu đồ và các thẻ thống kê.
- Rà soát loading, empty và error state trên các màn hình dữ liệu.

### Các công việc cần triển khai trong tuần này:

| Ngày | Nội dung thực hiện | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| Thứ 6 | - Xây dựng màn hình kiểm kê tài sản và danh sách phiên kiểm kê.<br>- Tìm hiểu S3 lifecycle và quản lý object storage.<br>&emsp; + Ghi lại các khái niệm chính để dùng khi viết báo cáo. | 22/05/2026 | 22/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 7 | - Tạo form tạo phiên kiểm kê và cập nhật tiến độ kiểm kê.<br>- Tìm hiểu mã hóa dữ liệu với AWS KMS.<br>&emsp; + Xem phần nào có thể áp dụng vào EAM Workspace. | 23/05/2026 | 23/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Chủ nhật | - Xử lý trạng thái tài sản sau kiểm kê như sẵn sàng, đang sử dụng, bảo trì, thất lạc hoặc thanh lý.<br>- Tìm hiểu Secrets Manager và quản lý secret.<br>&emsp; + Thực hành đọc tài liệu và ghi chú các bước cần dùng khi triển khai. | 24/05/2026 | 24/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 2 | - Xây dựng màn hình báo cáo tổng quan và báo cáo tài sản.<br>- Tìm hiểu Parameter Store và cấu hình ứng dụng.<br>&emsp; + So sánh với nhu cầu triển khai frontend/backend của project. | 25/05/2026 | 25/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 3 | - Bổ sung biểu đồ và thẻ thống kê cho dashboard admin.<br>- Tìm hiểu AWS WAF và cách bảo vệ web application.<br>&emsp; + Xem các rule cơ bản để giảm request bất thường vào API. | 26/05/2026 | 26/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 4 | - Kiểm tra empty state, loading state và error state trên các màn hình dữ liệu.<br>- Tìm hiểu GuardDuty, Macie và Security Hub ở mức tổng quan.<br>&emsp; + Ghi lại các khái niệm chính để dùng khi viết báo cáo. | 27/05/2026 | 27/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 5 | - Rà soát nghiệp vụ kiểm kê/báo cáo và chuẩn bị nâng cấp giao diện tổng thể.<br>- Tìm hiểu cách bảo vệ API, database và dữ liệu nhân viên.<br>&emsp; + Xem phần nào có thể áp dụng vào EAM Workspace. | 28/05/2026 | 28/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 6:

- Luồng kiểm kê đã có giao diện để tạo phiên, theo dõi tiến độ và cập nhật trạng thái tài sản.
- Dashboard và báo cáo có thêm số liệu tổng quan, giúp người dùng nắm nhanh tình trạng tài sản.
- Các kiến thức về S3 lifecycle, KMS, Secrets Manager, WAF và Security Hub giúp mở rộng góc nhìn về bảo mật và vận hành dữ liệu.

### Kế hoạch tuần tiếp theo

- Nâng cấp giao diện, responsive và trải nghiệm người dùng.




