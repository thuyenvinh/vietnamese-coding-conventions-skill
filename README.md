# Quy ước đặt tên và coding convention tiếng Việt

Một bộ quy ước đặt tên và những hướng dẫn thực hành (coding conventions) dành cho các dự án .NET/ASP.NET Core (và các stack frontend/khác) do nhóm phát triển ở Việt Nam sử dụng. Mục tiêu: giúp code nhất quán, dễ đọc và dễ bảo trì khi dùng tiếng Việt cho tên code và nhãn giao diện.

Xem tài liệu đầy đủ: [vietnamese-coding-conventions-skill.md](vietnamese-coding-conventions-skill.md)

## Ai nên dùng

- Thành viên đội backend .NET / ASP.NET Core.
- Frontend dev khi cần thống nhất nội dung hiển thị (label, placeholder, thông báo).
- Người review code và viết tài liệu nội bộ.
- Các bot/AI tạo code cho dự án (áp dụng cùng quy ước).

## Những điểm chính

- Nguyên tắc vàng: mọi thứ người dùng cuối nhìn thấy → tiếng Việt CÓ DẤU; mọi thứ máy/IDE/compiler đọc → tiếng Việt KHÔNG DẤU.
- Tên class/file/biến/method: PascalCase, KHÔNG DẤU (ví dụ: `NhanVien`, `LayDanhSach()`).
- Tên bảng/cột DB: UPPERCASE KHÔNG DẤU (ví dụ: `NHANVIEN`, `HOTEN`).
- Label/button/validation/message UI: Tiếng Việt CÓ DẤU (ví dụ: "Họ và tên", "Lưu").
- Route URL: kebab-case KHÔNG DẤU (ví dụ: `api/nhan-vien`).
- Bảng viết tắt chuẩn được đề xuất (ví dụ: TT, CT, DS, DM, SL, PB, KH, NCC, BC) — dùng thống nhất toàn dự án; tránh tự sáng tạo viết tắt nếu chưa được thống nhất.

## Quy tắc viết tắt (tóm tắt)

- Khi tên đầy đủ vượt 30 ký tự hoặc gây khó đọc, áp dụng viết tắt theo bảng chuẩn.
- Chỉ viết tắt phần bổ nghĩa, không viết tắt từ chính.
- Viết tắt phải nằm trong bảng chuẩn — không tự sáng tạo viết tắt mới khi chưa cập nhật bảng.
- Viết tắt giữ PascalCase: `CTDonHang` ✅, không phải `ctDonHang` hay `CT_DonHang`.
- Ví dụ: `TTNhanVien` (Thông tin → TT), `DSNhanVien` (Danh sách → DS), `MaNhanVien` (Mã → Ma).

## Cấu trúc thư mục đề xuất

Gợi ý cấu trúc thư mục (áp dụng cho dự án .NET có nhiều layer):

```
src/
├── Domain/
│   ├── Entities/          NhanVien.cs, DonHang.cs
│   ├── Enums/             TrangThaiDonHang.cs
│   └── Interfaces/        INhanVienRepository.cs
├── Application/
│   ├── DTOs/              NhanVienDto.cs, TaoNhanVienDto.cs
│   ├── ViewModels/        DSNhanVienViewModel.cs
│   ├── Services/          NhanVienService.cs
│   └── Validators/        TaoNhanVienValidator.cs
├── Infrastructure/
│   ├── Data/              ApplicationDbContext.cs
│   ├── Repositories/      NhanVienRepository.cs
│   └── Migrations/
└── Web/ (hoặc Api/)
    ├── Controllers/       NhanVienController.cs
    ├── Pages/ hoặc Views/
    └── wwwroot/
```

## Ví dụ nhanh

- Class entity:

```csharp
[Table("NHANVIEN")]
public class NhanVien
{
    [Key][Column("MANV")]
    public int MaNhanVien { get; set; }

    [Column("HOTEN")]
    [Display(Name = "Họ và tên")]
    public string HoTen { get; set; }
}
```

- Route & controller:

```csharp
[ApiController]
[Route("api/nhan-vien")]
public class NhanVienController : ControllerBase
{
    [HttpGet]
    public async Task<ActionResult<List<NhanVienDto>>> LayDanhSach() { }
}
```

## Checklist trước khi commit

- Tên class/file/biến/method: tiếng Việt không dấu (PascalCase/camelCase).
- Tên bảng/cột DB: UPPERCASE không dấu.
- UI text (`Display`, validation, placeholder, button, toast): tiếng Việt có dấu.
- Tên dài > 30 ký tự đã áp dụng viết tắt theo bảng chuẩn.
- Không đổi tên bảng Identity mặc định (`AspNetUsers`, ...).
- Route URL: kebab-case không dấu.
- Comment giải thích logic phức tạp: tiếng Việt có dấu.

## Cập nhật quy ước

1. Sửa file `vietnamese-coding-conventions-skill.md` bằng PR.
2. Viết rõ lý do thay đổi trong mô tả PR.
3. Cần ít nhất 1 reviewer duyệt trước khi merge.
4. Sau merge, thông báo cho team (chat/channel nội bộ).

## Góp ý & liên hệ

Mọi góp ý hoặc đề xuất viết tắt mới, sửa quy tắc, vui lòng tạo PR sửa file `vietnamese-coding-conventions-skill.md` hoặc mở issue trong repository.

---
README này là bản tóm tắt — nội dung chi tiết và ví dụ đầy đủ nằm trong `vietnamese-coding-conventions-skill.md`.
