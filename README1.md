```mermaid
classDiagram
    direction TB

    %% Entities (Model)
    class NguoiDung
    class TaiKhoan
    class Sach
    class PhieuMuon
    class ChiTietPhieuMuon

    %% Services (Business Logic)
    class AuthService
    class SachService
    class NguoiDocService
    class MuonTraService

    %% Controllers (API)
    class AuthController
    class SachController
    class NguoiDocController
    class MuonTraController

    %% Repositories (Data Access) - đánh dấu interface
    class NguoiDungRepository
    class TaiKhoanRepository
    class SachRepository
    class PhieuMuonRepository
    class ChiTietPhieuMuonRepository

    %% gắn nhãn interface (cú pháp annotation)
    NguoiDungRepository : <<Interface>>
    TaiKhoanRepository : <<Interface>>
    SachRepository : <<Interface>>
    PhieuMuonRepository : <<Interface>>
    ChiTietPhieuMuonRepository : <<Interface>>

    %% Quan hệ (dấu ..> là dependency / sử dụng)
    AuthController ..> AuthService
    SachController ..> SachService
    NguoiDocController ..> NguoiDocService
    MuonTraController ..> MuonTraService

    AuthService ..> NguoiDungRepository
    AuthService ..> TaiKhoanRepository
    SachService ..> SachRepository
    NguoiDocService ..> NguoiDungRepository
    MuonTraService ..> PhieuMuonRepository
    MuonTraService ..> ChiTietPhieuMuonRepository
    MuonTraService ..> SachRepository

    NguoiDungRepository ..> NguoiDung
    TaiKhoanRepository ..> TaiKhoan
    SachRepository ..> Sach
    PhieuMuonRepository ..> PhieuMuon
    ChiTietPhieuMuonRepository ..> ChiTietPhieuMuon
