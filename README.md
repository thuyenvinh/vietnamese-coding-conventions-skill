# Quy ước đặt tên và coding convention tiếng Việt

Một bộ quy ước đặt tên và hướng dẫn thực hành (coding conventions) dành cho các dự án do nhóm phát triển ở Việt Nam sử dụng. Mục tiêu: giúp code nhất quán, dễ đọc và dễ bảo trì khi dùng tiếng Việt cho tên code và nhãn giao diện.

Quy tắc **không phụ thuộc ngôn ngữ/stack cụ thể** — ví dụ minh họa có sẵn cho .NET/ASP.NET Core, Java/Spring Boot, Node.js/TypeScript (NestJS) và frontend (React/Vue), dễ áp dụng tương tự cho các ngôn ngữ/framework khác.

Repo này được đóng gói thành một **Claude Skill** (`SKILL.md`), nhưng nội dung quy ước hoàn toàn không phụ thuộc Claude — dùng được với bất kỳ AI coding assistant hoặc IDE nào.

- Chi tiết đầy đủ, luôn cần khi code: [SKILL.md](SKILL.md)
- Bảng viết tắt chuẩn, ví dụ code, cấu trúc thư mục: [reference.md](reference.md)

## Ai nên dùng

- Thành viên đội backend, ở bất kỳ stack nào (.NET, Java, Node.js/TypeScript, PHP, Python...).
- Frontend dev khi cần thống nhất nội dung hiển thị (label, placeholder, thông báo).
- Người review code và viết tài liệu nội bộ.
- Các bot/AI tạo code cho dự án (áp dụng cùng quy ước).

## Dùng làm Claude Skill

Đặt thư mục này vào nơi Claude Code tìm skill (ví dụ `.claude/skills/vietnamese-coding-conventions/` trong dự án, hoặc thư mục skill cá nhân/marketplace của bạn), giữ nguyên `SKILL.md` và `reference.md` cùng cấp. Claude Code sẽ tự đọc `description` trong frontmatter của `SKILL.md` để biết khi nào cần áp dụng skill này (khi tạo/sửa entity, DTO, database, route, UI text tiếng Việt...).

## Dùng với LLM/AI tool khác

Nội dung trong `SKILL.md`/`reference.md` là hướng dẫn thuần văn bản, không có cú pháp riêng của Claude, nên có thể tái sử dụng nguyên văn cho công cụ khác, ví dụ:

- **Claude Code (dự án khác)**: copy nội dung vào `CLAUDE.md` ở root dự án.
- **Cursor**: đặt vào `.cursor/rules/vietnamese-coding-conventions.mdc`.
- **GitHub Copilot**: đặt vào `.github/copilot-instructions.md`.
- **ChatGPT, Gemini, hoặc LLM khác**: dán nội dung `SKILL.md` (+ `reference.md` khi cần tra bảng viết tắt) vào system prompt hoặc custom instructions.

## Những điểm chính

- Nguyên tắc vàng: mọi thứ người dùng cuối nhìn thấy → tiếng Việt CÓ DẤU; mọi thứ máy/IDE/compiler đọc → tiếng Việt KHÔNG DẤU.
- Tên class/file/biến/method: PascalCase, KHÔNG DẤU (ví dụ: `NhanVien`, `LayDanhSach()`).
- Tên bảng/cột DB: UPPERCASE KHÔNG DẤU (ví dụ: `NHANVIEN`, `HOTEN`).
- Label/button/validation/message UI: Tiếng Việt CÓ DẤU (ví dụ: "Họ và tên", "Lưu").
- Route URL: kebab-case KHÔNG DẤU (ví dụ: `api/nhan-vien`).
- Bảng viết tắt chuẩn được đề xuất (ví dụ: TT, CT, DS, DM, SL, PB, KH, NCC, BC) — dùng thống nhất toàn dự án; tránh tự sáng tạo viết tắt nếu chưa được thống nhất. Xem đầy đủ tại [reference.md](reference.md#bảng-viết-tắt-chuẩn).

## Checklist trước khi commit

- Tên class/file/biến/method: tiếng Việt không dấu (PascalCase/camelCase).
- Tên bảng/cột DB: UPPERCASE không dấu.
- UI text (`Display`, validation, placeholder, button, toast): tiếng Việt có dấu.
- Tên dài > 30 ký tự đã áp dụng viết tắt theo bảng chuẩn.
- Không đổi tên bảng Identity mặc định (`AspNetUsers`, ...).
- Route URL: kebab-case không dấu.
- Comment giải thích logic phức tạp: tiếng Việt có dấu.

## Cập nhật quy ước

1. Sửa file `SKILL.md` hoặc `reference.md` bằng PR.
2. Viết rõ lý do thay đổi trong mô tả PR.
3. Cần ít nhất 1 reviewer duyệt trước khi merge.
4. Sau merge, thông báo cho team (chat/channel nội bộ).

## Góp ý & liên hệ

Mọi góp ý hoặc đề xuất viết tắt mới, sửa quy tắc, vui lòng tạo PR sửa `SKILL.md`/`reference.md` hoặc mở issue trong repository.
