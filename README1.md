# Đồ án Quản lý Thư viện

## 1. Sơ đồ Lớp Thực thể (Entities)

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
2. Sơ đồ Kiến trúc (Tương tác)
Đoạn mã

classDiagram
    direction TB

    %% Định nghĩa các lớp trong từng gói (layer)
    subgraph "1. Entities (Model)"
        direction LR
        NguoiDung
        TaiKhoan
        Sach
        PhieuMuon
        ChiTietPhieuMuon
    end

    subgraph "2. Services (Business Logic)"
        direction LR
        AuthService
        SachService
        NguoiDocService
        MuonTraService
    end

    subgraph "3. Controllers (API)"
        direction LR
        AuthController
        SachController
        NguoiDocController
        MuonTraController
    end

    subgraph "4. Repositories (Data Access)"
        direction LR
        class NguoiDungRepository {
            <<Interface>>
        }
        class TaiKhoanRepository {
            <<Interface>>
        }
        class SachRepository {
            <<Interface>>
        }
        class PhieuMuonRepository {
            <<Interface>>
        }
        class ChiTietPhieuMuonRepository {
            <<Interface>>
        }
    end

    %% Liên kết phụ thuộc (Dấu ..> nghĩa là "sử dụng")
    
    %% Controllers -> Services
    AuthController ..> AuthService
    SachController ..> SachService
    NguoiDocController ..> NguoiDocService
    MuonTraController ..> MuonTraService

    %% Services -> Repositories
    AuthService ..> NguoiDungRepository
    AuthService ..> TaiKhoanRepository
    SachService ..> SachRepository
    NguoiDocService ..> NguoiDungRepository
    MuonTraService ..> PhieuMuonRepository
    MuonTraService ..> ChiTietPhieuMuonRepository
    MuonTraService ..> SachRepository

    %% Repositories -> Entities
    NguoiDungRepository ..> NguoiDung
    TaiKhoanRepository ..> TaiKhoan
    SachRepository ..> Sach
    PhieuMuonRepository ..> PhieuMuon
    ChiTietPhieuMuonRepository ..> ChiTietPhieuMuon
