classDiagram
    direction TB

    %% Định nghĩa các lớp trong từng gói (layer)
    subgraph "3. Controllers (API)"
        direction LR
        AuthController
        SachController
        NguoiDocController
        MuonTraController
    end

    subgraph "2. Services (Business Logic)"
        direction LR
        AuthService
        SachService
        NguoiDocService
        MuonTraService
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

    subgraph "1. Entities (Model)"
        direction LR
        NguoiDung
        TaiKhoan
        Sach
        PhieuMuon
        ChiTietPhieuMuon
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
