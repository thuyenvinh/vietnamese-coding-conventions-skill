---
name: vietnamese-coding-conventions
description: Use this skill when writing, reviewing, or renaming code, database schema, API routes, or UI text for a project that follows Vietnamese naming conventions. Language/stack-agnostic — applies to any backend or frontend stack (.NET, Java, Node.js/TypeScript, PHP, Python, etc). Covers class/file/method/variable names (Vietnamese without diacritics, casing per the language's own convention), database table/column names (UPPERCASE without diacritics), UI text such as labels/buttons/validation/toast messages (Vietnamese with diacritics), route URLs (kebab-case without diacritics), and the standard Vietnamese abbreviation table for long identifiers. Trigger whenever creating or renaming entities/models, DTOs, ViewModels, database tables/columns, controllers/routes, or Vietnamese UI copy, in any programming language.
---

# Quy ước đặt tên tiếng Việt (Vietnamese Coding Conventions)

Bộ quy tắc đặt tên cho code, database và UI text của dự án tiếng Việt. Các quy tắc **không phụ thuộc ngôn ngữ/stack cụ thể** — áp dụng cho .NET, Java, Node.js/TypeScript, PHP, Python, frontend... và mọi AI/LLM hỗ trợ code (Claude, Copilot, ChatGPT, Cursor...). Ví dụ code cụ thể theo từng stack (trong đó .NET chỉ là một trong nhiều ví dụ) nằm ở [reference.md](reference.md#ví-dụ-theo-từng-stack).

## Nguyên tắc vàng

Mọi thứ người dùng cuối nhìn thấy → tiếng Việt **CÓ DẤU**. Mọi thứ máy/IDE/compiler đọc → tiếng Việt **KHÔNG DẤU**.

| Thành phần | Ngôn ngữ | Ví dụ |
|---|---|---|
| Class, file, biến, method, namespace | KHÔNG DẤU, PascalCase | `NhanVien`, `LayDanhSach()` |
| Tên bảng, cột database | UPPERCASE KHÔNG DẤU | `NHANVIEN`, `HOTEN` |
| Label, button, validation, toast, placeholder | CÓ DẤU | `"Họ và tên"`, `"Lưu"` |
| Comment giải thích logic phức tạp | CÓ DẤU | `// Kiểm tra mã nhân viên hợp lệ` |
| Route URL | kebab-case KHÔNG DẤU | `api/nhan-vien` |
| Commit message, PR title | CÓ DẤU hoặc tiếng Anh | `feat: thêm chức năng duyệt đơn hàng` |

## Quy tắc viết tắt cho tên dài

- Chỉ viết tắt khi tên đầy đủ vượt **30 ký tự** hoặc gây khó đọc.
- Chỉ viết tắt **phần bổ nghĩa**, giữ nguyên từ chính: `CTDonHang` ✅ (tắt "Chi tiết", giữ "DonHang") — không phải `ChiTietDH` ❌.
- Viết tắt phải nằm trong **bảng chuẩn** ở [reference.md § Bảng viết tắt chuẩn](reference.md#bảng-viết-tắt-chuẩn) — không tự sáng tạo viết tắt mới khi chưa cập nhật bảng.
- Viết tắt giữ PascalCase: `CTDonHang`, không phải `ctDonHang` hay `CT_DonHang`.
- Method/biến ưu tiên giữ tên đầy đủ (IDE đã có autocomplete). Entity/DTO được phép viết tắt nhiều hơn vì xuất hiện lặp lại ở nhiều nơi.

Bảng viết tắt đầy đủ và ví dụ so sánh độ dài tên: xem [reference.md](reference.md#bảng-viết-tắt-chuẩn).

## Entity/Model, DTO, ViewModel, Repository/Service, Controller

Mẫu đặt tên chung dưới đây áp dụng cho mọi stack — chỉ khác cơ chế mapping (attribute/annotation/decorator) và quy ước casing method riêng của từng ngôn ngữ (PascalCase cho C#; camelCase cho Java, JavaScript/TypeScript, PHP, Python...). Tên tiếng Việt không dấu vẫn giữ nguyên bất kể casing.

- **Entity/Model** map trực tiếp DB: tên PascalCase tiếng Việt không dấu (`NhanVien`); tên bảng/cột UPPERCASE không dấu khai báo qua cơ chế mapping của framework (`[Table]`/`[Column]` trong .NET, `@Table`/`@Column` trong Java, decorator `@Entity`/`@Column` trong TypeORM...). Nếu cả team thống nhất, class/property có thể trùng UPPERCASE với schema để dễ dò log/SQL — chọn một cách và dùng nhất quán toàn dự án.
- **Database view**: tên view `VW_TenView`; model tương ứng có hậu tố `View`, chỉ đọc.
- **DTO** (data transfer object / request-response object): hậu tố `Dto`, 4 biến thể chuẩn: `XDto` (trả về đầy đủ), `TaoXDto` (input tạo mới), `CapNhatXDto` (input cập nhật), `TomTatXDto` (tóm tắt cho dropdown/list).
- **ViewModel/Presenter**: hậu tố `ViewModel` (khuyến nghị) — không trộn lẫn với hậu tố `VM` trong cùng dự án.
- **Repository/Service**: interface `I` + tên + hậu tố (`Repository`/`Service`) khi ngôn ngữ hỗ trợ interface; method giữ tên đầy đủ, casing theo convention chuẩn của ngôn ngữ. Tiền tố chuẩn: `Lay`, `Them`, `CapNhat`, `Xoa`, `KiemTra`, `Tinh`, `Tao`, `Duyet`, `HuyBo`, `XuatFile`, `NhapFile`, `GuiEmail`.
- **Controller/Route handler**: tên `TenController` (hoặc tương đương theo framework); route kebab-case không dấu; action/method theo casing chuẩn của ngôn ngữ.
- **Bảng hệ thống mặc định của framework** (auth/identity, ví dụ ASP.NET Core Identity: `AspNetUsers`, `AspNetRoles`...): TUYỆT ĐỐI KHÔNG đổi tên. Chỉ extend bằng property/field riêng.
- **UI/UX** (bất kỳ framework frontend nào — Razor Pages, Blazor, React, Vue, Angular...): label/button/validation/toast/placeholder/tooltip/breadcrumb đều CÓ DẤU. Tên component vẫn KHÔNG DẤU (`NhanVienList.tsx`, `DonHangForm.vue`).

Ví dụ code đầy đủ theo từng stack (.NET, Java, Node.js/TypeScript): xem [reference.md § Ví dụ theo từng stack](reference.md#ví-dụ-theo-từng-stack).

## Checklist trước khi commit

- [ ] Class/file/biến/method: tiếng Việt không dấu, PascalCase/camelCase.
- [ ] Tên bảng/cột DB: UPPERCASE không dấu.
- [ ] UI text (`Display`, validation, placeholder, button, toast): tiếng Việt có dấu.
- [ ] Tên dài > 30 ký tự đã viết tắt theo bảng chuẩn (không tự chế viết tắt mới).
- [ ] Bảng Identity mặc định giữ nguyên tên.
- [ ] Route URL kebab-case không dấu.
- [ ] Comment giải thích logic phức tạp đã viết tiếng Việt có dấu.

## Khi quy ước chưa đủ

Không tự bịa viết tắt hoặc quy tắc mới. Nếu chưa có trong bảng chuẩn hoặc chưa được tài liệu này bao quát, giữ tên đầy đủ/rõ nghĩa và đề xuất bổ sung vào `reference.md` qua PR — nêu rõ lý do trong mô tả PR, cần ít nhất 1 reviewer duyệt trước khi merge, thông báo team sau khi merge.
