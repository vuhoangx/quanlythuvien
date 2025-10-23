```markdown
classDiagram
    direction TB

    %% 1. Lớp Thực thể (Entities)
    subgraph "Entities (Model)"
        NguoiDung {
            -id: int
            -hoTen: String
            -email: String
            -soDienThoai: String
            -vaiTro: Enum
        }
        TaiKhoan {
            -tenDangNhap: String
            -matKhau: String
        }
        Sach {
            -id: int
            -tenSach: String
            -tacGia: String
            -nhaXuatBan: String
            -namXuatBan: int
            -soLuongTong: int
            -soLuongConLai: int
        }
        PhieuMuon {
            -id: int
            -ngayMuon: Date
            -ngayHenTra: Date
            -trangThai: String
        }
        ChiTietPhieuMuon {
            -id: int
            -ngayTraThucTe: Date
        }
        
        NguoiDung "1" -- "1" TaiKhoan : "sở hữu"
        PhieuMuon "1" *-- "N" ChiTietPhieuMuon : "có"
        ChiTietPhieuMuon "N" -- "1" Sach : "mượn"
        PhieuMuon "N" -- "1" NguoiDung : "nguoiDoc"
        PhieuMuon "N" -- "1" NguoiDung : "thuThu"
    end

    %% 2. Lớp Truy cập Dữ liệu (Repositories)
    subgraph "Repositories (Data Access)"
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

    %% 3. Lớp Dịch vụ (Services)
    subgraph "Services (Business Logic)"
        AuthService {
            +dangNhap(String, String)
        }
        SachService {
            +themSach(Sach)
            +capNhatThongTinSach(int, Sach)
            +xoaSach(int)
            +timKiemSach(String)
        }
        NguoiDocService {
            +themNguoiDoc(NguoiDung)
            +capNhatThongTinNguoiDoc(int, NguoiDung)
            +xoaNguoiDoc(int)
        }
        MuonTraService {
            +taoPhieuMuon(int, List~int~, int)
            +traSach(int)
            +xemLichSuMuonTra(int)
        }
    end

    %% 4. Lớp Điều khiển (Controllers)
    subgraph "Controllers (API)"
        AuthController {
            +handleDangNhap(request)
        }
        SachController {
            +handleThemSach(request)
            +handleCapNhatSach(request)
            +handleXoaSach(request)
            +handleTimKiemSach(request)
        }
        NguoiDocController {
            +handleThemNguoiDoc(request)
            +handleCapNhatNguoiDoc(request)
            +handleXoaNguoiDoc(request)
        }
        MuonTraController {
            +handleMuonSach(request)
            +handleTraSach(request)
            +handleXemLichSu(request)
        }
    end

    %% Mối quan hệ phụ thuộc giữa các lớp
    Controllers ..> Services
    Services ..> Repositories
    Repositories ..> Entities
    Services ..> Entities
```
