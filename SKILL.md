---
name: vietnamese-coding-conventions
description: Use this skill when writing, reviewing, or renaming code, database schema, API routes, or UI text for a project that follows Vietnamese naming conventions. Applies to class/file/method/variable names (Vietnamese without diacritics, PascalCase/camelCase), database table/column names (UPPERCASE without diacritics), UI text such as labels/buttons/validation/toast messages (Vietnamese with diacritics), route URLs (kebab-case without diacritics), and the standard Vietnamese abbreviation table for long identifiers. Written for .NET/ASP.NET Core but the rules apply to any stack (Node, Java, PHP, frontend frameworks) and any AI coding assistant. Trigger whenever creating or renaming entities, DTOs, ViewModels, database tables/columns, controllers/routes, or Vietnamese UI copy.
---

# Quy ước đặt tên tiếng Việt (Vietnamese Coding Conventions)

Bộ quy tắc đặt tên cho code, database và UI text của dự án tiếng Việt. Áp dụng cho mọi stack (.NET, Node, Java, PHP, frontend...) và mọi AI/LLM hỗ trợ code (Claude, Copilot, ChatGPT, Cursor...) — nội dung không phụ thuộc công cụ cụ thể nào.

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

## Entity, DTO, ViewModel, Service, Controller

- **Entity** map trực tiếp DB: PascalCase không dấu + `[Table("UPPERCASE")]` / `[Column("UPPERCASE")]`. Nếu cả team thống nhất, class/property có thể trùng UPPERCASE với schema để dễ dò log/SQL — chọn một cách và dùng nhất quán toàn dự án.
- **Database view**: tên view `VW_TenView`; class tương ứng có hậu tố `View` và `[Keyless]`.
- **DTO**: hậu tố `Dto`, 4 biến thể chuẩn: `XDto` (trả về đầy đủ), `TaoXDto` (input tạo mới), `CapNhatXDto` (input cập nhật), `TomTatXDto` (tóm tắt cho dropdown/list).
- **ViewModel**: hậu tố `ViewModel` (khuyến nghị) — không trộn lẫn với hậu tố `VM` trong cùng dự án.
- **Repository/Service**: interface `I` + tên + hậu tố (`Repository`/`Service`); method PascalCase, giữ tên đầy đủ. Tiền tố chuẩn: `Lay`, `Them`, `CapNhat`, `Xoa`, `KiemTra`, `Tinh`, `Tao`, `Duyet`, `HuyBo`, `XuatFile`, `NhapFile`, `GuiEmail`.
- **Controller**: `TenController`; route kebab-case không dấu; action method PascalCase không dấu.
- **ASP.NET Core Identity**: TUYỆT ĐỐI KHÔNG đổi tên bảng mặc định (`AspNetUsers`, `AspNetRoles`, `AspNetUserRoles`, `AspNetUserClaims`, `AspNetRoleClaims`, `AspNetUserLogins`, `AspNetUserTokens`). Chỉ extend bằng custom property.
- **UI/UX** (Razor Pages, Blazor, React, Vue, hay framework nào khác): label/button/validation/toast/placeholder/tooltip/breadcrumb đều CÓ DẤU. Tên component vẫn KHÔNG DẤU (`NhanVienList.tsx`, `DonHangForm.vue`).

Ví dụ code đầy đủ cho từng loại ở trên: xem [reference.md § Ví dụ code](reference.md#ví-dụ-code).

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
