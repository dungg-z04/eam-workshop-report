# Bao cao tong quan Frontend - EAM Workspace

## 1. Muc dich tai lieu

Tai lieu nay mo ta chi tiet phan Frontend cua du an **EAM Workspace**. Noi dung duoc viet de ho tro:

- Viet bao cao thuc tap/do an.
- Lam template thiet ke bao cao cho team.
- Chuan hoa mau sac, typography, component, spacing va style cua project.
- Chuyen thong tin thiet ke sang mot template Word/PowerPoint/Canva/Figma khac sao cho hop voi nhan dien cua du an.

Phan Frontend duoc mo ta ky hon ve mau sac, logo, bo cuc, dark mode, dashboard style va cac component UI vi day la phan can thiet de dieu chinh template bao cao cho dong bo voi san pham.

## 2. Tong quan Frontend

Frontend cua **EAM Workspace** la ung dung React danh cho hai nhom nguoi dung chinh:

- **Admin Portal**: danh cho nguoi quan tri tai san/nhan su trong doanh nghiep.
- **Employee Portal**: danh cho nhan vien xem tai san, ho so, lich su, gui yeu cau ho tro va tu phuc vu.

Frontend co vai tro:

- Hien thi dashboard va cac man hinh nghiep vu.
- Goi REST API tu Backend.
- Quan ly trang thai dang nhap va token.
- Dieu huong theo role.
- Hien thi loading, empty, error va toast notification.
- Ho tro dark mode/light mode.
- Ho tro tieng Viet/tieng Anh.
- Toi uu trai nghiem desktop va mobile.

## 3. Cong nghe su dung

| Thanh phan | Cong nghe | Vai tro |
| --- | --- | --- |
| Framework UI | React | Xay dung giao dien component-based |
| Build tool | Vite | Dev server va build nhanh |
| CSS framework | Tailwind CSS | Tao UI nhanh, dong bo design system |
| Routing | React Router | Quan ly route admin/employee/auth |
| Icons | lucide-react | Icon hien dai, dong bo |
| Notification | react-hot-toast | Toast thong bao thanh cong/loi |
| API client | fetch/custom client | Goi Backend API |
| State | React hooks/context/local state | Quan ly state phu hop voi quy mo MVP |
| Testing UI | Playwright | Smoke test luong UI |
| Deployment | AWS Amplify | Host React static app |

## 4. Kien truc Frontend

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

Huong to chuc:

- `pages`: moi page lon cua Admin/Employee.
- `components/layout`: navbar, sidebar, layout wrapper.
- `components/ui`: button, card, input, modal, table, badge, toast wrapper.
- `services`: gom API client va cac service theo module.
- `contexts`: quan ly auth, theme va ngon ngu.
- `routes`: phan chia route public/protected/admin/employee.

## 5. Dinh huong thiet ke tong the

Phong cach UI cua EAM Workspace nen duoc mo ta la:

```text
Modern SaaS Dashboard
Premium Enterprise Tool
Clean Tech Interface
Asset Operations Workspace
```

Dac diem cam nhan:

- Chuyen nghiep, gon gang, khong qua mau me.
- Uu tien kha nang doc du lieu, quan ly bang bieu va thao tac lap lai.
- Su dung navy/emerald lam nhan dien chinh.
- Co dark mode cao cap, gan voi cam giac cong nghe va van hanh he thong.
- Card, table, sidebar va form co border radius vua phai, shadow mem.
- Khong dung style landing page qua trang tri; day la san pham quan tri, can thuc dung va ro rang.

## 6. Logo va nhan dien thuong hieu

### 6.1 Ten san pham

Ten hien thi:

```text
EAM Workspace
```

Y nghia:

- `EAM`: Enterprise Asset Management.
- `Workspace`: khong gian lam viec chung cho admin va nhan vien.

### 6.2 Mo ta logo

Logo gom:

- Bieu tuong khoi/hop dai dien cho tai san.
- Khung luc giac/navy tao cam giac ben vung va ky thuat.
- Dau check mau emerald dai dien cho xac nhan, kiem ke, ban giao thanh cong.
- Chu `EAM Workspace` mau navy tao cam giac doanh nghiep.

### 6.3 Cach su dung logo

Trong bao cao/template:

- Trang bia: dung logo day du co wordmark.
- Header/footer: dung icon logo nho.
- Slide mo dau: logo dat goc trai tren hoac can giua.
- Nen toi: dung logo co chu mau sang hoac chi dung icon.
- Nen sang: dung logo day du ban goc.

Ty le khuyen nghi:

- Logo day du tren bia: rong 180-260px.
- Logo trong header: cao 28-36px.
- Icon trong sidebar/app: 40-48px.
- Favicon/app icon: dung icon rieng, khong dung wordmark dai.

## 7. He mau chu dao

### 7.1 Bang mau nhan dien

| Vai tro | Mau | Ma mau goi y | Cach dung |
| --- | --- | --- | --- |
| Primary Navy | Xanh navy dam | `#062B49`, `#0B2545` | Logo, heading, sidebar, nut chinh dark |
| Deep Ink | Gan den xanh | `#0F172A`, `#111827` | Nen dark, text dam |
| Emerald | Xanh thanh cong | `#10B981`, `#059669` | CTA, active state, success, badge |
| Teal | Xanh cong nghe | `#14B8A6`, `#0D9488` | Hover, accent, chart |
| Sky/Cyan | Xanh sang | `#38BDF8`, `#0EA5E9` | Focus ring, link, highlight nhe |
| Slate | Xam xanh | `#64748B`, `#94A3B8` | Text phu, icon, label |
| Surface Light | Nen sang | `#F8FAFC`, `#F1F5F9` | Background, section |
| Border Light | Vien sang | `#E2E8F0`, `#CBD5E1` | Border card/input/table |
| Surface Dark | Nen toi | `#06130F`, `#081C16`, `#0B1220` | Dark mode background |
| Danger | Do loi | `#EF4444`, `#DC2626` | Error, delete, broken asset |
| Warning | Vang/cam | `#F59E0B`, `#D97706` | Canh bao, pending |
| Info | Xanh info | `#3B82F6`, `#2563EB` | Link, info badge |
| Purple | Tim phu | `#8B5CF6`, `#7C3AED` | Task, secondary metric |

### 7.2 Ti le su dung mau

Nen ap dung quy tac:

```text
70% neutral/surface
20% navy/emerald brand
10% semantic/accent
```

Y nghia:

- UI khong bi roi mat.
- Dashboard van ro rang khi co nhieu bang, form, card.
- Emerald chi nen dung de nhan manh hanh dong chinh, active state, success.
- Navy dung lam nen hoac text quan trong.

### 7.3 Mau cho bao cao/template

Neu sua template bao cao, nen doi bang mau theo he sau:

| Thanh phan bao cao | Mau nen | Mau chu | Ghi chu |
| --- | --- | --- | --- |
| Trang bia | Gradient `#062B49 -> #0F172A` | Trang `#FFFFFF` | Logo dat noi bat |
| Tieu de chuong | `#062B49` | Trang | Co thanh accent emerald |
| Heading H1 | Khong nen | `#0F172A` hoac `#062B49` | Ban sang |
| Heading H2 | Khong nen | `#0B2545` | Dong bo voi logo |
| Heading dark | Khong nen | `#F8FAFC` | Neu nen toi |
| Bang table header | `#E6F7F2` | `#065F46` | Nhe, sach |
| Vien bang | `#CBD5E1` | - | Khong dung vien den dam |
| Callout success | `#ECFDF5` | `#047857` | Ket qua dat |
| Callout warning | `#FFFBEB` | `#B45309` | Luu y |
| Callout error | `#FEF2F2` | `#B91C1C` | Loi/rui ro |
| Code block | `#0B1220` | `#E2E8F0` | Giong developer console |
| Footer | `#0F172A` | `#CBD5E1` | Nho gon |

## 8. Design tokens de dua vao template

### 8.1 Mau nen

```text
Light background: #F8FAFC
Light surface: #FFFFFF
Light elevated surface: #FFFFFF with shadow
Dark background: #06130F / #0B1220
Dark surface: #111827 / #16211B
Dark elevated surface: rgba(15, 23, 42, 0.86)
```

### 8.2 Mau text

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

Font nen dung:

```text
Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif
```

Neu template Word/PowerPoint khong co Inter, co the dung:

```text
Aptos / Segoe UI / Calibri
```

Cap bac chu:

| Cap | Size web | Size bao cao goi y | Weight | Cach dung |
| --- | --- | --- | --- | --- |
| Display | 36-48px | 28-36pt | 800/900 | Bia, tieu de lon |
| H1 | 28-36px | 24-28pt | 800 | Ten chuong |
| H2 | 22-28px | 18-22pt | 700/800 | Muc lon |
| H3 | 18-20px | 15-17pt | 700 | Muc nho |
| Body | 14-16px | 10.5-12pt | 400/500 | Noi dung |
| Label | 11-13px | 9-10pt | 700 | Label, table header |
| Caption | 11-12px | 8.5-9pt | 500 | Ghi chu |

Nguyen tac:

- Heading ngan, ro, dam.
- Body text khong qua xam nhat.
- Label trong dashboard nen uppercase nhe, tracking vua phai.
- Khong dung letter spacing am.
- Khong phong to chu qua muc trong card nho.

## 10. Layout tong the

### 10.1 Admin layout

Admin layout gom:

- Sidebar trai co nhom menu.
- Navbar tren cung co search, theme toggle, notification, status.
- Main content gom page header, metric cards, table/form/workflow.
- Floating/inline actions nhu them moi, import, export.

Cam giac thiet ke:

- Giao dien quan tri day du nhung khong bi roi.
- Menu duoc gom nhom de giam tai nhan thuc.
- Table va form la trung tam, khong phai hero marketing.

### 10.2 Employee layout

Employee layout gom:

- Sidebar ca nhan.
- Navbar co search nhanh, theme toggle, notification.
- Dashboard ca nhan.
- Cac trang: tai san cua toi, yeu cau ho tro, cam nang tu phuc vu, ho so, doi mat khau, lich su.

Cam giac thiet ke:

- Gan gui hon Admin.
- Uu tien viec nhan vien tim thay thong tin cua minh nhanh.
- Card co nhieu trang thai ro rang: da dong bo, cho xu ly, can xac nhan.

## 11. Sidebar

### 11.1 Sidebar Admin

Sidebar Admin nen gom cac nhom:

```text
Tong quan
Quan ly to chuc
  - Phong ban
  - Nhan vien
Quan ly tai san
  - Danh muc
  - Tai san
  - Ban giao
  - Bao tri
  - Kiem ke
  - So do mat bang
Phan tich
  - Bao cao
  - Lich su dang nhap
  - Lich su cham cong
Ho tro
  - Quan ly FAQ
  - Gop y va phan hoi
  - Support chat
Cai dat
```

Style:

- Nen sidebar: navy/green dark `#062B49`, `#06351F`, hoac gradient rat nhe.
- Item active: emerald text + nen trong suot co opacity.
- Item hover: nen xanh/emerald trong suot, khong dung nen trang trong dark sidebar.
- Icon lucide co stroke 1.75-2px.
- Khoang cach item dong deu.
- Muc cha nen `font-bold`.

### 11.2 Sidebar Employee

Menu:

```text
Tong quan
Tai san cua toi
Yeu cau ho tro
Cam nang tu phuc vu
Ho so ca nhan
Doi mat khau
Lich su
Cai dat
```

Vung user card cuoi sidebar:

- Hien thi avatar.
- Hien thi ten nhan vien that.
- Hien thi email rut gon.
- Nut logout bang icon.
- Avatar nen co fallback initials neu anh loi.

## 12. Navbar

Navbar nen co:

- Breadcrumb/section label.
- Page title ngan.
- Global search.
- Trang thai dong bo.
- Toggle dark/light mode.
- Notification button.
- QR/app shortcut neu co.

Style:

- Light: nen trang co blur nhe, border bottom `#E2E8F0`.
- Dark: nen `rgba(15, 23, 42, 0.82)`, border `rgba(148, 163, 184, 0.18)`.
- Search input bo tron, co icon search, shortcut hint `Ctrl K`.
- Trang thai dong bo dung badge emerald.

## 13. Button system

### 13.1 Primary button

Dung cho hanh dong chinh:

```text
Nen: #059669 hoac #047857
Text: #FFFFFF
Hover: #047857
Shadow: emerald glow nhe
Radius: 10-12px
```

Vi du:

- Them tai san.
- Luu thay doi.
- Xac nhan ban giao.
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

Dung cho:

- Xoa.
- Khoa tai khoan.
- Bao hong neu la hanh dong canh bao.

### 13.4 Icon button

Dung cho:

- Sua.
- Xoa.
- Loc.
- Dong modal.
- Thong bao.
- Doi theme.

Kich thuoc:

```text
Desktop: 40-44px
Mobile: 38-42px
```

## 14. Card va metric

Metric card tren dashboard nen co:

- Label nho uppercase.
- So lieu lon, dam.
- Icon trong o mau nhat.
- Mo ta/trend nho.
- Border va shadow mem.

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

- Tai san: blue/cyan.
- Nhan vien: emerald.
- Bao tri: amber.
- Loi/hong: red.
- Cong viec: purple.

## 15. Table

Table la thanh phan quan trong cua Admin.

Style khuyen nghi:

- Header nen slate/emerald nhat.
- Row hover ro nhung khong qua sang.
- Text chinh dam vua.
- Text phu xam.
- Badge trang thai co mau rieng.
- Action button dung icon.
- Co empty state khi khong co du lieu.
- Co loading skeleton khi dang tai.

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

## 16. Form va input

Form nen co:

- Label ro rang.
- Placeholder ngan gon.
- Focus ring emerald/cyan.
- Loi validate hien thi ngay duoi input.
- Disabled state ro.
- Grid responsive 1 cot tren mobile, 2 cot tren desktop.

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

## 17. Modal va drawer

Modal dung cho:

- Them/sua phong ban.
- Them/sua nhan vien.
- Them/sua tai san.
- Import Excel.
- Xac nhan hanh dong.

Style:

- Overlay mau den opacity 40-60%.
- Modal surface sang/toi theo theme.
- Header co title va nut dong.
- Footer co cancel + primary action.
- Mobile full-width gan nhu full screen.
- Desktop max-width 560-900px tuy form.

## 18. Toast notification

Toast nen dung `react-hot-toast`.

Nguyen tac:

- Thanh cong: emerald.
- Loi: red.
- Canh bao: amber.
- Info: blue.
- Chu tieng Viet co dau.
- Dark mode phai doc ro.

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

Dark mode cua project nen mang cam giac:

```text
Enterprise control room
Premium SaaS dashboard
Dark emerald/navy workspace
```

Quy tac dark mode:

- Khong de card nen trang trong dark mode.
- Khong de text den tren nen toi.
- So lieu metric phai dung mau sang.
- Border dung opacity, khong dung vien trang qua manh.
- Hover dung emerald/teal opacity thap.
- Input co background toi va focus ring ro.
- Empty state phai co icon/text du sang.
- Map/floor plan can co contrast cao.

Bang mau dark:

| Thanh phan | Mau |
| --- | --- |
| App background | `#06130F` hoac `#0B1220` |
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

Light mode nen sach, sang, nhieu khoang tho:

| Thanh phan | Mau |
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

## 21. Admin Portal - cac man hinh chinh

### 21.1 Dashboard

Noi dung:

- Tong so phong ban.
- Tong nhan vien.
- Tong tai san.
- Tong gia tri tai san.
- Tai san theo trang thai.
- Hoat dong gan day.
- Canh bao/yeu cau can xu ly.

UI:

- Metric cards 4 cot desktop, 2 cot tablet, 1 cot mobile.
- Chart/card co border radius 16px.
- Cac so lieu lon dung font weight 800/900.

### 21.2 Quan ly phong ban

Chuc nang:

- Danh sach phong ban.
- Tim kiem.
- Them/sua/xoa.
- Gan truong phong/manager neu co.

UI:

- Table ro rang.
- Form modal ngan gon.
- Empty state khi chua co phong ban.

### 21.3 Quan ly nhan vien

Chuc nang:

- Danh sach nhan vien.
- Loc theo phong ban/trang thai.
- Tao ho so.
- Tao/khoa tai khoan.
- Cap nhat anh dai dien.
- Import tu Excel.

UI:

- Badge trang thai active/inactive.
- Avatar co fallback initials.
- Action icon gom xem/sua/khoa.

### 21.4 Quan ly danh muc

Chuc nang:

- CRUD danh muc tai san.
- Tim kiem theo ten/mo ta.

UI:

- Table don gian.
- So luong tai san theo danh muc co badge.

### 21.5 Quan ly tai san

Chuc nang:

- CRUD tai san.
- Tim kiem/loc.
- Upload anh.
- Import Excel.
- Xem trang thai va nguoi dang su dung.

UI:

- Card/table ket hop.
- Badge status ro mau.
- Anh tai san co fallback.

### 21.6 Ban giao tai san

Chuc nang:

- Ban giao.
- Thu hoi.
- Chuyen giao.
- Xem lich su.

UI:

- Workflow cards.
- Trang thai: cho xac nhan, da nhan, da tra.
- Lich su hien thi timeline/table.

### 21.7 Bao tri

Chuc nang:

- Xem yeu cau bao tri.
- Cap nhat trang thai.
- Gan uu tien.
- Ghi chu xu ly.

UI:

- Badge severity.
- Filter theo trang thai.
- Modal chi tiet.

### 21.8 Kiem ke

Chuc nang:

- Tao phien kiem ke.
- Theo doi tien do.
- Cap nhat ket qua tung tai san.

UI:

- Progress bar.
- Cards thong ke: khop, thieu, hong, chua kiem.

### 21.9 Bao cao

Chuc nang:

- Tong quan tai san.
- Tai san theo phong ban.
- Chat luong du lieu.
- Bao cao loc/tim kiem.

UI:

- Chart/cards/table.
- Export neu co.
- Mau chart dong bo navy/emerald/cyan/amber.

### 21.10 So do mat bang

Chuc nang:

- Xem vi tri tai san trong van phong.
- Hien thi toa do tai san.
- Loc theo phong ban/trang thai.

UI:

- Dark mode can dam bao contrast cua marker va label.
- Marker nen dung emerald/amber/red theo trang thai.

## 22. Employee Portal - cac man hinh chinh

### 22.1 Dashboard nhan vien

Noi dung:

- Loi chao theo ten nhan vien.
- Tai san dang giu.
- Yeu cau dang xu ly.
- Cong viec can lam.
- Widget cham cong.

UI:

- Card ca nhan gon.
- Metric phai doc ro ca light/dark.
- Neu so lieu 0, mau van phai du contrast.

### 22.2 Tai san cua toi

Chuc nang:

- Xem danh sach tai san duoc ban giao.
- Xem chi tiet tung tai san.
- Xac nhan ban giao.
- Bao hong/su co.

UI:

- Chi tiet tai san chia 2 cot desktop.
- Mobile stack 1 cot.
- Dark mode khong de card trang gay kho doc.
- Thong tin tai san gom: ten, ma, serial, danh muc, ngay nhan, tinh trang.

### 22.3 Yeu cau ho tro

Chuc nang:

- Tao yeu cau ho tro.
- Dinh kem file.
- Theo doi trang thai.
- Xem lich su phan hoi.

UI:

- Form don gian.
- Badge trang thai.
- File dinh kem hien thi ro ten file.

### 22.4 Cam nang tu phuc vu

Chuc nang:

- Xem FAQ.
- Tim kiem cau hoi.
- Chuyen sang tao phieu ho tro neu can.

UI:

- FAQ accordion/card.
- CTA tao phieu ho tro dung emerald gradient hoac primary button.
- Dark mode dam bao text tren gradient doc duoc.

### 22.5 Ho so ca nhan

Chuc nang:

- Xem thong tin cong viec.
- Xem thong tin ca nhan.
- Xem so yeu ly lich.
- Xem tai lieu/dinh kem.
- Xem lich su cap nhat.
- Cap nhat avatar.
- Xuat ho so PDF neu co.

UI:

- Header profile co avatar lon.
- Tabs ro rang.
- Anh loi phai co fallback initials.

### 22.6 Doi mat khau

Chuc nang:

- Nhap mat khau hien tai.
- Nhap mat khau moi.
- Xac nhan mat khau moi.

UI:

- Co nut hien/an mat khau.
- Validate ro.
- Toast thanh cong/loi.

## 23. Search

Project co search o navbar va trong tung page.

Global search nen:

- Hien thi shortcut `Ctrl K`.
- Tim nhanh trang/chuc nang.
- UI dong bo giua Admin va Employee.
- Co keyboard focus ring.
- Co empty state neu khong co ket qua.

Search page/table nen:

- Co placeholder cu the.
- Khong trung aria-label voi field form khac.
- Debounce nhe neu du lieu lon.

## 24. Loading, empty va error state

### 24.1 Loading

Nen dung:

- Skeleton cho card/table.
- Spinner nho trong button.
- Disable button khi submitting.

### 24.2 Empty state

Can co:

- Icon line style.
- Tieu de ngan.
- Mo ta ngan.
- CTA neu phu hop.

Vi du:

```text
Chua co tai san nao
Hay them tai san moi hoac import tu Excel de bat dau quan ly.
```

### 24.3 Error state

Can co:

- Message ro, tieng Viet co dau.
- Nut thu lai.
- Khong show stack trace cho user.

## 25. Responsive

### 25.1 Desktop

- Sidebar co dinh ben trai.
- Main content rong, table day du cot.
- Dashboard 3-4 cot.
- Form co 2 cot.

### 25.2 Tablet

- Sidebar co the collapse.
- Dashboard 2 cot.
- Table co horizontal scroll neu can.
- Modal max-width nho hon.

### 25.3 Mobile

- Sidebar thanh drawer.
- Navbar gon, search co the full-screen overlay.
- Dashboard 1 cot.
- Table chuyen sang card list neu can.
- Button full width trong form quan trong.

Breakpoint goi y:

```text
sm: 640px
md: 768px
lg: 1024px
xl: 1280px
2xl: 1536px
```

## 26. Accessibility

Can dam bao:

- Contrast text dat muc doc duoc.
- Button co focus ring.
- Input co label.
- Icon button co aria-label/title.
- Modal trap focus neu co the.
- Khong chi dung mau de truyen dat trang thai.
- Text trong button khong bi tran.
- Anh co alt phu hop.

Mau focus:

```text
Light focus ring: rgba(16, 185, 129, 0.25)
Dark focus ring: rgba(52, 211, 153, 0.25)
```

## 27. Internationalization

Frontend ho tro:

- Tieng Viet.
- Tieng Anh.

Yeu cau chat luong:

- Khi chuyen sang English, tat ca menu/page/button/empty/error/toast can la English.
- Khong de nua Viet nua Anh.
- Khong dung tieng Viet khong dau trong toast.
- Text nen quan ly tap trung de de bao tri.

## 28. API integration

Frontend goi API qua client dung chung.

Local:

```env
VITE_API_BASE_URL=http://localhost:5000/api
```

Deploy voi Amplify rewrite:

```env
VITE_API_BASE_URL=/api
```

Amplify rewrite can dam bao:

```text
/api/<*> -> API Gateway/Elastic Beanstalk backend
/<*> -> /index.html
```

Neu route React nhu `/login` bi 404 khi refresh, can co SPA rewrite:

```json
{
  "source": "/<*>",
  "status": "404-200",
  "target": "/index.html"
}
```

## 29. De xuat style cho template bao cao

### 29.1 Trang bia

Nen:

```text
Gradient navy: #062B49 -> #0F172A
Accent: emerald #10B981
Text: #FFFFFF
Subtitle: #CBD5E1
```

Bo cuc:

- Logo EAM Workspace dat giua hoac goc trai tren.
- Tieu de: "Bao cao du an EAM Workspace".
- Subtitle: "Enterprise Asset Management System".
- Thanh accent emerald mong o duoi tieu de.

### 29.2 Trang muc luc

Nen:

```text
Background: #F8FAFC
Heading: #062B49
Accent number: #10B981
```

### 29.3 Trang noi dung

Bo cuc:

- Header nho co logo icon + ten chuong.
- Footer co so trang va ten du an.
- Heading navy.
- Bullet dung dau cham emerald.
- Bang co header nen emerald rat nhat.

### 29.4 Trang chuong moi

Nen:

```text
Background: #0F172A
Large chapter number: rgba(16, 185, 129, 0.18)
Title: #FFFFFF
Subtitle: #CBD5E1
```

### 29.5 Trang screenshot UI

Nen:

- Nen `#F8FAFC`.
- Screenshot dat trong frame bo tron 16px.
- Shadow mem.
- Caption mau `#64748B`.
- Neu screenshot dark mode, nen trang phai co border de tach nen.

### 29.6 Trang ket qua/demo

Nen:

```text
Background: #ECFDF5
Heading: #065F46
Badge: #10B981
```

Dung cho:

- Ket qua deploy.
- Health OK.
- Test login thanh cong.
- Cac tinh nang hoan thanh.

## 30. Mau chart cho bao cao/dashboard

Dung bo mau:

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

## 31. Doan mo ta ngan co the dua vao bao cao

Frontend cua EAM Workspace duoc xay dung bang React, Vite va Tailwind CSS, theo phong cach modern SaaS dashboard phu hop voi he thong quan ly tai san doanh nghiep. Giao dien duoc chia thanh Admin Portal va Employee Portal, moi portal co layout, sidebar, navbar va cac man hinh nghiep vu rieng. He thong ho tro light/dark mode, song ngu Viet-Anh, toast notification, global search, responsive layout va cac thanh phan UI tai su dung nhu card, table, form, modal, badge va button. Mau sac chu dao la navy, emerald va slate, tao cam giac chuyen nghiep, hien dai va dong bo voi logo EAM Workspace. Frontend duoc deploy len AWS Amplify va giao tiep voi Backend thong qua API Gateway/Elastic Beanstalk bang duong dan `/api`.

## 32. Checklist UI truoc khi demo

- Dang nhap admin thanh cong.
- Dang nhap user thanh cong.
- Tai khoan inactive bi chan.
- Refresh `/login`, `/admin/dashboard`, `/employee/dashboard` khong bi 404.
- Dark mode tren Admin dashboard doc ro.
- Dark mode tren Employee tai san/ho so/cam nang doc ro.
- Sidebar active/hover khong lam mat chu.
- Search navbar hoat dong.
- Toast hien thi tieng Viet co dau.
- Table co loading/empty state.
- Import Excel hien thi ket qua ro.
- Upload avatar hien thi ngay sau khi cap nhat.
- Anh upload qua deploy khong bi 404.
- Mobile khong tran text, khong vo layout.
- API `/api/health` OK tren domain deploy.

## 33. Checklist template bao cao

Khi dua tai lieu nay sang template bao cao, nen yeu cau template:

- Doi mau chu dao sang navy/emerald/slate.
- Dung logo EAM Workspace tren bia va header.
- Thay cac mau cam/tim/beige khong lien quan neu template mau dang dung.
- Dung Inter/Segoe UI thay cho font trang tri.
- Dung table header emerald nhat.
- Dung code block nen navy dam.
- Dung screenshot frame co radius 16px va shadow mem.
- Dung badge mau theo semantic status.
- Them trang rieng cho Admin Portal, Employee Portal, Backend Architecture va AWS Deployment.

## 34. Tom tat nhan dien hinh anh

Neu can gui cho nguoi sua template, co the gui doan nay:

```text
Du an EAM Workspace co phong cach modern SaaS / premium enterprise dashboard.
Mau chinh la navy dam (#062B49, #0F172A), emerald (#10B981, #059669), teal/cyan (#14B8A6, #38BDF8) va slate neutral (#64748B, #E2E8F0, #F8FAFC).
Logo la bieu tuong khoi tai san mau navy/trang ket hop shield check emerald.
Template bao cao nen sach, hien dai, nhieu khoang trang, heading navy, accent emerald, table gon, card bo tron 14-18px, shadow mem.
Tranh dung mau be/cam/tim qua nhieu vi khong hop voi nhan dien project.
```
