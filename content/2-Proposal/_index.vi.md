---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Triển khai hệ thống quản lý tài sản doanh nghiệp trên AWS

## Không gian làm việc cloud cho quản lý tài sản doanh nghiệp

### 1. Tóm tắt đề xuất

EAM Workspace là hệ thống quản lý tài sản doanh nghiệp, hỗ trợ doanh nghiệp quản lý nhân viên, phòng ban, tài sản, bàn giao, yêu cầu bảo trì, phiên kiểm kê, báo cáo, góp ý, FAQ, chấm công, lịch sử đăng nhập, thông báo và support chat trong một không gian làm việc tập trung.

Hệ thống được phát triển theo nhóm 5 thành viên. Dự án bao gồm frontend React, backend Node.js/Express, cơ sở dữ liệu MySQL được quản lý bằng Prisma, và phương án triển khai trên AWS. Trong phạm vi báo cáo này, workshop tập trung vào việc triển khai ứng dụng full-stack lên AWS theo kiến trúc chi phí thấp, dễ vận hành và phù hợp cho môi trường demo nội bộ.

Kiến trúc AWS mục tiêu sử dụng AWS Amplify Hosting cho frontend, Application Load Balancer và AWS Elastic Beanstalk cho backend, Amazon RDS for MySQL cho dữ liệu nghiệp vụ, Amazon S3 cho lưu trữ file trong thiết kế sẵn sàng production, Amazon SES cho gửi email, và Amazon CloudWatch cho log/monitoring.

### 2. Vấn đề cần giải quyết

#### Vấn đề hiện tại

Nhiều doanh nghiệp nhỏ và vừa vẫn quản lý tài sản văn phòng bằng bảng tính, tin nhắn hoặc các file nội bộ rời rạc. Cách làm này tạo ra nhiều vấn đề:

- Thông tin tài sản bị phân tán và khó cập nhật.
- Quản trị viên khó theo dõi ai đang sử dụng tài sản nào.
- Lịch sử bàn giao, thu hồi, chuyển giao, bảo trì và kiểm kê khó truy vết.
- Nhân viên không có cổng tự phục vụ rõ ràng để xem tài sản được cấp hoặc gửi yêu cầu hỗ trợ.
- Việc lập báo cáo chậm vì dữ liệu phải được gom và xử lý thủ công.
- File đính kèm, hình ảnh tài sản và feedback khó được tổ chức tập trung.

#### Giải pháp đề xuất

EAM Workspace giải quyết các vấn đề trên bằng cách cung cấp một ứng dụng web tập trung với hai portal chính:

- **Admin Portal**: dành cho quản trị viên để quản lý nhân viên, phòng ban, danh mục tài sản, tài sản, bàn giao, yêu cầu bảo trì, phiên kiểm kê, vị trí, báo cáo, feedback, FAQ, lịch sử chấm công, lịch sử đăng nhập và support chat.
- **Employee Portal**: dành cho nhân viên để xem tài sản được bàn giao, xem chi tiết tài sản, gửi yêu cầu hỗ trợ, xem FAQ, cập nhật hồ sơ, đổi mật khẩu, xem lịch sử cá nhân và trao đổi hỗ trợ.

Ứng dụng được triển khai lên AWS để frontend, backend, database và các dịch vụ hỗ trợ có thể chạy trong môi trường cloud, dễ truy cập, dễ giám sát và dễ mở rộng hơn.

#### Lợi ích

- Quản lý tập trung vòng đời tài sản từ tạo mới, bàn giao, bảo trì, kiểm kê đến báo cáo.
- Tách rõ luồng làm việc của quản trị viên và nhân viên.
- Tăng tính bảo mật thông qua xác thực, phân quyền theo role, database private và kiểm soát biến môi trường.
- Dễ demo và triển khai nhờ các dịch vụ managed của AWS.
- Có lộ trình nâng cấp rõ ràng từ môi trường demo nội bộ lên môi trường production.

### 3. Kiến trúc giải pháp

Kiến trúc triển khai AWS được đề xuất theo mô hình ứng dụng web full-stack đơn giản cho môi trường demo nội bộ. Chế độ triển khai hiện tại không yêu cầu Route 53 hoặc custom domain. Người dùng truy cập URL mặc định của AWS Amplify Hosting, và các request API từ frontend được proxy qua Amplify rewrite rule đến Application Load Balancer của backend.

{{< mermaid >}}
flowchart LR
    User["Trình duyệt người dùng"] --> Amplify["AWS Amplify Hosting\nReact Frontend"]
    Amplify --> Rewrite["Rewrite Rule /api"]
    Rewrite --> ALB["Application Load Balancer\nPublic Subnets"]
    ALB --> EB["AWS Elastic Beanstalk\nNode.js Backend"]
    EB --> RDS["Amazon RDS for MySQL\nPrivate Subnet"]
    EB --> S3["Amazon S3\nPrivate Bucket"]
    EB --> SES["Amazon SES\nEmail / OTP"]
    EB --> SSM["SSM Parameter Store\nRuntime Config"]
    EB --> Secrets["AWS Secrets Manager\nSecrets"]
    EB --> CW["Amazon CloudWatch\nLogs and Alarms"]
    CloudTrail["AWS CloudTrail"] --> Audit["Audit Trail"]
{{< /mermaid >}}

#### Dịch vụ AWS sử dụng

- **AWS Amplify Hosting**: host và build frontend React.
- **Application Load Balancer**: nhận HTTP traffic từ Amplify rewrite rule và chuyển tiếp đến backend.
- **AWS Elastic Beanstalk**: chạy backend Node.js/Express với quy trình deploy được AWS quản lý.
- **Amazon EC2**: cung cấp compute instance do Elastic Beanstalk quản lý.
- **Amazon RDS for MySQL**: lưu dữ liệu như user, nhân viên, tài sản, bàn giao, yêu cầu bảo trì, phiên kiểm kê và báo cáo.
- **Amazon S3**: lưu ảnh tài sản và file upload trong thiết kế sẵn sàng production.
- **Amazon SES**: gửi OTP và email của ứng dụng.
- **AWS Secrets Manager**: lưu các giá trị nhạy cảm như application secret hoặc thông tin database khi nâng cấp khỏi chế độ demo.
- **AWS Systems Manager Parameter Store**: lưu các giá trị cấu hình runtime.
- **Amazon CloudWatch Logs and Alarms**: thu thập log backend và hỗ trợ monitoring.
- **AWS CloudTrail**: ghi nhận hoạt động trong AWS account để phục vụ audit.
- **AWS Systems Manager Session Manager**: hỗ trợ quản trị instance an toàn hơn mà không cần mở SSH public.

#### Thành phần ứng dụng

- **Frontend**: React, Vite, Tailwind CSS, React Router, component UI tái sử dụng, Admin Portal và Employee Portal.
- **Backend**: Node.js, Express.js, Prisma ORM, JWT authentication, validation, centralized error handling, request logging và các REST API module.
- **Database**: schema MySQL cho users, employees, departments, assets, assignments, maintenance requests, inventory sessions, notifications, feedback, attendance, login history và support chat.
- **Deployment**: AWS Amplify cho frontend hosting, Elastic Beanstalk cho backend hosting, RDS cho database và CloudWatch cho log.

### 4. Kế hoạch triển khai kỹ thuật

#### Giai đoạn 1: Phân tích yêu cầu và lập kế hoạch UI

- Phân tích bài toán quản lý tài sản và xác định các module chính.
- Xác định hai nhóm người dùng: quản trị viên và nhân viên.
- Thiết kế các luồng chính cho tạo tài sản, bàn giao, thu hồi, bảo trì, kiểm kê, báo cáo và self-service của nhân viên.
- Xây dựng các mẫu UI tái sử dụng cho Admin Portal.

#### Giai đoạn 2: Nền tảng backend và database

- Thiết kế schema MySQL bằng Prisma.
- Triển khai authentication, authorization, kiểm tra trạng thái tài khoản và xử lý mật khẩu.
- Xây dựng REST API cho nhân viên, phòng ban, danh mục, tài sản, bàn giao, yêu cầu bảo trì, kiểm kê, báo cáo, notification, feedback, FAQ, chấm công, lịch sử đăng nhập và support chat.
- Thêm seed data cho tài khoản demo và dữ liệu nghiệp vụ mẫu.

#### Giai đoạn 3: Phát triển frontend

- Xây dựng các màn hình Admin Portal cho quản lý tài sản và tổ chức.
- Xây dựng các màn hình Employee Portal cho luồng self-service.
- Tích hợp API với backend.
- Thêm loading, empty, error và toast state.
- Rà soát responsive behavior và dark/light mode.

#### Giai đoạn 4: Triển khai AWS

- Tạo Amazon RDS for MySQL trong private subnet.
- Tạo các thành phần mạng như public/private subnet, Internet Gateway, NAT Gateway và security group nếu chưa có sẵn.
- Deploy backend lên AWS Elastic Beanstalk phía sau Application Load Balancer.
- Cấu hình biến môi trường như `DATABASE_URL`, `JWT_SECRET`, `PORT`, `FRONTEND_ORIGIN` và mail settings.
- Chạy Prisma migration và seed data nếu cần.
- Deploy frontend lên AWS Amplify Hosting.
- Cấu hình Amplify rewrite rule từ `/api/<*>` đến DNS name của Application Load Balancer.

#### Giai đoạn 5: Kiểm thử và xác nhận

- Kiểm tra `GET /api/health`.
- Kiểm thử đăng nhập admin và nhân viên.
- Kiểm thử các luồng CRUD chính.
- Kiểm thử bàn giao tài sản, thu hồi, yêu cầu bảo trì, kiểm kê và báo cáo.
- Kiểm tra CloudWatch Logs để phát hiện lỗi backend.
- Xác nhận CORS và Amplify rewrite rule hoạt động đúng.

### 5. Lộ trình và mốc triển khai

| Thời gian | Mốc triển khai | Kết quả kỳ vọng |
| --- | --- | --- |
| Week 1 - Week 2 | Phân tích yêu cầu và lập kế hoạch UI | Xác định module chính, role và cấu trúc navigation. |
| Week 3 - Week 4 | Nền tảng backend và schema database | Hoàn thành authentication, Prisma schema và cấu trúc API chính. |
| Week 5 - Week 7 | Phát triển Admin Portal | Hoàn thành dashboard, asset, employee, department, category, assignment, maintenance, inventory và report screens. |
| Week 8 - Week 9 | Employee Portal và tích hợp workflow | Tích hợp employee dashboard, tài sản của tôi, support requests, FAQ, profile và history pages. |
| Week 10 | Kiến trúc AWS và chuẩn bị deployment | Chuẩn bị deployment guide, biến môi trường, source bundle và kế hoạch dịch vụ AWS. |
| Week 11 | Deploy AWS và kiểm thử | Frontend và backend được deploy, kết nối RDS và kiểm thử end-to-end. |
| Week 12 | Tài liệu hóa và hoàn thiện workshop | Hoàn thành nội dung workshop, bằng chứng kiểm thử, bước clean-up và báo cáo cuối. |

### 6. Ước tính ngân sách

Dự án được thiết kế cho môi trường demo nội bộ, vì vậy lần triển khai đầu tiên ưu tiên chi phí thấp thay vì độ sẵn sàng cao. Chi phí cuối cùng cần được kiểm tra bằng AWS Pricing Calculator trước khi triển khai vì giá AWS thay đổi theo Region, loại instance, dung lượng lưu trữ và traffic.

| Dịch vụ | Lựa chọn tối ưu chi phí |
| --- | --- |
| AWS Amplify Hosting | Dùng domain mặc định của Amplify và chỉ deploy branch cần thiết. |
| AWS Elastic Beanstalk / EC2 | Dùng một instance nhỏ cho môi trường demo. |
| Application Load Balancer | Dùng một ALB cho backend traffic. |
| Amazon RDS for MySQL | Dùng Single-AZ và instance class nhỏ cho dev/test. |
| Amazon S3 | Chỉ lưu các file upload cần thiết và áp dụng clean-up policy khi cần. |
| Amazon SES | Chỉ dùng cho OTP và email flow của ứng dụng. |
| CloudWatch | Giới hạn thời gian lưu log cho môi trường demo. |

Các hành động kiểm soát chi phí:

- Dùng một AWS Region cho toàn bộ resource.
- Không bật RDS Multi-AZ trong giai đoạn demo.
- Không dùng Route 53 và custom domain cho đến khi cần production.
- Clean up Elastic Beanstalk, RDS, S3, ALB và CloudWatch sau workshop.
- Không giữ các môi trường deploy không còn sử dụng.

### 7. Đánh giá rủi ro

| Rủi ro | Ảnh hưởng | Xác suất | Cách giảm thiểu |
| --- | --- | --- | --- |
| Amplify rewrite rule sai | Frontend không gọi được backend API | Trung bình | Đặt rule `/api/<*>` phía trên SPA fallback và test `/api/health`. |
| Sai port Elastic Beanstalk | Backend bị unhealthy | Trung bình | Set `PORT=8080` và đảm bảo backend đọc port từ biến môi trường. |
| Cấu hình security group RDS sai | Backend không kết nối được MySQL | Trung bình | Chỉ mở port `3306` từ backend security group. |
| Lỗi CORS | Browser chặn API call | Trung bình | Set `FRONTEND_ORIGIN` hoặc `FRONTEND_ORIGINS` đúng URL Amplify. |
| File upload không bền vững | File upload có thể mất khi instance bị thay thế | Trung bình | Dùng S3 private bucket cho production-ready storage hoặc ghi rõ giới hạn local upload trong demo. |
| Phát sinh chi phí ngoài dự kiến | Tốn chi phí AWS không cần thiết | Thấp đến trung bình | Dùng resource nhỏ nhất cho demo, đặt budget alert và clean up sau khi kiểm thử. |
| Thiếu dữ liệu test | Không demo được các luồng chính | Trung bình | Chạy Prisma seed trước demo và tài liệu hóa tài khoản demo riêng. |

### 8. Kết quả kỳ vọng

Sau khi hoàn thành project và workshop, các kết quả kỳ vọng gồm:

- Một ứng dụng Enterprise Asset Management hoạt động với Admin Portal và Employee Portal.
- Backend API hỗ trợ authentication, authorization, asset lifecycle workflow, reporting, notification, feedback, attendance và support chat.
- Schema MySQL lưu trữ dữ liệu nghiệp vụ cốt lõi của hệ thống.
- Mô hình triển khai AWS thực tế sử dụng Amplify, ALB, Elastic Beanstalk, RDS, S3, SES, CloudWatch, Secrets Manager và Parameter Store.
- Một workshop step-by-step để người học khác có thể làm theo, triển khai và kiểm thử hệ thống.
- Hiểu rõ hơn về triển khai full-stack, cloud networking, biến môi trường, CORS, kết nối database, monitoring và clean-up trên AWS.

### 9. Hướng phát triển trong tương lai

- Chuyển toàn bộ file upload từ local instance storage sang Amazon S3.
- Thêm Route 53 và AWS Certificate Manager khi cần custom production domain.
- Bật RDS Multi-AZ để tăng độ sẵn sàng.
- Thêm Auto Scaling cho backend khi traffic tăng.
- Thêm Amazon ElastiCache for Redis nếu ứng dụng cần shared state cho nhiều backend instance.
- Thêm AWS WAF khi ứng dụng mở public-facing.
- Cải thiện CI/CD và automated testing cho cả frontend và backend.
