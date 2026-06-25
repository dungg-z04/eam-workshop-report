# Báo cáo tổng quan Frontend - EAM Workspace

## 1. Mục đích tài liệu

Tài liệu này mô tả chi tiết phần Frontend của dự án **EAM Workspace**. Nội dung được viết để hỗ trợ:

- Viết báo cáo thực tập/đồ án.
- Làm template thiết kế báo cáo cho team.
- Chuẩn hóa màu sắc, typography, component, spacing và style của project.
- Chuyển thông tin thiết kế sang một template Word/PowerPoint/Canva/Figma khác sao cho hợp với nhận diện của dự án.

Phần Frontend được mô tả kỹ hơn về màu sắc, logo, bố cục, dark mode, dashboard style và các component UI vì đây là phần cần thiết để điều chỉnh template báo cáo cho đồng bộ với sản phẩm.

## 2. Tổng quan Frontend

Frontend của **EAM Workspace** là ứng dụng React dành cho hai nhóm người dùng chính:

- **Admin Portal**: dành cho người quản trị tài sản/nhân sự trong doanh nghiệp.
- **Employee Portal**: dành cho nhân viên xem tài sản, hồ sơ, lịch sử, gửi yêu cầu hỗ trợ và tự phục vụ.

Frontend có vai trò:

- Hiển thị dashboard và các màn hình nghiệp vụ.
- Gọi REST API từ Backend.
- Quản lý trạng thái đăng nhập và token.
- Điều hướng theo role.
- Hiển thị loading, empty, error và toast notification.
- Hỗ trợ dark mode/light mode.
- Hỗ trợ tiếng Việt/tiếng Anh.
- Tối ưu trải nghiệm desktop và mobile.

## 3. Công nghệ sử dụng

| Thành phần | Công nghệ | Vai trò |
| --- | --- | --- |
| Framework UI | React | Xây dựng giao diện component-based |
| Build tool | Vite | Dev server và build nhanh |
| CSS framework | Tailwind CSS | Tạo UI nhanh, đồng bộ design system |
| Routing | React Router | Quản lý route admin/employee/auth |
| Icons | lucide-react | Icon hiện đại, đồng bộ |
| Notification | react-hot-toast | Toast thông báo thành công/lỗi |
| API client | fetch/custom client | Gọi Backend API |
| State | React hooks/context/local state | Quản lý state phù hợp với quy mô MVP |
| Testing UI | Playwright | Smoke test luồng UI |
| Deployment | AWS Amplify | Host React static app |

## 4. Kiến trúc Frontend

```text
frontend/
  package.json
  vite.config.js
  tailwind.config.js
  src/
    main.jsx
    App.jsx
    routes/
      AppRoutes.jsx
    components/
      layout/
      ui/
      forms/
      tables/
      common/
    pages/
      auth/
      admin/
      employee/
    services/
      client.js
      auth.service.js
      employee.service.js
      asset.service.js
      ...
    contexts/
      AuthContext.jsx
      ThemeContext.jsx
      LanguageContext.jsx
    styles/
      index.css
```

Hướng tổ chức:

- `pages`: mỗi page lớn của Admin/Employee.
- `components/layout`: navbar, sidebar, layout wrapper.
- `components/ui`: button, card, input, modal, table, badge, toast wrapper.
- `services`: gồm API client và các service theo module.
- `contexts`: quản lý auth, theme và ngôn ngữ.
- `routes`: phần chia route public/protected/admin/employee.

## 5. Định hướng thiết kế tổng thể

Phòng cách UI của EAM Workspace nên được mô tả là:

```text
Modern SaaS Dashboard
Premium Enterprise Tool
Clean Tech Interface
Asset Operations Workspace
```

Đặc điểm cảm nhận:

- Chuyên nghịệp, gọn gàng, không quá màu mè.
- Ưu tiên khả năng đọc dữ liệu, quản lý bảng bịểu và thao tắc lặp lại.
- Sử dùng navy/emerald làm nhân diện chính.
- Có dark mode cáo cập, gần với cảm giác công nghệ và vận hành hệ thống.
- Card, table, sidebar và form có border radius vua phải, shadow mềm.
- Không dùng style landing page quá trang trí; đây là sản phẩm quản trị, cần thực dụng và rõ rang.

## 6. Logo và nhận diện thương hiệu

### 6.1 Tên sản phẩm

Tên hiển thị:

```text
EAM Workspace
```

Ý nghĩa:

- `EAM`: Enterprise Asset Management.
- `Workspace`: không gian làm việc chung cho admin và nhân viên.

### 6.2 Mô tả logo

Logo gồm:

- Bịểu tượng khởi/hợp đại diện cho tài sản.
- Khung lục gìác/navy tạo cảm giác bền vững và kỹ thuật.
- Dấu check màu emerald đại diện cho xác nhận, kiểm kê, bàn giao thành công.
- Chủ `EAM Workspace` màu navy tạo cảm giác doanh nghiệp.

### 6.3 Cách sử dụng logo

Trong báo cáo/template:

- Trang bìa: dùng logo đầy đủ có wordmark.
- Header/footer: dùng icon logo nhỏ.
- Slide mô đầu: logo dat góc trai trên hoặc cần giua.
- Nền tối: dùng logo có chủ màu sáng hoặc chỉ dùng icon.
- Nền sáng: dùng logo đầy đủ bàn góc.

Tỷ lệ khuyến nghị:

- Logo đầy đủ trên bìa: rộng 180-260px.
- Logo trong header: cáo 28-36px.
- Icon trong sidebar/app: 40-48px.
- Favicon/app icon: dùng icon riêng, không dùng wordmark đại.

## 7. Hệ màu chủ đạo

### 7.1 Bảng màu nhân diện

| Vai trò | Màu | Mã màu goi y | Cách dùng |
| --- | --- | --- | --- |
| Primary Navy | Xanh navy đậm | `#062B49`, `#0B2545` | Logo, heading, sidebar, nút chính dark |
| Deep Ink | Gần đen xanh | `#0F172A`, `#111827` | Nên dark, text đảm |
| Emerald | Xanh thành công | `#10B981`, `#059669` | CTA, active state, success, badge |
| Teal | Xanh công nghệ | `#14B8A6`, `#0D9488` | Hover, accent, chart |
| Sky/Cyan | Xanh sáng | `#38BDF8`, `#0EA5E9` | Focus ring, link, highlight nhe |
| Slate | Xám xanh | `#64748B`, `#94A3B8` | Text phụ, icon, label |
| Surface Light | Nền sáng | `#F8FAFC`, `#F1F5F9` | Background, section |
| Border Light | Viền sáng | `#E2E8F0`, `#CBD5E1` | Border card/input/table |
| Surface Dark | Nền tối | `#06130F`, `#081C16`, `#0B1220` | Dark mode background |
| Danger | Do lỗi | `#EF4444`, `#DC2626` | Error, delete, broken asset |
| Warning | Vang/cảm | `#F59E0B`, `#D97706` | Cảnh báo, pending |
| Info | Xanh info | `#3B82F6`, `#2563EB` | Link, info badge |
| Purple | Tìm phụ | `#8B5CF6`, `#7C3AED` | Task, secondary metric |

### 7.2 Tỉ lệ sử dụng màu

Nên áp dụng quy tắc:

```text
70% neutral/surface
20% navy/emerald brand
10% semantic/accent
```

Ý nghĩa:

- UI không bị rối mật.
- Dashboard vận rõ rang khi có nhiều bảng, form, card.
- Emerald chỉ nên dùng để nhấn mạnh hành động chính, active state, success.
- Navy dùng làm nên hoặc text quản trong.

### 7.3 Màu cho báo cáo/template

Nếu sửa template báo cáo, nên đời bảng màu theo hệ sau:

| Thành phần báo cáo | Màu nên | Màu chủ | Ghi chú |
| --- | --- | --- | --- |
| Trang bìa | Gradient `#062B49 -> #0F172A` | Trang `#FFFFFF` | Logo dat nội bắt |
| Tiêu đề chuong | `#062B49` | Trang | Có thành accent emerald |
| Heading H1 | Không nên | `#0F172A` hoặc `#062B49` | Bàn sáng |
| Heading H2 | Không nên | `#0B2545` | Đồng bộ với logo |
| Heading dark | Không nên | `#F8FAFC` | Nếu nền tối |
| Bảng table header | `#E6F7F2` | `#065F46` | Nhẹ, sạch |
| Viền bảng | `#CBD5E1` | - | Không dùng viền đến đảm |
| Callout success | `#ECFDF5` | `#047857` | Kết quả đạt |
| Callout warning | `#FFFBEB` | `#B45309` | Lưu ý |
| Callout error | `#FEF2F2` | `#B91C1C` | Lỗi/rui rõ |
| Code block | `#0B1220` | `#E2E8F0` | Giong developer console |
| Footer | `#0F172A` | `#CBD5E1` | Nhỏ gọn |

## 8. Design tokens để đưa vào template

### 8.1 Màu nên

```text
Light background: #F8FAFC
Light surface: #FFFFFF
Light elevated surface: #FFFFFF with shadow
Dark background: #06130F / #0B1220
Dark surface: #111827 / #16211B
Dark elevated surface: rgba(15, 23, 42, 0.86)
```

### 8.2 Màu text

```text
Light heading: #0F172A
Light body: #334155
Light muted: #64748B
Dark heading: #F8FAFC
Dark body: #CBD5E1
Dark muted: #94A3B8
```

### 8.3 Border

```text
Light border: #E2E8F0
Light strong border: #CBD5E1
Dark border: rgba(148, 163, 184, 0.20)
Dark strong border: rgba(148, 163, 184, 0.35)
Accent border: rgba(16, 185, 129, 0.35)
```

### 8.4 Shadow

```text
Small: 0 1px 2px rgba(15, 23, 42, 0.06)
Medium: 0 8px 24px rgba(15, 23, 42, 0.08)
Large: 0 24px 60px rgba(15, 23, 42, 0.16)
Emerald glow: 0 20px 48px rgba(16, 185, 129, 0.18)
```

### 8.5 Border radius

```text
Button: 10px - 12px
Input: 10px
Card: 14px - 18px
Modal: 20px
Sidebar item: 12px
Badge: 999px
```

## 9. Typography

Font nên dùng:

```text
Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif
```

Nếu template Word/PowerPoint không có Inter, có thể dùng:

```text
Aptos / Segoe UI / Calibri
```

Cấp bậc chữ:

| Cập | Size web | Size báo cáo goi y | Weight | Cách dùng |
| --- | --- | --- | --- | --- |
| Display | 36-48px | 28-36pt | 800/900 | Bìa, tiêu đề lớn |
| H1 | 28-36px | 24-28pt | 800 | Tên chuong |
| H2 | 22-28px | 18-22pt | 700/800 | Mục lớn |
| H3 | 18-20px | 15-17pt | 700 | Mục nhỏ |
| Body | 14-16px | 10.5-12pt | 400/500 | Nội dung |
| Label | 11-13px | 9-10pt | 700 | Label, table header |
| Caption | 11-12px | 8.5-9pt | 500 | Ghi chú |

Nguyên tắc:

- Heading ngắn, rõ, đảm.
- Body text không quá xám nhạt.
- Label trong dashboard nên uppercase nhe, tracking vua phải.
- Không dùng letter spacing am.
- Không phòng to chủ qua mục trong card nhỏ.

## 10. Layout tổng thể

### 10.1 Admin layout

Admin layout gồm:

- Sidebar trái có nhóm menu.
- Navbar trên cùng có search, theme toggle, notification, status.
- Main content gồm page header, metric cards, table/form/workflow.
- Floating/inline actions như them mới, import, export.

Cảm gìác thiết kế:

- Giao diện quản trị đầy đủ nhưng không bị rối.
- Menu được gồm nhóm để giảm tài nhận thức.
- Table và form là trung tâm, không phải hero marketing.

### 10.2 Employee layout

Employee layout gồm:

- Sidebar cả nhân.
- Navbar có search nhanh, theme toggle, notification.
- Dashboard cả nhân.
- Các trang: tài sản của tối, yêu cầu hỗ trợ, cẩm nang tự phục vụ, hồ sơ, đời mật khẩu, lịch sử.

Cảm gìác thiết kế:

- Gần gũi hon Admin.
- Ưu tiên việc nhân viên tìm thấy thông tin của minh nhanh.
- Card có nhiều trạng thái rõ rang: đã đồng bộ, chờ xử lý, cần xác nhận.

## 11. Sidebar

### 11.1 Sidebar Admin

Sidebar Admin nên gồm các nhóm:

```text
Tổng quan
Quản lý tổ chức
  - Phòng ban
  - Nhân viên
Quản lý tài sản
  - Danh mục
  - Tài sản
  - Bàn giao
  - Bảo trì
  - Kiểm kê
  - Sơ đồ mặt bằng
Phân tích
  - Báo cáo
  - Lịch sử đăng nhập
  - Lịch sử chấm công
Hỗ trợ
  - Quản lý FAQ
  - Góp ý và phản hồi
  - Support chat
Cài đặt
```

Style:

- Nền sidebar: navy/green dark `#062B49`, `#06351F`, hoặc gradient rất nhẹ.
- Item active: emerald text + nền trong suốt có opacity.
- Item hover: nền xanh/emerald trong suốt, không dùng nền trắng trong dark sidebar.
- Icon lucide có stroke 1.75-2px.
- Khoảng cách item đồng đều.
- Mục cha nên `font-bold`.

### 11.2 Sidebar Employee

Menu:

```text
Tổng quan
Tài sản của tôi
Yêu cầu hỗ trợ
Cẩm nang tự phục vụ
Hồ sơ cá nhân
Đổi mật khẩu
Lịch sử
Cài đặt
```

Vùng user card cuối sidebar:

- Hiển thị avatar.
- Hiển thị tên nhân viên thật.
- Hiển thị email rút gọn.
- Nút logout bằng icon.
- Avatar nên có fallback initials nếu ảnh lỗi.

## 12. Navbar

Navbar nên có:

- Breadcrumb/section label.
- Page title ngắn.
- Global search.
- Trạng thái đồng bộ.
- Toggle dark/light mode.
- Notification button.
- QR/app shortcut nếu có.

Style:

- Light: nền trắng có blur nhe, border bottom `#E2E8F0`.
- Dark: nên `rgba(15, 23, 42, 0.82)`, border `rgba(148, 163, 184, 0.18)`.
- Search input bộ tròn, có icon search, shortcut hint `Ctrl K`.
- Trạng thái đồng bộ dùng badge emerald.

## 13. Button system

### 13.1 Primary button

Dùng cho hành động chính:

```text
Nen: #059669 hoac #047857
Text: #FFFFFF
Hover: #047857
Shadow: emerald glow nhe
Radius: 10-12px
```

Ví dụ:

- Them tài sản.
- Lưu thấy đời.
- Xác nhận bàn giao.
- Import Excel.

### 13.2 Secondary button

```text
Nen: #FFFFFF / dark surface
Border: #CBD5E1 / dark border
Text: #334155 / #E2E8F0
Hover: surface hover
```

### 13.3 Danger button

```text
Nen: #EF4444
Hover: #DC2626
Text: #FFFFFF
```

Dùng cho:

- Xóa.
- Khóa tài khoản.
- Báo hỏng nếu là hành động cảnh báo.

### 13.4 Icon button

Dùng cho:

- Sửa.
- Xóa.
- Loc.
- Động modal.
- Thông báo.
- Đời theme.

Kích thước:

```text
Desktop: 40-44px
Mobile: 38-42px
```

## 14. Card và metric

Metric card trên dashboard nên có:

- Label nhỏ uppercase.
- Số liệu lớn, đảm.
- Icon trong o màu nhạt.
- Mô tả/trend nhỏ.
- Border và shadow mềm.

Light mode:

```text
Card background: #FFFFFF
Border: #E2E8F0
Heading: #0F172A
Muted: #64748B
```

Dark mode:

```text
Card background: rgba(15, 23, 42, 0.86)
Border: rgba(148, 163, 184, 0.20)
Heading: #F8FAFC
Muted: #94A3B8
```

Metric icon colors:

- Tài sản: blue/cyan.
- Nhân viên: emerald.
- Bảo trì: amber.
- Lỗi/hỏng: red.
- Công việc: purple.

## 15. Table

Table là thành phần quản trong của Admin.

Style khuyến nghị:

- Header nên slate/emerald nhạt.
- Row hover rõ nhưng không qua sáng.
- Text chính đảm vua.
- Text phụ xám.
- Badge trạng thái có màu riêng.
- Action button dùng icon.
- Có empty state khi không có dữ liệu.
- Có loading skeleton khi đang tài.

Light:

```text
Header bg: #F8FAFC
Row bg: #FFFFFF
Border: #E2E8F0
Hover: #F1F5F9
```

Dark:

```text
Header bg: rgba(15, 23, 42, 0.95)
Row bg: rgba(15, 23, 42, 0.75)
Border: rgba(148, 163, 184, 0.18)
Hover: rgba(16, 185, 129, 0.08)
```

## 16. Form và input

Form nên có:

- Label rõ rang.
- Placeholder ngắn gon.
- Focus ring emerald/cyan.
- Lỗi validate hiển thị ngay dưới input.
- Disabled state rõ.
- Grid responsive 1 cột trên mobile, 2 cột trên desktop.

Input light:

```text
Background: #FFFFFF
Border: #CBD5E1
Text: #0F172A
Placeholder: #94A3B8
Focus border: #10B981
Focus ring: rgba(16, 185, 129, 0.14)
```

Input dark:

```text
Background: rgba(15, 23, 42, 0.80)
Border: rgba(148, 163, 184, 0.25)
Text: #F8FAFC
Placeholder: #64748B
Focus border: #34D399
Focus ring: rgba(52, 211, 153, 0.16)
```

## 17. Modal và drawer

Modal dùng cho:

- Them/sửa phòng ban.
- Them/sửa nhân viên.
- Them/sửa tài sản.
- Import Excel.
- Xác nhận hành động.

Style:

- Overlay màu đến opacity 40-60%.
- Modal surface sáng/tối theo theme.
- Header có title và nút động.
- Footer có cancel + primary action.
- Mobile full-width gần như full screen.
- Desktop max-width 560-900px tuy form.

## 18. Toast notification

Toast nên dùng `react-hot-toast`.

Nguyên tắc:

- Thành công: emerald.
- Lỗi: red.
- Cảnh báo: amber.
- Info: blue.
- Chủ tiếng Việt có dấu.
- Dark mode phải đọc rõ.

Style toast light:

```text
Background: #FFFFFF
Text: #0F172A
Border: #E2E8F0
Shadow: 0 20px 48px rgba(15, 23, 42, 0.14)
```

Style toast dark:

```text
Background: #111827
Text: #F8FAFC
Border: rgba(148, 163, 184, 0.25)
Shadow: 0 24px 60px rgba(0, 0, 0, 0.35)
```

## 19. Dark mode

Dark mode của project nên mang cảm giác:

```text
Enterprise control room
Premium SaaS dashboard
Dark emerald/navy workspace
```

Quy tắc dark mode:

- Không để card nền trắng trong dark mode.
- Không để text đến trên nền tối.
- Số liệu metric phải dùng màu sáng.
- Border dùng opacity, không dùng viền trang qua mạnh.
- Hover dùng emerald/teal opacity thap.
- Input có background tối và focus ring rõ.
- Empty state phải có icon/text đủ sáng.
- Map/floor plan cần có contrast cáo.

Bảng màu dark:

| Thành phần | Màu |
| --- | --- |
| App background | `#06130F` hoặc `#0B1220` |
| Sidebar | `#062B1F`, `#062B49` |
| Navbar | `rgba(15, 23, 42, 0.86)` |
| Card | `rgba(15, 23, 42, 0.82)` |
| Card border | `rgba(148, 163, 184, 0.20)` |
| Text heading | `#F8FAFC` |
| Text body | `#CBD5E1` |
| Text muted | `#94A3B8` |
| Active | `#34D399` |
| Hover | `rgba(16, 185, 129, 0.10)` |

## 20. Light mode

Light mode nên sạch, sáng, nhiều khoảng thở:

| Thành phần | Màu |
| --- | --- |
| App background | `#F8FAFC` |
| Main surface | `#FFFFFF` |
| Sidebar | Navy/emerald dark |
| Navbar | `#FFFFFF` + blur |
| Card | `#FFFFFF` |
| Border | `#E2E8F0` |
| Heading | `#0F172A` |
| Body | `#334155` |
| Muted | `#64748B` |
| Active | `#059669` |

## 21. Admin Portal - các màn hình chính

### 21.1 Dashboard

Nội dung:

- Tổng số phòng ban.
- Tổng nhân viên.
- Tổng tài sản.
- Tổng giá trị tài sản.
- Tài sản theo trạng thái.
- Hoạt động gần đây.
- Cảnh báo/yêu cầu cần xử lý.

UI:

- Metric cards 4 cột desktop, 2 cột tablet, 1 cột mobile.
- Chart/card có border radius 16px.
- Các số liệu lớn dùng font weight 800/900.

### 21.2 Quản lý phòng ban

Chuc nang:

- Danh sách phòng ban.
- Tìm kiếm.
- Them/sửa/xóa.
- Gần trường phòng/manager nếu có.

UI:

- Table rõ rang.
- Form modal ngắn gon.
- Empty state khi chưa có phòng ban.

### 21.3 Quản lý nhân viên

Chuc nang:

- Danh sách nhân viên.
- Lọc theo phòng ban/trạng thái.
- Tạo hồ sơ.
- Tạo/khóa tài khoản.
- Cập nhật ảnh đại diện.
- Import từ Excel.

UI:

- Badge trạng thái active/inactive.
- Avatar có fallback initials.
- Action icon gồm xem/sửa/khóa.

### 21.4 Quản lý danh mục

Chuc nang:

- CRUD danh mục tài sản.
- Tìm kiếm theo tên/mô tả.

UI:

- Table đơn gìản.
- Số lượng tài sản theo danh mục có badge.

### 21.5 Quản lý tài sản

Chuc nang:

- CRUD tài sản.
- Tìm kiếm/loc.
- Upload ảnh.
- Import Excel.
- Xem trạng thái và người đang sử dùng.

UI:

- Card/table kết hợp.
- Badge status rõ màu.
- Ảnh tài sản có fallback.

### 21.6 Bàn giao tài sản

Chuc nang:

- Bàn giao.
- Thử hồi.
- Chuyển giao.
- Xem lịch sử.

UI:

- Workflow cards.
- Trạng thái: cho xác nhận, đã nhân, đã trả.
- Lịch sử hiển thị timeline/table.

### 21.7 Bảo trì

Chuc nang:

- Xem yêu cầu bảo trì.
- Cập nhật trạng thái.
- Gần ưu tiên.
- Ghi chú xử lý.

UI:

- Badge severity.
- Filter theo trạng thái.
- Modal chi tiết.

### 21.8 Kiểm kê

Chuc nang:

- Tạo phiên kiểm kê.
- Theo dõi tien do.
- Cập nhật kết quả từng tài sản.

UI:

- Progress bar.
- Cards thống kê: khớp, thiếu, hỏng, chưa kiểm.

### 21.9 Báo cáo

Chuc nang:

- Tổng quan tài sản.
- Tài sản theo phòng ban.
- Chất lượng dữ liệu.
- Báo cáo loc/tìm kiếm.

UI:

- Chart/cards/table.
- Export nếu có.
- Màu chart đồng bộ navy/emerald/cyan/amber.

### 21.10 Sơ đồ mặt bằng

Chuc nang:

- Xem vị trí tài sản trong văn phòng.
- Hiển thị tọa độ tài sản.
- Lọc theo phòng ban/trạng thái.

UI:

- Dark mode cần đảm bảo contrast của marker và label.
- Marker nên dùng emerald/amber/red theo trạng thái.

## 22. Employee Portal - các màn hình chính

### 22.1 Dashboard nhân viên

Nội dung:

- Lỗi chao theo tên nhân viên.
- Tài sản đang giu.
- Yêu cầu đang xử lý.
- Công việc cần làm.
- Widget chấm công.

UI:

- Card cả nhân gon.
- Metric phải đọc rõ cả light/dark.
- Nếu số liệu 0, màu vận phải dự contrast.

### 22.2 Tài sản của tối

Chuc nang:

- Xem danh sách tài sản được bàn giao.
- Xem chi tiết từng tài sản.
- Xác nhận bàn giao.
- Báo hỏng/sử có.

UI:

- Chi tiết tài sản chia 2 cột desktop.
- Mobile stack 1 cột.
- Dark mode không để card trang gay kho đọc.
- Thông tin tài sản gồm: tên, mã, serial, danh mục, ngay nhân, tinh trang.

### 22.3 Yêu cầu hỗ trợ

Chuc nang:

- Tạo yêu cầu hỗ trợ.
- Định kèm file.
- Theo dõi trạng thái.
- Xem lịch sử phản hồi.

UI:

- Form đơn gìản.
- Badge trạng thái.
- File đính kèm hiển thị rõ tên file.

### 22.4 Cảm nang tự phục vụ

Chuc nang:

- Xem FAQ.
- Tìm kiếm cau hồi.
- Chuyển sáng tạo phieu hỗ trợ nếu cần.

UI:

- FAQ accordion/card.
- CTA tạo phieu hỗ trợ dùng emerald gradient hoặc primary button.
- Dark mode đảm bảo text trên gradient đọc được.

### 22.5 Hồ sơ cả nhân

Chuc nang:

- Xem thông tin công việc.
- Xem thông tin cá nhân.
- Xem số yêu lý lịch.
- Xem tài liệu/định kèm.
- Xem lịch sử cập nhật.
- Cập nhật avatar.
- Xuat hồ sơ PDF nếu có.

UI:

- Header profile có avatar lớn.
- Tabs rõ rang.
- Ảnh lỗi phải có fallback initials.

### 22.6 Đời mật khẩu

Chuc nang:

- Nhập mật khẩu hiện tại.
- Nhập mật khẩu mới.
- Xác nhận mật khẩu mới.

UI:

- Có nút hiện/án mật khẩu.
- Validate rõ.
- Toast thành công/lỗi.

## 23. Search

Project có search ở navbar và trong từng page.

Global search nên:

- Hiển thị shortcut `Ctrl K`.
- Tìm nhanh trang/chuc nang.
- UI đồng bộ giữa Admin và Employee.
- Có keyboard focus ring.
- Có empty state nếu không có kết quả.

Search page/table nên:

- Có placeholder cụ thể.
- Không trùng aria-label với field form khác.
- Debounce nhẹ nếu dữ liệu lớn.

## 24. Loading, empty và error state

### 24.1 Loading

Nên dùng:

- Skeleton cho card/table.
- Spinner nhỏ trong button.
- Disable button khi submitting.

### 24.2 Empty state

Cần có:

- Icon line style.
- Tiêu đề ngắn.
- Mô tả ngắn.
- CTA nếu phù hợp.

Ví dụ:

```text
Chưa có tài sản nào
Hãy thêm tài sản mới hoặc import từ Excel để bắt đầu quản lý.
```

### 24.3 Error state

Cần có:

- Message rõ, tiếng Việt có dấu.
- Nút thử lại.
- Không show stack trace cho user.

## 25. Responsive

### 25.1 Desktop

- Sidebar cố định bên trái.
- Main content rộng, table đầy đủ cột.
- Dashboard 3-4 cột.
- Form có 2 cột.

### 25.2 Tablet

- Sidebar có thể collapse.
- Dashboard 2 cột.
- Table có horizontal scroll nếu cần.
- Modal max-width nhỏ hon.

### 25.3 Mobile

- Sidebar thành drawer.
- Navbar gon, search có thể full-screen overlay.
- Dashboard 1 cột.
- Table chuyển sáng card list nếu cần.
- Button full width trong form quản trong.

Breakpoint goi y:

```text
sm: 640px
md: 768px
lg: 1024px
xl: 1280px
2xl: 1536px
```

## 26. Accessibility

Cần đảm bảo:

- Contrast text dat mục đọc được.
- Button có focus ring.
- Input có label.
- Icon button có aria-label/title.
- Modal trap focus nếu có thể.
- Không chỉ dùng màu để truyen dat trạng thái.
- Text trong button không bị tràn.
- Ảnh có alt phù hợp.

Màu focus:

```text
Light focus ring: rgba(16, 185, 129, 0.25)
Dark focus ring: rgba(52, 211, 153, 0.25)
```

## 27. Internationalization

Frontend hỗ trợ:

- Tieng Viết.
- Tieng Ảnh.

Yêu cầu chất lượng:

- Khi chuyển sáng English, tất cả menu/page/button/empty/error/toast cần là English.
- Không để nửa Việt nửa Ảnh.
- Không dùng tiếng Việt không dấu trong toast.
- Text nên quản lý tập trung để dễ bảo trì.

## 28. API integration

Frontend goi API qua client dùng chung.

Local:

```env
VITE_API_BASE_URL=http://localhost:5000/api
```

Deploy với Amplify rewrite:

```env
VITE_API_BASE_URL=/api
```

Amplify rewrite cần đảm bảo:

```text
/api/<*> -> API Gateway/Elastic Beanstalk backend
/<*> -> /index.html
```

Nếu route React như `/login` bị 404 khi refresh, cần có SPA rewrite:

```json
{
  "source": "/<*>",
  "status": "404-200",
  "target": "/index.html"
}
```

## 29. Để xuat style cho template báo cáo

### 29.1 Trang bìa

Nên:

```text
Gradient navy: #062B49 -> #0F172A
Accent: emerald #10B981
Text: #FFFFFF
Subtitle: #CBD5E1
```

Bố cục:

- Logo EAM Workspace dat giua hoặc góc trai trên.
- Tiêu đề: "Báo cáo dự án EAM Workspace".
- Subtitle: "Enterprise Asset Management System".
- Thành accent emerald mong o dưới tiêu đề.

### 29.2 Trang mục lục

Nên:

```text
Background: #F8FAFC
Heading: #062B49
Accent number: #10B981
```

### 29.3 Trang nội dung

Bố cục:

- Header nhỏ có logo icon + tên chuong.
- Footer có số trang và tên dự án.
- Heading navy.
- Bullet dùng đầu chấm emerald.
- Bảng có header nên emerald rat nhạt.

### 29.4 Trang chuong mới

Nên:

```text
Background: #0F172A
Large chapter number: rgba(16, 185, 129, 0.18)
Title: #FFFFFF
Subtitle: #CBD5E1
```

### 29.5 Trang screenshot UI

Nên:

- Nên `#F8FAFC`.
- Screenshot dat trong frame bộ trọn 16px.
- Shadow mềm.
- Caption màu `#64748B`.
- Nếu screenshot dark mode, nền trắng phải có border để tách nên.

### 29.6 Trang kết quả/demo

Nên:

```text
Background: #ECFDF5
Heading: #065F46
Badge: #10B981
```

Dùng cho:

- Kết quả deploy.
- Health OK.
- Test login thành công.
- Các tính năng hoan thành.

## 30. Màu chart cho báo cáo/dashboard

Dùng bộ màu:

```text
Emerald: #10B981
Cyan: #06B6D4
Blue: #3B82F6
Amber: #F59E0B
Red: #EF4444
Purple: #8B5CF6
Slate: #64748B
```

Mapping:

- Available/OK: emerald.
- Assigned/In progress: blue.
- Maintenance/Pending: amber.
- Broken/Error: red.
- Task/Other: purple.
- Unknown/Inactive: slate.

## 31. Đoạn mô tả ngắn có thể đưa vào báo cáo

Frontend của EAM Workspace được xây dựng bằng React, Vite và Tailwind CSS, theo phong cách modern SaaS dashboard phù hợp với hệ thống quản lý tài sản doanh nghiệp. Giao diện được chia thành Admin Portal và Employee Portal, mỗi portal có layout, sidebar, navbar và các màn hình nghiệp vụ riêng. Hệ thống hỗ trợ light/dark mode, song ngữ Việt-Anh, toast notification, global search, responsive layout và các thành phần UI tái sử dụng như card, table, form, modal, badge và button. Màu sắc chủ đạo là navy, emerald và slate, tạo cảm giác chuyên nghiệp, hiện đại và đồng bộ với logo EAM Workspace. Frontend được deploy lên AWS Amplify và giao tiếp với Backend thông qua API Gateway/Elastic Beanstalk bằng đường dẫn `/api`.

## 32. Checklist UI trước khi demo

- Đăng nhập admin thành công.
- Đăng nhập user thành công.
- Tài khoản inactive bị chặn.
- Refresh `/login`, `/admin/dashboard`, `/employee/dashboard` không bị 404.
- Dark mode trên Admin dashboard đọc rõ.
- Dark mode trên Employee tài sản/hồ sơ/cẩm nang đọc rõ.
- Sidebar active/hover không làm mất chữ.
- Search navbar hoạt động.
- Toast hiển thị tiếng Việt có dấu.
- Table có loading/empty state.
- Import Excel hiển thị kết quả rõ.
- Upload avatar hiển thị ngay sau khi cập nhật.
- Ảnh upload qua deploy không bị 404.
- Mobile không tràn text, không vỡ layout.
- API `/api/health` OK trên domain deploy.

## 33. Checklist template báo cáo

Khi đưa tài liệu này sang template báo cáo, nên yêu cầu template:

- Đổi màu chủ đạo sang navy/emerald/slate.
- Dùng logo EAM Workspace trên bìa và header.
- Thay các màu cam/tím/beige không liên quan nếu template màu đang dùng.
- Dùng Inter/Segoe UI thay cho font trang trí.
- Dùng table header emerald nhạt.
- Dùng code block nền navy đậm.
- Dùng screenshot frame có radius 16px và shadow mềm.
- Dùng badge màu theo semantic status.
- Thêm trang riêng cho Admin Portal, Employee Portal, Backend Architecture và AWS Deployment.

## 34. Tóm tắt nhận diện hình ảnh

Nếu cần gửi cho người sửa template, có thể gửi đoạn này:

```text
Dự án EAM Workspace có phong cách modern SaaS / premium enterprise dashboard.
Màu chính là navy đậm (#062B49, #0F172A), emerald (#10B981, #059669), teal/cyan (#14B8A6, #38BDF8) và slate neutral (#64748B, #E2E8F0, #F8FAFC).
Logo là biểu tượng khối tài sản màu navy/trắng kết hợp shield check emerald.
Template báo cáo nên sạch, hiện đại, nhiều khoảng trắng, heading navy, accent emerald, table gọn, card bo tròn 14-18px, shadow mềm.
Tránh dùng màu be/cam/tím quá nhiều vì không hợp với nhận diện project.
```
