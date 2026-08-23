# Quy ước đặt tên dự án

Tài liệu này định nghĩa quy ước đặt tên cho toàn bộ dự án. Mọi code mới (do người hoặc AI tạo ra) đều phải tuân thủ. Khi sửa code cũ chưa theo quy ước, refactor dần dần — không sửa hàng loạt nếu chưa được duyệt.

## 1. Nguyên tắc cốt lõi

| Thành phần | Ngôn ngữ | Ví dụ |
|---|---|---|
| Tên class, file, biến, method, namespace | **Tiếng Việt KHÔNG DẤU** | `NhanVien`, `LayDanhSach()` |
| Tên bảng, cột database | **UPPERCASE KHÔNG DẤU** | `NHANVIEN`, `HOTEN` |
| Label, button, message, validation, placeholder | **Tiếng Việt CÓ DẤU** | `"Họ và tên"`, `"Lưu"` |
| Comment trong code | **Tiếng Việt CÓ DẤU** | `// Kiểm tra mã nhân viên hợp lệ` |
| Commit message, PR title | **Tiếng Việt CÓ DẤU** hoặc tiếng Anh | `feat: thêm chức năng duyệt đơn hàng` |
| Route URL | **kebab-case không dấu** | `api/nhan-vien`, `api/don-hang` |

**Nguyên tắc vàng**: Bất cứ thứ gì người dùng cuối nhìn thấy → CÓ DẤU. Bất cứ thứ gì máy/compiler đọc → KHÔNG DẤU.

## 2. Quy tắc viết tắt cho tên dài

Khi tên đầy đủ vượt **30 ký tự** hoặc gây khó đọc, áp dụng viết tắt theo thứ tự ưu tiên sau:

### 2.1. Bảng từ viết tắt chuẩn (dùng thống nhất toàn dự án)

| Từ đầy đủ | Viết tắt | Ví dụ áp dụng |
|---|---|---|
| Thông tin | TT | `TTNhanVien` thay cho `ThongTinNhanVien` |
| Chi tiết | CT | `CTDonHang` thay cho `ChiTietDonHang` |
| Danh sách | DS | `DSNhanVien` thay cho `DanhSachNhanVien` |
| Danh mục | DM | `DMSanPham` thay cho `DanhMucSanPham` |
| Số lượng | SL | `SLTon`, `SLBan` |
| Số thứ tự | STT | `STTDong` |
| Đơn vị | DV | `DVTinh`, `DVHanhChinh` |
| Trạng thái | TT *(xung đột)* → dùng `TrangThai` đầy đủ | `TrangThaiDonHang` |
| Loại | Loai *(không tắt)* | `LoaiSanPham` |
| Mã | Ma | `MaNhanVien`, `MaDonHang` |
| Số | So | `SoHoaDon`, `SoDienThoai` |
| Tên | Ten | `TenSanPham` |
| Ngày | Ngay | `NgaySinh`, `NgayLap` |
| Giờ | Gio | `GioVao`, `GioRa` |
| Tổng | Tong | `TongTien`, `TongSL` |
| Quản lý | QL | `QLNhanVien`, `QLKhoHang` |
| Hệ thống | HT | `HTPhanQuyen` |
| Báo cáo | BC | `BCDoanhThu`, `BCTonKho` |
| Phòng ban | PB | `PBKeToan` |
| Phiếu | P | `PNhap`, `PXuat`, `PThu`, `PChi` |
| Kiểm tra | KT | `KTHopLe()` |
| Cập nhật | CapNhat *(không tắt — method)* | `CapNhatNhanVien()` |
| Khách hàng | KH | `KHThanThiet`, `MaKH` |
| Nhà cung cấp | NCC | `MaNCC`, `DSNCC` |
| Hợp đồng | HD | `HDLaoDong`, `MaHD` |
| Hóa đơn | HD *(xung đột)* → dùng `HoaDon` đầy đủ | `MaHoaDon` |

> **Lưu ý xung đột**: Khi 2 từ viết tắt trùng nhau (TT = Thông tin / Trạng thái, HD = Hợp đồng / Hóa đơn), **giữ từ đầy đủ cho cả hai** để tránh nhầm lẫn.

### 2.2. Quy tắc áp dụng

1. **Ưu tiên giữ tên đầy đủ** nếu dưới 30 ký tự và đọc dễ.
2. **Chỉ viết tắt phần bổ nghĩa**, không viết tắt từ chính.
   - ✅ `CTDonHang` (tắt "Chi tiết", giữ "DonHang")
   - ❌ `ChiTietDH` (giữ phần bổ nghĩa, tắt từ chính → khó đọc)
3. **Viết tắt phải nằm trong bảng 2.1** — không tự sáng tạo viết tắt mới khi chưa cập nhật bảng.
4. **Viết tắt giữ PascalCase**: `CTDonHang` ✅, không phải `ctDonHang` hay `CT_DonHang`.
5. **Database column** có thể dùng UPPERCASE viết tắt: `[Column("MAKH")]`, `[Column("SLTON")]`.
6. **Method, biến** ưu tiên đầy đủ vì IDE đã có autocomplete: `LayDanhSachNhanVien()` tốt hơn `LayDSNV()`.
7. **Class entity và DTO** mới được phép tắt nhiều, vì xuất hiện ở nhiều nơi.

### 2.3. Ví dụ so sánh

| Tên đầy đủ | Độ dài | Tên đề xuất | Ghi chú |
|---|---|---|---|
| `NhanVien` | 8 | `NhanVien` | Giữ nguyên |
| `ChiTietDonHang` | 14 | `ChiTietDonHang` | Giữ nguyên |
| `ChiTietHoaDonNhapKho` | 20 | `ChiTietHoaDonNhapKho` | Giữ nguyên |
| `DanhSachNhanVienTheoPhongBan` | 28 | `DanhSachNhanVienTheoPhongBan` | Giữ nguyên |
| `ThongTinChiTietDonHangNhapKho` | 30 | `TTCTDonHangNhapKho` | Tắt "Thông tin", "Chi tiết" |
| `BaoCaoTongHopDoanhThuTheoPhongBanTheoThang` | 43 | `BCTongHopDoanhThuPBThang` | Tắt "Báo cáo", "Phòng ban" |
| `LichSuCapNhatTrangThaiDonHang` | 30 | `LichSuCapNhatTrangThaiDonHang` | Đủ rõ, giữ nguyên |
| `PhieuYeuCauNhapKhoTuKhachHang` | 30 | `PYCNhapKhoTuKH` | Tắt "Phiếu yêu cầu", "Khách hàng" |

## 3. Entity & Database

### 3.1. Class entity
- File và class trùng tên: `NhanVien.cs` chứa `class NhanVien`.
- Class: PascalCase tiếng Việt không dấu.
- Mapping: `[Table("UPPERCASE")]`, `[Column("UPPERCASE")]`.
- Property: PascalCase không dấu, có `[Display(Name = "...")]` tiếng Việt có dấu cho UI.
- Validation message: tiếng Việt có dấu.

```csharp
[Table("NHANVIEN")]
public class NhanVien
{
    [Key]
    [Column("MANV")]
    public int MaNhanVien { get; set; }

    [Column("HOTEN")]
    [MaxLength(100)]
    [Display(Name = "Họ và tên")]
    [Required(ErrorMessage = "Vui lòng nhập họ tên")]
    public string HoTen { get; set; }

    [Column("NGAYSINH")]
    [Display(Name = "Ngày sinh")]
    [DataType(DataType.Date)]
    public DateTime NgaySinh { get; set; }

    [Column("MAPB")]
    [Display(Name = "Phòng ban")]
    public int MaPhongBan { get; set; }

    public virtual PhongBan PhongBan { get; set; }
}
```

### 3.2. Database View
- Tên view: `VW_TenView` (uppercase phần `VW_`, PascalCase phần tên).
- Class: `TenViewView` với hậu tố `View` và `[Keyless]`.

```csharp
[Table("VW_TTDonHang")]
[Keyless]
public class TTDonHangView
{
    public int MaDonHang { get; set; }
    public string TenKhachHang { get; set; }
    public decimal TongTien { get; set; }
}
```

## 4. DTO (Data Transfer Object)

- Hậu tố `Dto`. Có 4 biến thể chuẩn:

```csharp
public class NhanVienDto             // Trả về cho client (đầy đủ)
public class TaoNhanVienDto          // Input khi tạo mới
public class CapNhatNhanVienDto      // Input khi cập nhật
public class TomTatNhanVienDto       // Trả về tóm tắt (cho dropdown, list)
```

```csharp
public class TaoNhanVienDto
{
    [Required(ErrorMessage = "Vui lòng nhập họ tên")]
    [StringLength(100, ErrorMessage = "Họ tên không quá 100 ký tự")]
    public string HoTen { get; set; }

    [EmailAddress(ErrorMessage = "Email không hợp lệ")]
    public string Email { get; set; }
}
```

## 5. ViewModel

- Hậu tố `ViewModel` hoặc `VM` (chọn 1 và dùng nhất quán toàn dự án — **khuyến nghị `ViewModel`**).

```csharp
public class DSNhanVienViewModel
{
    public List<NhanVienDto> DanhSach { get; set; }
    public int TongSo { get; set; }
    public int TrangHienTai { get; set; }
    public int SoTrang { get; set; }
}
```

## 6. Service & Repository

- Interface: `I` + tên + hậu tố (`Repository` / `Service`).
- Method: PascalCase, tiếng Việt không dấu, **giữ tên đầy đủ** (ưu tiên đọc hiểu).

```csharp
public interface INhanVienRepository
{
    Task<NhanVien> LayTheoMa(int maNhanVien);
    Task<List<NhanVien>> LayDanhSach();
    Task<List<NhanVien>> LayDanhSachTheoPhongBan(int maPhongBan);
    Task<NhanVien> Them(NhanVien nhanVien);
    Task<NhanVien> CapNhat(NhanVien nhanVien);
    Task<bool> Xoa(int maNhanVien);
    Task<bool> KiemTraTonTai(int maNhanVien);
}
```

**Tiền tố method chuẩn**: `Lay`, `Them`, `CapNhat`, `Xoa`, `KiemTra`, `Tinh`, `Tao`, `Duyet`, `HuyBo`, `XuatFile`, `NhapFile`, `GuiEmail`.

## 7. Controller & Route

- Class: `TenController`.
- Route: kebab-case không dấu.
- Action method: PascalCase tiếng Việt không dấu.

```csharp
[ApiController]
[Route("api/nhan-vien")]
public class NhanVienController : ControllerBase
{
    [HttpGet]
    public async Task<ActionResult<List<NhanVienDto>>> LayDanhSach() { }

    [HttpGet("{id}")]
    public async Task<ActionResult<NhanVienDto>> LayTheoMa(int id) { }

    [HttpGet("phong-ban/{maPhongBan}")]
    public async Task<ActionResult> LayTheoPhongBan(int maPhongBan) { }

    [HttpPost]
    public async Task<ActionResult> Them([FromBody] TaoNhanVienDto dto) { }

    [HttpPut("{id}")]
    public async Task<ActionResult> CapNhat(int id, [FromBody] CapNhatNhanVienDto dto) { }

    [HttpDelete("{id}")]
    public async Task<ActionResult> Xoa(int id) { }
}
```

## 8. ASP.NET Core Identity

**TUYỆT ĐỐI KHÔNG đổi tên bảng Identity mặc định**: `AspNetUsers`, `AspNetRoles`, `AspNetUserRoles`, `AspNetUserClaims`, `AspNetRoleClaims`, `AspNetUserLogins`, `AspNetUserTokens`.

Chỉ extend bằng custom property:

```csharp
public class ApplicationUser : IdentityUser
{
    [Column("HOTEN")]
    [Display(Name = "Họ và tên")]
    public string HoTen { get; set; }

    [Column("NGAYSINH")]
    [Display(Name = "Ngày sinh")]
    public DateTime? NgaySinh { get; set; }

    [Column("MAPB")]
    public int? MaPhongBan { get; set; }
}
```

## 9. UI/UX (Frontend)

Dù dùng Razor Pages, Blazor, React, Vue hay framework nào — quy tắc CÓ DẤU áp dụng cho:

- **Label**: `"Họ và tên"`, `"Ngày sinh"`, `"Mã nhân viên"`
- **Button**: `"Lưu"`, `"Hủy"`, `"Thêm mới"`, `"Cập nhật"`, `"Xóa"`, `"Tìm kiếm"`
- **Validation message**: `"Vui lòng nhập họ tên"`, `"Email không hợp lệ"`, `"Mật khẩu phải có ít nhất 8 ký tự"`
- **Toast / notification**: `"Lưu thành công"`, `"Có lỗi xảy ra"`, `"Bạn có chắc muốn xóa?"`
- **Placeholder**: `"Nhập họ và tên..."`, `"Tìm kiếm theo mã..."`
- **Tooltip, header bảng, breadcrumb, page title**: tất cả CÓ DẤU.

Component name (React/Vue) vẫn không dấu: `NhanVienList.tsx`, `DonHangForm.vue`.

## 10. Cấu trúc thư mục đề xuất

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

## 11. Checklist trước khi commit

- [ ] Tên class, file, biến, method: tiếng Việt không dấu PascalCase/camelCase.
- [ ] Tên bảng và cột: UPPERCASE không dấu.
- [ ] `[Display(Name = "...")]`, validation message, label UI: tiếng Việt CÓ DẤU.
- [ ] Tên dài quá 30 ký tự đã viết tắt theo bảng mục 2.1 (không tự chế).
- [ ] Identity table giữ nguyên tên mặc định.
- [ ] Route URL kebab-case không dấu.
- [ ] Comment giải thích logic phức tạp đã viết tiếng Việt có dấu.

## 12. Cập nhật quy ước

Nếu cần thêm từ viết tắt mới hoặc sửa quy tắc:
1. Mở PR sửa file này.
2. Ghi rõ lý do trong PR description.
3. Cần ít nhất 1 reviewer duyệt trước khi merge.
4. Sau khi merge, thông báo cho team trên kênh chat.
