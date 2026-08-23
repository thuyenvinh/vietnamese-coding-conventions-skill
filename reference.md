# Tài liệu tham khảo đầy đủ — Quy ước đặt tên tiếng Việt

Chi tiết bổ sung cho [SKILL.md](SKILL.md): bảng viết tắt chuẩn, ví dụ code đầy đủ, cấu trúc thư mục đề xuất. Tải file này khi cần tra cứu viết tắt hoặc xem ví dụ implement cụ thể.

## Bảng viết tắt chuẩn

Dùng thống nhất toàn dự án. Không tự sáng tạo viết tắt mới khi chưa cập nhật bảng này.

| Từ đầy đủ | Viết tắt | Ví dụ áp dụng |
|---|---|---|
| Thông tin | TT | `TTNhanVien` thay cho `ThongTinNhanVien` |
| Chi tiết | CT | `CTDonHang` thay cho `ChiTietDonHang` |
| Danh sách | DS | `DSNhanVien` thay cho `DanhSachNhanVien` |
| Danh mục | DM | `DMSanPham` thay cho `DanhMucSanPham` |
| Số lượng | SL | `SLTon`, `SLBan` |
| Số thứ tự | STT | `STTDong` |
| Đơn vị | DV | `DVTinh`, `DVHanhChinh` |
| Trạng thái | *(xung đột với TT)* → dùng `TrangThai` đầy đủ | `TrangThaiDonHang` |
| Loại | *(không tắt)* | `LoaiSanPham` |
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
| Cập nhật | *(không tắt — method)* | `CapNhatNhanVien()` |
| Khách hàng | KH | `KHThanThiet`, `MaKH` |
| Nhà cung cấp | NCC | `MaNCC`, `DSNCC` |
| Hợp đồng | HD | `HDLaoDong`, `MaHD` |
| Hóa đơn | *(xung đột với HD)* → dùng `HoaDon` đầy đủ | `MaHoaDon` |

> **Lưu ý xung đột**: Khi 2 từ viết tắt trùng nhau (TT = Thông tin / Trạng thái, HD = Hợp đồng / Hóa đơn), **giữ từ đầy đủ cho cả hai** để tránh nhầm lẫn.

### Quy tắc áp dụng

1. Ưu tiên giữ tên đầy đủ nếu dưới 30 ký tự và đọc dễ.
2. Chỉ viết tắt phần bổ nghĩa, không viết tắt từ chính.
3. Viết tắt phải nằm trong bảng trên — không tự sáng tạo viết tắt mới khi chưa cập nhật bảng.
4. Viết tắt giữ PascalCase: `CTDonHang` ✅, không phải `ctDonHang` hay `CT_DonHang`.
5. Database column có thể dùng UPPERCASE viết tắt: `[Column("MAKH")]`, `[Column("SLTON")]`.
6. Method, biến ưu tiên đầy đủ vì IDE đã có autocomplete: `LayDanhSachNhanVien()` tốt hơn `LayDSNV()`.
7. Class entity và DTO mới được phép tắt nhiều, vì xuất hiện ở nhiều nơi.

### Ví dụ so sánh độ dài

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

## Ví dụ code

### Entity & Database

File và class trùng tên (`NhanVien.cs` chứa `class NhanVien`). Class PascalCase tiếng Việt không dấu, mapping `[Table("UPPERCASE")]`/`[Column("UPPERCASE")]`, property có `[Display(Name = "...")]` tiếng Việt có dấu cho UI, validation message tiếng Việt có dấu.

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

**Mapping trực tiếp với database**: đối với bảng mà class map TRỰC TIẾP tới table (không phải view/projection), có thể đặt tên class và property giống hệt tên table/cột (UPPERCASE) để nhất quán với schema, dễ dò log/SQL, tránh nhầm lẫn khi mapping — nếu cả team thống nhất dùng cách này.

```csharp
[Table("NHANVIEN")]
public class NHANVIEN
{
    [Key]
    [Column("MANV")]
    public int MANV { get; set; }

    [Column("HOTEN")]
    public string HOTEN { get; set; }
}
```

Cả hai cách (PascalCase truyền thống + attribute mapping, hoặc UPPERCASE trùng schema) đều được chấp nhận nhưng cần thống nhất toàn dự án.

### Database View

Tên view: `VW_TenView` (uppercase phần `VW_`, PascalCase phần tên). Class: `TenViewView` với hậu tố `View` và `[Keyless]`.

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

### DTO

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

### ViewModel

```csharp
public class DSNhanVienViewModel
{
    public List<NhanVienDto> DanhSach { get; set; }
    public int TongSo { get; set; }
    public int TrangHienTai { get; set; }
    public int SoTrang { get; set; }
}
```

### Service & Repository

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

### Controller & Route

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

### ASP.NET Core Identity

TUYỆT ĐỐI KHÔNG đổi tên bảng Identity mặc định: `AspNetUsers`, `AspNetRoles`, `AspNetUserRoles`, `AspNetUserClaims`, `AspNetRoleClaims`, `AspNetUserLogins`, `AspNetUserTokens`. Chỉ extend bằng custom property.

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

## Cấu trúc thư mục đề xuất

Áp dụng cho dự án .NET có nhiều layer (điều chỉnh tương ứng cho stack khác):

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
