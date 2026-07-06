---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Triển khai hệ thống quản lý tài sản doanh nghiệp 

## Không gian làm việc cloud cho quản lý tài sản doanh nghiệp

### 1. Tóm tắt đề xuất

Đề tài của project là xây dựng **EAM Workspace**, một hệ thống quản lý tài sản doanh nghiệp chạy trên nền tảng web và được triển khai lên AWS. Hệ thống hướng đến bài toán quản lý tài sản văn phòng trong doanh nghiệp, nơi thông tin về thiết bị, người sử dụng, bàn giao, bảo trì và kiểm kê cần được theo dõi rõ ràng, tập trung và dễ truy xuất.

EAM Workspace hỗ trợ doanh nghiệp quản lý nhân viên, phòng ban, tài sản, bàn giao, yêu cầu bảo trì, phiên kiểm kê, báo cáo, góp ý, FAQ, chấm công, lịch sử đăng nhập, thông báo và support chat trong một không gian làm việc tập trung. Thay vì lưu thông tin rời rạc bằng Excel, tin nhắn hoặc file nội bộ, hệ thống gom các luồng nghiệp vụ chính vào một ứng dụng có phân quyền rõ ràng cho quản trị viên và nhân viên.

Hệ thống được phát triển theo nhóm 5 thành viên. Dự án bao gồm frontend React, backend Node.js/Express, cơ sở dữ liệu MySQL được quản lý bằng Prisma, và phương án triển khai trên AWS. Trong phạm vi báo cáo này, nội dung tập trung vào quá trình xây dựng giao diện, tích hợp API, tìm hiểu các dịch vụ AWS, triển khai demo full-stack và tài liệu hóa workshop trong giai đoạn thực tập từ **17/04/2026 đến 10/07/2026**.

Ở bản demo, kiến trúc AWS sử dụng AWS Amplify Hosting cho frontend, Amazon API Gateway làm lớp API public, AWS Elastic Beanstalk cho backend Node.js, Amazon RDS for MySQL cho dữ liệu nghiệp vụ, Amazon SES cho gửi email và Amazon CloudWatch cho log/monitoring. Một số dịch vụ như Amazon S3, AWS Secrets Manager, AWS Systems Manager Parameter Store và AWS CloudTrail được đưa vào như định hướng mở rộng để hệ thống sẵn sàng hơn khi chuyển sang môi trường production.

### 2. Mục đích sử dụng của hệ thống

EAM Workspace được dùng để hỗ trợ doanh nghiệp quản lý toàn bộ vòng đời tài sản từ lúc tạo mới, phân loại, bàn giao cho nhân viên, ghi nhận bảo trì, kiểm kê, thu hồi cho đến báo cáo tình trạng sử dụng. Hệ thống phù hợp với các doanh nghiệp có nhiều thiết bị văn phòng như laptop, màn hình, máy in, thiết bị ngoại vi hoặc tài sản cần theo dõi theo phòng ban và người sử dụng.

Với quản trị viên, hệ thống giúp theo dõi danh sách tài sản, tình trạng tài sản, nhân viên đang sử dụng, lịch sử bàn giao, yêu cầu bảo trì, dữ liệu kiểm kê và báo cáo tổng quan. Với nhân viên, hệ thống cung cấp cổng tự phục vụ để xem tài sản được cấp, gửi yêu cầu hỗ trợ, xem thông tin cá nhân và theo dõi các hoạt động liên quan đến tài sản của mình.

Mục tiêu chính của đề tài không chỉ là xây dựng một ứng dụng web có đầy đủ chức năng quản lý tài sản, mà còn là thực hành cách đưa một hệ thống full-stack lên AWS, cấu hình kết nối frontend-backend-database, kiểm thử môi trường public và kiểm soát chi phí sau khi triển khai.

### 3. Vấn đề cần giải quyết

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

Ứng dụng được triển khai lên AWS để frontend, backend, database và các dịch vụ hỗ trợ có thể chạy trong môi trường cloud, dễ truy cập, dễ giám sát và dễ mở rộng hơn. Trong giai đoạn thực tập, quá trình tự học AWS được thực hiện song song với phát triển sản phẩm, tập trung vào các chủ đề tài khoản AWS, IAM, networking, compute, database, storage, deployment, monitoring và tối ưu chi phí.

#### Lợi ích

- Quản lý tập trung vòng đời tài sản từ tạo mới, bàn giao, bảo trì, kiểm kê đến báo cáo.
- Tách rõ luồng làm việc của quản trị viên và nhân viên.
- Tăng tính bảo mật thông qua xác thực, phân quyền theo role, database private và kiểm soát biến môi trường.
- Dễ demo và triển khai nhờ các dịch vụ managed của AWS.
- Có lộ trình nâng cấp rõ ràng từ môi trường demo nội bộ lên môi trường production.

### 4. Kiến trúc giải pháp

Kiến trúc triển khai AWS được đề xuất theo mô hình ứng dụng web full-stack đơn giản cho môi trường demo nội bộ. Chế độ triển khai hiện tại không yêu cầu Route 53 hoặc custom domain. Người dùng truy cập URL mặc định của AWS Amplify Hosting, và các request API từ frontend được rewrite qua `/api/*` đến Amazon API Gateway. API Gateway tiếp tục chuyển request đến backend chạy trên AWS Elastic Beanstalk, backend kết nối đến Amazon RDS for MySQL.

{{< mermaid >}}
flowchart LR
    User["Trình duyệt người dùng"] --> Amplify["AWS Amplify Hosting\nReact Frontend"]
    Amplify --> Rewrite["Amplify Rewrite Rule\n/api/*"]
    Rewrite --> APIGW["Amazon API Gateway\nHTTP API"]
    APIGW --> EB["AWS Elastic Beanstalk\nNode.js Backend"]
    EB --> RDS["Amazon RDS for MySQL\nPrivate Subnet"]
    EB --> S3["Amazon S3\nProduction Extension"]
    EB --> SES["Amazon SES\nEmail / OTP"]
    EB --> SSM["SSM Parameter Store\nProduction Extension"]
    EB --> Secrets["AWS Secrets Manager\nProduction Extension"]
    EB --> CW["Amazon CloudWatch\nLogs and Alarms"]
    CloudTrail["AWS CloudTrail\nProduction Extension"] --> Audit["Audit Trail"]
{{< /mermaid >}}

#### Dịch vụ AWS sử dụng

- **AWS Amplify Hosting**: host và build frontend React từ nhánh triển khai.
- **Amazon API Gateway HTTP API**: nhận request `/api/*` từ Amplify và chuyển tiếp đến backend.
- **AWS Elastic Beanstalk**: chạy backend Node.js/Express với quy trình deploy được AWS quản lý.
- **Amazon EC2**: cung cấp compute instance do Elastic Beanstalk quản lý.
- **Amazon RDS for MySQL**: lưu dữ liệu như user, nhân viên, tài sản, bàn giao, yêu cầu bảo trì, phiên kiểm kê và báo cáo.
- **Amazon S3**: lưu ảnh tài sản và file upload trong thiết kế mở rộng cho môi trường production.
- **Amazon SES**: gửi OTP và email của ứng dụng.
- **AWS Secrets Manager**: định hướng lưu các giá trị nhạy cảm như application secret hoặc thông tin database khi nâng cấp khỏi chế độ demo.
- **AWS Systems Manager Parameter Store**: định hướng lưu các giá trị cấu hình runtime.
- **Amazon CloudWatch Logs and Alarms**: thu thập log backend và hỗ trợ monitoring.
- **AWS CloudTrail**: định hướng ghi nhận hoạt động trong AWS account để phục vụ audit.
- **AWS Systems Manager Session Manager**: định hướng hỗ trợ quản trị instance an toàn hơn mà không cần mở SSH public.

#### Thành phần ứng dụng

- **Frontend**: React, Vite, Tailwind CSS, React Router, component UI tái sử dụng, Admin Portal và Employee Portal.
- **Backend**: Node.js, Express.js, Prisma ORM, JWT authentication, validation, centralized error handling, request logging và các REST API module.
- **Database**: schema MySQL cho users, employees, departments, assets, assignments, maintenance requests, inventory sessions, notifications, feedback, attendance, login history và support chat.
- **Deployment**: AWS Amplify cho frontend hosting, API Gateway cho API entrypoint, Elastic Beanstalk cho backend hosting, RDS cho database và CloudWatch cho log.

### 5. Kế hoạch triển khai kỹ thuật

#### Giai đoạn 1: Phân tích yêu cầu và lập kế hoạch UI

- Phân tích bài toán quản lý tài sản và xác định các module chính.
- Xác định hai nhóm người dùng: quản trị viên và nhân viên.
- Thiết kế các luồng chính cho tạo tài sản, bàn giao, thu hồi, bảo trì, kiểm kê, báo cáo và self-service của nhân viên.
- Xây dựng các mẫu UI tái sử dụng cho Admin Portal.
- Tự học nền tảng AWS về tài khoản, quản lý chi phí, IAM, Region/AZ và các khái niệm cloud cơ bản.

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
- Tự học thêm các dịch vụ AWS liên quan đến compute, storage, database, networking và deployment để chuẩn bị cho giai đoạn triển khai.

#### Giai đoạn 4: Triển khai AWS

- Tạo hoặc sử dụng Amazon RDS for MySQL cho database của ứng dụng.
- Cấu hình security group để backend có thể truy cập RDS qua port `3306`.
- Deploy backend lên AWS Elastic Beanstalk và tạo source bundle phù hợp với môi trường Linux.
- Cấu hình biến môi trường như `DATABASE_URL`, `JWT_SECRET`, `PORT`, `FRONTEND_ORIGIN` và mail settings.
- Chạy Prisma migration và seed data nếu cần.
- Deploy frontend lên AWS Amplify Hosting.
- Cấu hình Amazon API Gateway HTTP API để proxy request đến backend Elastic Beanstalk.
- Cấu hình Amplify rewrite rule từ `/api/*` đến endpoint API Gateway và SPA fallback về `index.html`.

#### Giai đoạn 5: Kiểm thử và xác nhận

- Kiểm tra `GET /api/health`.
- Kiểm thử đăng nhập admin và nhân viên.
- Kiểm thử các luồng CRUD chính.
- Kiểm thử bàn giao tài sản, thu hồi, yêu cầu bảo trì, kiểm kê và báo cáo.
- Kiểm tra CloudWatch Logs để phát hiện lỗi backend.
- Xác nhận CORS, API Gateway route/stage/integration và Amplify rewrite rule hoạt động đúng.
- Kiểm tra upload ảnh/avatar, trạng thái tài khoản inactive và các flow demo chính.

### 6. Lộ trình và mốc triển khai

| Thời gian | Mốc triển khai | Kết quả kỳ vọng |
| --- | --- | --- |
| Tuần 1 | Định hướng dự án và nền tảng AWS | Xác định vai trò frontend, chuẩn bị môi trường và học các khái niệm AWS cơ bản. |
| Tuần 2 | Khởi tạo React app và layout admin | Dựng cấu trúc route, sidebar, layout và component cơ bản. |
| Tuần 3 | Login, token và API layer | Hoàn thiện protected route, xử lý token và service layer để tích hợp backend. |
| Tuần 4 | CRUD admin cơ bản | Hoàn thiện màn hình tài sản, nhân viên, phòng ban và các form/table chính. |
| Tuần 5 | Workflow tài sản | Phát triển bàn giao, thu hồi, điều chuyển và bảo trì tài sản. |
| Tuần 6 | Kiểm kê, báo cáo và dữ liệu | Hoàn thiện inventory, report, biểu đồ và trạng thái dữ liệu. |
| Tuần 7 | Hoàn thiện trải nghiệm giao diện | Nâng cấp responsive, dark mode, loading, toast và xử lý lỗi UI. |
| Tuần 8 | User portal và module mở rộng | Hoàn thiện employee dashboard, tài sản được bàn giao, FAQ, feedback, import Excel và floor map. |
| Tuần 9 | Chuẩn bị triển khai AWS | Rà soát production build, cấu hình môi trường, tài liệu deploy và xử lý lỗi tích hợp. |
| Tuần 10 | Deploy AWS | Triển khai với RDS, Elastic Beanstalk, API Gateway và Amplify; kiểm thử health endpoint và luồng đăng nhập. |
| Tuần 11 | Kiểm thử production và tài liệu workshop | Sửa lỗi tích hợp, kiểm tra các màn hình chính, chụp ảnh workshop và bổ sung hướng dẫn triển khai. |
| Tuần 12 | Hoàn thiện báo cáo cuối kỳ | Rà soát Hugo site, hoàn thiện self-evaluation, sharing/feedback, cleanup và chuẩn bị nộp báo cáo. |

### 7. Ước tính ngân sách

Dự án được thiết kế cho môi trường demo nội bộ, vì vậy lần triển khai đầu tiên ưu tiên chi phí thấp thay vì độ sẵn sàng cao. Chi phí cuối cùng cần được kiểm tra bằng AWS Pricing Calculator trước khi triển khai vì giá AWS thay đổi theo Region, loại instance, dung lượng lưu trữ và traffic.

| Dịch vụ | Lựa chọn tối ưu chi phí |
| --- | --- |
| AWS Amplify Hosting | Dùng domain mặc định của Amplify và chỉ deploy branch cần thiết. |
| Amazon API Gateway | Dùng HTTP API đơn giản cho route `/api/*`. |
| AWS Elastic Beanstalk / EC2 | Dùng một instance nhỏ cho môi trường demo. |
| Amazon RDS for MySQL | Dùng Single-AZ và instance class nhỏ cho dev/test. |
| Amazon S3 | Chỉ lưu các file upload cần thiết và áp dụng clean-up policy khi cần. |
| Amazon SES | Chỉ dùng cho OTP và email flow của ứng dụng. |
| CloudWatch | Giới hạn thời gian lưu log cho môi trường demo. |

Các hành động kiểm soát chi phí:

- Dùng một AWS Region cho toàn bộ resource.
- Không bật RDS Multi-AZ trong giai đoạn demo.
- Không dùng Route 53 và custom domain cho đến khi cần production.
- Clean up Elastic Beanstalk, API Gateway, RDS, S3 và CloudWatch sau workshop.
- Không giữ các môi trường deploy không còn sử dụng.

### 8. Đánh giá rủi ro

| Rủi ro | Ảnh hưởng | Xác suất | Cách giảm thiểu |
| --- | --- | --- | --- |
| Amplify rewrite rule sai | Frontend không gọi được backend API hoặc static assets bị lỗi MIME type | Trung bình | Đặt rule `/api/*` phía trên SPA fallback, giữ static assets không bị rewrite sai và test `/api/health`. |
| API Gateway route hoặc stage sai | API trả 404 dù backend vẫn chạy | Trung bình | Kiểm tra route, integration, stage và parameter mapping trước khi test frontend. |
| Sai port Elastic Beanstalk | Backend bị unhealthy | Trung bình | Set `PORT=8080` và đảm bảo backend đọc port từ biến môi trường. |
| Cấu hình security group RDS sai | Backend không kết nối được MySQL | Trung bình | Chỉ mở port `3306` từ backend security group. |
| Lỗi CORS | Browser chặn API call | Trung bình | Set `FRONTEND_ORIGIN` hoặc `FRONTEND_ORIGINS` đúng URL Amplify. |
| Thiếu hoặc sai biến môi trường production | Login, upload hoặc health check bị lỗi | Trung bình | Chuẩn hóa `DATABASE_URL`, `JWT_SECRET`, `FRONTEND_ORIGIN`, OTP/mail config và kiểm tra từng lớp sau deploy. |
| File upload không bền vững | File upload có thể mất khi instance bị thay thế | Trung bình | Dùng S3 private bucket cho production-ready storage hoặc ghi rõ giới hạn local upload trong demo. |
| Phát sinh chi phí ngoài dự kiến | Tốn chi phí AWS không cần thiết | Thấp đến trung bình | Dùng resource nhỏ nhất cho demo, đặt budget alert và clean up sau khi kiểm thử. |
| Thiếu dữ liệu test | Không demo được các luồng chính | Trung bình | Chạy Prisma seed trước demo và tài liệu hóa tài khoản demo riêng. |

### 9. Kết quả kỳ vọng

Sau khi hoàn thành project và workshop, các kết quả kỳ vọng gồm:

- Một ứng dụng Enterprise Asset Management hoạt động với Admin Portal và Employee Portal.
- Backend API hỗ trợ authentication, authorization, asset lifecycle workflow, reporting, notification, feedback, attendance và support chat.
- Schema MySQL lưu trữ dữ liệu nghiệp vụ cốt lõi của hệ thống.
- Mô hình triển khai AWS thực tế sử dụng Amplify, API Gateway, Elastic Beanstalk, RDS, SES và CloudWatch, kèm định hướng mở rộng với S3, Secrets Manager và Parameter Store.
- Một workshop step-by-step để người học khác có thể làm theo, triển khai và kiểm thử hệ thống.
- Hiểu rõ hơn về triển khai full-stack, cloud networking, biến môi trường, CORS, kết nối database, monitoring và clean-up trên AWS.

### 10. Hướng phát triển trong tương lai

- Chuyển toàn bộ file upload từ local instance storage sang Amazon S3.
- Thêm Route 53 và AWS Certificate Manager khi cần custom production domain.
- Bật RDS Multi-AZ để tăng độ sẵn sàng.
- Thêm Auto Scaling cho backend khi traffic tăng.
- Thêm Amazon ElastiCache for Redis nếu ứng dụng cần shared state cho nhiều backend instance.
- Thêm AWS WAF khi ứng dụng mở public-facing.
- Cải thiện CI/CD và automated testing cho cả frontend và backend.
