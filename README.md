# Đồ án Quản lý Thư viện

Đây là dự án quản lý thư viện, xây dựng dựa trên sơ đồ use case.

## 1. Sơ đồ Lớp Thực thể (Entities)

Sơ đồ này mô tả cấu trúc dữ liệu cốt lõi và cách chúng liên kết với nhau.

```mermaid
classDiagram
    direction LR

    class NguoiDung {
        -id: int
        -hoTen: String
        -email: String
        -soDienThoai: String
        -vaiTro: Enum
    }

    class TaiKhoan {
        -tenDangNhap: String
        -matKhau: String
    }

    class Sach {
        -id: int
        -tenSach: String
        -tacGia: String
        -theLoai: String
        -nhaXuatBan: String
        -namXuatBan: int
        -soLuongTong: int
        -soLuongConLai: int
    }

    class PhieuMuon {
        -id: int
        -ngayMuon: Date
        -ngayHenTra: Date
        -trangThai: String
    }

    class ChiTietPhieuMuon {
        -id: int
        -ngayTraThucTe: Date
    }

    %% Mối quan hệ giữa các thực thể
    NguoiDung "1" -- "1" TaiKhoan : "sở hữu"
    
    PhieuMuon "1" *-- "N" ChiTietPhieuMuon : "có"
    
    ChiTietPhieuMuon "N" -- "1" Sach : "mượn"
    
    PhieuMuon "1" -- "1" NguoiDung : "nguoiDoc"
    PhieuMuon "1" -- "1" NguoiDung : "thuThu"
