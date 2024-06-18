# QUẢN LÝ CỬA HÀNG ĐỒ GỖ NỘI THẤT
BTL: Mon HQT- CSDL
 ## --Thông Tin Cá nhân--
 ### Tác Giả: Lại Chí Bảo   
 ### Lớp: K57KMT.01           
 ### MSSV: K215520216829

 
      
I. Mô tả hệ thống (Quản lý thông tin cửa hàng nội thất)
1. Các chức năng
   - Quản lý Sản Phẩm
   Bảng SanPham chứa thông tin về các sản phẩm đồ gỗ mà cửa hàng bán. Các thông tin này bao gồm:
    Mã sản phẩm (MaSanPham)
    Tên sản phẩm (TenSanPham)
    Loại sản phẩm (LoaiSanPham)
    Giá bán (GiaBan)
    Số lượng tồn kho (SoLuongTon)
    Kích thước (KichThuoc)
    Chất liệu (ChatLieu)
    Màu sắc (MauSac)
   - Quản lý Khách Hàng
     Bảng KhachHang chứa thông tin về khách hàng của cửa hàng. Các thông tin này bao gồm:
     Mã khách hàng (MaKhachHang)
     Tên khách hàng (TenKhachHang)
     Địa chỉ (DiaChi)
     Số điện thoại (SoDienThoai)
     Email (Email)
   - Quản lý Đơn Hàng
     Bảng DonHang chứa thông tin về các đơn hàng mà cửa hàng nhận được từ khách hàng. Các thông tin này bao gồm:
     Mã đơn hàng (MaDonHang)
     Ngày đặt hàng (NgayDatHang)
     Mã khách hàng (MaKhachHang)
     Tổng giá trị đơn hàng (TongGiaTri)
     Tình trạng đơn hàng (TinhTrangDonHang)
    - Quản lý Chi Tiết Đơn Hàng
      Bảng ChiTietDonHang chứa thông tin chi tiết về từng sản phẩm trong mỗi đơn hàng. Các thông tin này bao gồm:
      Mã chi tiết đơn hàng (MaChiTietDonHang)
      Mã đơn hàng (MaDonHang)
      Mã sản phẩm (MaSanPham)
      Số lượng sản phẩm (SoLuong)
      Giá bán của sản phẩm (GiaBan)
    - Quản lý Nhà Cung Cấp
      Bảng NhaCungCap chứa thông tin về các nhà cung cấp sản phẩm cho cửa hàng. Các thông tin này bao gồm:
      Mã nhà cung cấp (MaNhaCungCap)
      Tên nhà cung cấp (TenNhaCungCap)
      Địa chỉ (DiaChi)
      Số điện thoại (SoDienThoai)
    - Chức năng quản lý hàng hóa:
      Liệt Kê Tất Cả Hàng Hóa
      Thêm Một Hàng Hóa
      Xóa Một Hàng Hóa
      Sửa thông tin hàng hóa
    - Chức năng Quản Lý Bán Hàng:
      Thêm Một Hóa Đơn
      Sửa Một Hóa Đơn
      Xóa 1 hóa đơn
      Thêm Một Chi Tiết Hóa Đơn
      Cập Nhật Số Lượng Cho Một Chi Tiết Hóa Đơn
      Xóa Một Dòng Trong Chi Tiết Hóa Đơn
2. Báo cáo
 - Báo Cáo Hàng Tồn
 - Báo Cáo Hàng Bán Nhiều Nhất Trong Tháng
 - Báo Cáo Mặt Hàng Bán Chạy Trong Tháng
 - Cập Nhật Số Lượng Tồn Kho Khi Thêm Chi Tiết Hóa Đơn
 - Cursor Báo Cáo Hàng Bán Trong Tháng
 - Function để tính tổng số lượng sản phẩm trong một đơn hàng dựa trên mã đơn hàng.
   
3. Các bảng của hệ thống được lập
- Bảng KhachHang
  MaKhachHang (Mã khách hàng)
     Mô tả: Mã định danh duy nhất cho mỗi khách hàng.
     PK: Đúng. Đây là trường Primary Key (PK) vì nó sẽ được dùng để xác định duy nhất mỗi khách hàng trong bảng.
     Kiểu dữ liệu: INT (với AUTO_INCREMENT nếu sử dụng MySQL, hoặc SERIAL nếu sử dụng PostgreSQL)
     NULL: NOT NULL. Mã khách hàng không thể là NULL vì nó là PK.
  TenKhachHang (Tên khách hàng)
      Mô tả: Tên của khách hàng.
      PK: Không.
      FK: Không.
      Kiểu dữ liệu: VARCHAR(100)
      NULL: NOT NULL. Tên khách hàng là thông tin bắt buộc.
  DiaChi (Địa chỉ)
      Mô tả: Địa chỉ của khách hàng.
      PK: Không.
      FK: Không.
      Kiểu dữ liệu: VARCHAR(255)
      NULL: Có thể là NULL. Địa chỉ có thể không bắt buộc phải nhập.
  SoDienThoai (Số điện thoại)
      Mô tả: Số điện thoại liên lạc của khách hàng.
      PK: Không.
      FK: Không.
      Kiểu dữ liệu: VARCHAR(15) (hoặc tùy thuộc vào định dạng số điện thoại trong nước hoặc quốc tế)
      NULL: NOT NULL. Số điện thoại là thông tin bắt buộc.
  Email (Email)
     Mô tả: Địa chỉ email của khách hàng.
     PK: Không.
     FK: Không.
     Kiểu dữ liệu: VARCHAR(100)
     NULL: NOT NULL. Email là thông tin bắt buộc.
  [-Bảng Khách hàng-] (![image](https://github.com/baolaichi/Quan_Ly_Cua_hang_Noi_That/assets/131328468/a3a92715-2c73-4385-8ae9-cedfb79a2adc))

                           
- Bảng SanPham
Bảng SanPham chứa thông tin về các sản phẩm đồ gỗ mà cửa hàng bán. Dưới đây là mô tả chi tiết cho từng trường trong bảng:
  + Mã sản phẩm (MaSanPham):
Loại: Primary Key (PK)
Giải thích: Đây là khóa chính của bảng, giúp xác định duy nhất từng sản phẩm trong bảng. Mã sản phẩm phải là duy nhất và không được trùng lặp.
Kiểu dữ liệu: INT
NULL: Không
   + Tên sản phẩm (TenSanPham):
Loại: Không khóa
Giải thích: Đây là tên của sản phẩm, mô tả tên gọi cụ thể của mỗi sản phẩm đồ gỗ.
Kiểu dữ liệu: VARCHAR(255)
NULL: Không
    + Loại sản phẩm (LoaiSanPham):
Loại: Foreign Key (FK)
Giải thích: Đây là khóa ngoại, liên kết với bảng khác (ví dụ, bảng LoaiSanPham) để xác định loại sản phẩm. Điều này giúp phân loại sản phẩm theo các loại khác nhau.
Kiểu dữ liệu: INT
NULL: Không
     + Giá bán (GiaBan):
Loại: Không khóa
Giải thích: Đây là giá bán của sản phẩm.
Kiểu dữ liệu: FLOAT
NULL: Không
      + Số lượng tồn kho (SoLuongTon):
Loại: Không khóa
Giải thích: Đây là số lượng sản phẩm còn lại trong kho.
Kiểu dữ liệu: INT
NULL: Không
      + Kích thước (KichThuoc):
Loại: Không khóa.
Giải thích: Đây là kích thước của sản phẩm, có thể là các kích thước cụ thể như chiều dài, chiều rộng, chiều cao, v.v.
Kiểu dữ liệu: VARCHAR(50).
NULL: Không.
      + Chất liệu (ChatLieu):
Loại: Không khóa.
Giải thích: Đây là chất liệu sản xuất ra sản phẩm (gỗ, kim loại, nhựa, v.v.).
Kiểu dữ liệu: VARCHAR(50).
NULL: Không.
    + Màu sắc (MauSac):
         Loại: Không khóa
         Giải thích: Đây là màu sắc của sản phẩm.
         Kiểu dữ liệu: VARCHAR(50).
         NULL: Có.
    [-Bảng Sản Phẩm-] (![image](https://github.com/baolaichi/Quan_Ly_Cua_hang_Noi_That/assets/131328468/9489bed2-8dd6-472f-b926-5328b565668b))
                                                
 -Bảng DonHang
Bảng DonHang chứa thông tin về các đơn hàng.
Các trường trong bảng DonHang:
  + MaDonHang:
Mô tả: Mã đơn hàng, là khóa chính (PK).
Lý do là PK: Mã đơn hàng là duy nhất cho mỗi đơn hàng và dùng để định danh đơn hàng một cách độc nhất.
Kiểu dữ liệu: INT
Ràng buộc: Không được NULL, tự động tăng (AUTO_INCREMENT).
  + NgayDatHang:
Mô tả: Ngày đặt hàng.
Kiểu dữ liệu: DATE
Ràng buộc: Không được NULL.
  + NgayGiaoHang:
Mô tả: Ngày giao hàng.
Kiểu dữ liệu: DATE
Ràng buộc: Có thể NULL (vì có thể ngày giao hàng chưa được xác định khi đơn hàng mới được tạo).
   + TongGiaTri:
Mô tả: Tổng tiền của đơn hàng.
Kiểu dữ liệu: FLOAT
Ràng buộc: Không được NULL.
    + KhachHangID:
Mô tả: Mã khách hàng (foreign key liên kết với bảng KhachHang).
Kiểu dữ liệu: INT
Ràng buộc: Không được NULL
   [-Bảng Đơn hàng-] (![image](https://github.com/baolaichi/Quan_Ly_Cua_hang_Noi_That/assets/131328468/c2c84577-a0e6-476c-b8e8-216975dca1da))

                                       			
 -ChiTietDonHang
   + MaChiTietDonHang:
Mô tả: Mã chi tiết đơn hàng, là khóa chính (PK).
Lý do là PK: Mã chi tiết đơn hàng là duy nhất cho mỗi mục chi tiết và dùng để định danh một cách độc nhất.
Kiểu dữ liệu: INT
Ràng buộc: Không được NULL, tự động tăng (AUTO_INCREMENT).
  + MaDonHang:
Mô tả: Mã đơn hàng, là khóa ngoại (FK) liên kết với bảng DonHang.
Lý do là FK: Dùng để xác định đơn hàng mà mục chi tiết này thuộc về.
Kiểu dữ liệu: INT
Ràng buộc: Không được NULL.
   + MaSanPham:
Mô tả: Mã sản phẩm, là khóa ngoại (FK) liên kết với bảng SanPham.
Lý do là FK: Dùng để xác định sản phẩm nào trong đơn hàng.
Kiểu dữ liệu: INT
Ràng buộc: Không được NULL.
    + SoLuong:
Mô tả: Số lượng sản phẩm.
Kiểu dữ liệu: INT
Ràng buộc: Không được NULL.
     + GiaBan:
Mô tả: Giá bán của sản phẩm.
Kiểu dữ liệu: FLOAT
Ràng buộc: Không được NULL.
   [-Bảng Chi tiết đơn hàng-] (![image](https://github.com/baolaichi/Quan_Ly_Cua_hang_Noi_That/assets/131328468/a005f779-ebfe-4622-9ccc-b6ede794bbef))

     					
-Bảng NhaCungCap
Bảng NhaCungCap chứa thông tin về các nhà cung cấp sản phẩm cho cửa hàng. Dưới đây là mô tả chi tiết cho từng trường trong bảng:
   + MaNhaCungCap
Mô tả: Mã nhà cung cấp, là mã định danh duy nhất cho mỗi nhà cung cấp.
Kiểu dữ liệu: INT
Ràng buộc:
Primary Key (PK): Đây là khóa chính của bảng, vì nó duy nhất xác định từng bản ghi.
Not Null: Không thể để trống, vì mỗi nhà cung cấp phải có một mã duy nhất.
    + TenNhaCungCap
Mô tả: Tên của nhà cung cấp.
Kiểu dữ liệu: VARCHAR(255)
Ràng buộc:
Not Null: Bắt buộc phải nhập, vì cần biết tên của nhà cung cấp.
     + DiaChi
Mô tả: Địa chỉ của nhà cung cấp.
Kiểu dữ liệu: VARCHAR(255)
Ràng buộc:
Có thể để NULL: Không bắt buộc phải nhập, có thể có nhà cung cấp không cần ghi rõ địa chỉ.
     + SoDienThoai
Mô tả: Số điện thoại của nhà cung cấp.
Kiểu dữ liệu: VARCHAR(20)
Ràng buộc:
Not Null: Bắt buộc phải nhập, vì cần số điện thoại để liên hệ với nhà cung cấp.
   [-Bảng Nhà Cung Cấp-] (![image](https://github.com/baolaichi/Quan_Ly_Cua_hang_Noi_That/assets/131328468/440267c5-39c7-44c9-bfab-686e196cada7))

     					


II. Các SP của các chức năng

1. thêm, sửa, xóa Hàng Hóa. có chức năng:
[Thêm đơn hàng: Thêm dữ liệu mới vào DonHang và ChiTietDonHang.]
[Sửa đơn hàng: Cập nhật thông tin trong DonHang và xóa rồi thêm lại các chi tiết đơn hàng.]
[Xóa đơn hàng: Xóa dữ liệu từ cả hai bảng DonHang và ChiTietDonHang.]

 --------------Liệt Kê Tất Cả Hàng Hóa-----------------
 ```sql
 CREATE PROCEDURE LietKeHangHoa
AS
BEGIN
 SELECT * FROM SanPham;
END;
```
 --- Thêm Một Hàng Hóa -------
 ```sql
CREATE PROCEDURE ThemHangHoa
    @TenSanPham NVARCHAR(100),
    @LoaiSanPham NVARCHAR(50),
    @GiaBan DECIMAL(10, 2),
    @SoLuongTon INT,
    @KichThuoc NVARCHAR(50),
    @ChatLieu NVARCHAR(50),
   @MauSac NVARCHAR(30)
AS
BEGIN
   INSERT INTO SanPham (TenSanPham, LoaiSanPham, GiaBan, SoLuongTon, KichThuoc, ChatLieu, MauSac)
  VALUES (@TenSanPham, @LoaiSanPham, @GiaBan, @SoLuongTon, @KichThuoc, @ChatLieu, @MauSac);
END;
```
 ------Xóa Một Hàng Hóa--------------
 ```sql
 CREATE PROCEDURE XoaHangHoa
 @MaSanPham INT
AS
BEGIN
    DELETE FROM SanPham WHERE MaSanPham = @MaSanPham;
END;
```
---------------------Sửa thông tin hàng hóa-------------
```sql
CREATE PROCEDURE SuaThongTinHangHoa
    @MaSanPham INT,
    @TenSanPham NVARCHAR(100),
    @LoaiSanPham NVARCHAR(50),
    @GiaBan DECIMAL(10, 2),
    @SoLuongTon INT,
    @KichThuoc NVARCHAR(50),
    @ChatLieu NVARCHAR(50),
    @MauSac NVARCHAR(30)
AS
BEGIN
    UPDATE SanPham
    SET TenSanPham = @TenSanPham,
        LoaiSanPham = @LoaiSanPham,
        GiaBan = @GiaBan,
        SoLuongTon = @SoLuongTon,
        KichThuoc = @KichThuoc,
        ChatLieu = @ChatLieu,
        MauSac = @MauSac
    WHERE MaSanPham = @MaSanPham;
END;
```
2. Thêm, Sửa, Xóa Hóa Đơn. có các chức năng:
[Thêm một dòng mới vào bảng SanPham với thông tin về tên sản phẩm, giá và số lượng.]
[Cập nhật thông tin của một sản phẩm đã có trong bảng SanPham dựa trên SanPhamID.]
[Xóa một sản phẩm khỏi bảng SanPham dựa trên SanPhamID.]
  --------------Thêm Một Hóa Đơn--------------	 
  ```sql
CREATE PROCEDURE ThemHoaDon
  @NgayDatHang DATE,
    @MaKhachHang INT,
    @TongGiaTri DECIMAL(10, 2),
    @TinhTrangDonHang NVARCHAR(20)
AS
BEGIN
    INSERT INTO DonHang (NgayDatHang, MaKhachHang, TongGiaTri, TinhTrangDonHang)
    VALUES (@NgayDatHang, @MaKhachHang, @TongGiaTri, @TinhTrangDonHang);
END;
```
------------Sửa Một Hóa Đơn-------------------
```sql
CREATE PROCEDURE SuaHoaDon
    @MaDonHang INT,
    @NgayDatHang DATE,
    @MaKhachHang INT,
    @TongGiaTri DECIMAL(10, 2),
    @TinhTrangDonHang NVARCHAR(20)
AS
BEGIN
    UPDATE DonHang
    SET NgayDatHang = @NgayDatHang,
        MaKhachHang = @MaKhachHang,
        TongGiaTri = @TongGiaTri,
        TinhTrangDonHang = @TinhTrangDonHang
    WHERE MaDonHang = @MaDonHang;
END;
```
------------Xóa 1 hóa đơn--------------
```sql
CREATE PROCEDURE XoaHoaDon
    @MaDonHang INT
AS
BEGIN
    DELETE FROM ChiTietDonHang WHERE MaDonHang = @MaDonHang;
    DELETE FROM DonHang WHERE MaDonHang = @MaDonHang;
END;
```
------------Thêm một chi tiết hóa đơn----------------
```sql
CREATE PROCEDURE ThemChiTietHoaDon
    @MaDonHang INT,
    @MaSanPham INT,
    @SoLuong INT,
    @GiaBan DECIMAL(10, 2)
AS
BEGIN
    INSERT INTO ChiTietDonHang (MaDonHang, MaSanPham, SoLuong, GiaBan)
    VALUES (@MaDonHang, @MaSanPham, @SoLuong, @GiaBan);
END;
```
------------Cập Nhật Số Lượng Cho Một Chi Tiết Hóa Đơn----------------
```sql
CREATE PROCEDURE CapNhatSoLuongChiTietHoaDon
    @MaChiTietDonHang INT,
    @SoLuong INT
AS
BEGIN
    UPDATE ChiTietDonHang
    SET SoLuong = @SoLuong
    WHERE MaChiTietDonHang = @MaChiTietDonHang;
END;
```
---------------Xóa Một Dòng Trong Chi Tiết Hóa Đơn-----------
```sql
CREATE PROCEDURE XoaChiTietHoaDon
    @MaChiTietDonHang INT
AS
BEGIN
    DELETE FROM ChiTietDonHang WHERE MaChiTietDonHang = @MaChiTietDonHang;
END;
```

3. Các SP_Báo Cáo
----------Báo Cáo Hàng Tồn------------
[stored procedure có tên là BaoCaoHangTon trong cơ sở dữ liệu hiện tại. Stored procedure này sẽ lấy tên sản phẩm và số lượng tồn của các sản phẩm có số lượng tồn lớn hơn 0 từ bảng SanPham.]
```sql
CREATE PROCEDURE BaoCaoHangTon
AS
BEGIN
    SELECT TenSanPham, SoLuongTon
    FROM SanPham
    WHERE SoLuongTon > 0;
END;
```
------------------Báo Cáo Hàng Bán Nhiều Nhất Trong Tháng---------------------
[stored procedure có tên là BaoCaoHangBanNhieuTrongThang trong cơ sở dữ liệu hiện tại. Stored procedure này lấy tên sản phẩm và tổng số lượng đã bán trong tháng và năm được chỉ định từ bảng ChiTietDonHang, DonHang, và SanPham.]
```sql
CREATE PROCEDURE BaoCaoHangBanNhieuTrongThang
    @Thang INT,
    @Nam INT
AS
BEGIN
    SELECT SP.TenSanPham, SUM(CTDH.SoLuong) AS SoLuongBan
    FROM ChiTietDonHang CTDH
    INNER JOIN DonHang DH ON CTDH.MaDonHang = DH.MaDonHang
    INNER JOIN SanPham SP ON CTDH.MaSanPham = SP.MaSanPham
    WHERE MONTH(DH.NgayDatHang) = @Thang AND YEAR(DH.NgayDatHang) = @Nam
    GROUP BY SP.TenSanPham
    ORDER BY SoLuongBan DESC;
END;
```
----------------Báo Cáo Mặt Hàng Bán Chạy Trong Tháng------------------------
[Stored procedure này lấy tên của mặt hàng bán chạy nhất (có số lượng bán nhiều nhất) trong tháng và năm được chỉ định từ bảng ChiTietDonHang, DonHang, và SanPham.]
```sql
CREATE PROCEDURE BaoCaoMatHangBanChayTrongThang
    @Thang INT,
    @Nam INT
AS
BEGIN
    SELECT TOP 1 SP.TenSanPham, SUM(CTDH.SoLuong) AS SoLuongBan
    FROM ChiTietDonHang CTDH
    INNER JOIN DonHang DH ON CTDH.MaDonHang = DH.MaDonHang
    INNER JOIN SanPham SP ON CTDH.MaSanPham = SP.MaSanPham
    WHERE MONTH(DH.NgayDatHang) = @Thang AND YEAR(DH.NgayDatHang) = @Nam
    GROUP BY SP.TenSanPham
    ORDER BY SoLuongBan DESC;
END;
```
-------------Cập Nhật Số Lượng Tồn Kho Khi Thêm Chi Tiết Hóa Đơn--------------
(Trigger)
```sql
CREATE TRIGGER CapNhatSoLuongTonSauKhiThemChiTiet
ON ChiTietDonHang
AFTER INSERT
AS
BEGIN
    DECLARE @MaSanPham INT, @SoLuong INT;
    SELECT @MaSanPham = inserted.MaSanPham, @SoLuong = inserted.SoLuong
    FROM inserted;
    UPDATE SanPham
    SET SoLuongTon = SoLuongTon - @SoLuong
    WHERE MaSanPham = @MaSanPham;
END;
```
[trigger này đảm bảo rằng mỗi khi có thêm chi tiết đơn hàng mới vào bảng ChiTietDonHang, số lượng tồn của sản phẩm tương ứng trong bảng SanPham sẽ được cập nhật tự động giảm đi số lượng đó. Điều này giúp duy trì tính toàn vẹn dữ liệu và đồng bộ giữa các bảng dữ liệu trong hệ thống của bạn]

---------------Cursor Báo Cáo Hàng Bán Trong Tháng--------------
```sql
CREATE PROCEDURE BaoCaoHangBanTrongThang
    @Thang INT,
    @Nam INT
AS
BEGIN
    DECLARE @TenSanPham NVARCHAR(100), @SoLuongBan INT;
    DECLARE HangBanCursor CURSOR FOR
    SELECT SP.TenSanPham, SUM(CTDH.SoLuong) AS SoLuongBan
    FROM ChiTietDonHang CTDH
    INNER JOIN DonHang DH ON CTDH.MaDonHang = DH.MaDonHang
    INNER JOIN SanPham SP ON CTDH.MaSanPham = SP.MaSanPham
    WHERE MONTH(DH.NgayDatHang) = @Thang AND YEAR(DH.NgayDatHang) = @Nam
    GROUP BY SP.TenSanPham;
    OPEN HangBanCursor;
    FETCH NEXT FROM HangBanCursor INTO @TenSanPham, @SoLuongBan;
    WHILE @@FETCH_STATUS = 0
    BEGIN
        PRINT 'Sản phẩm: ' + @TenSanPham + ' - Số lượng bán: ' + CAST(@SoLuongBan AS NVARCHAR);
        FETCH NEXT FROM HangBanCursor INTO @TenSanPham, @SoLuongBan;
    END;
    CLOSE HangBanCursor;
    DEALLOCATE HangBanCursor;
END;
```
[Stored procedure này giúp bạn tạo ra một báo cáo chi tiết về các sản phẩm đã bán trong một tháng cụ thể. Nó sử dụng con trỏ để lặp qua từng sản phẩm và in ra thông tin chi tiết của sản phẩm và số lượng đã bán. Quá trình này giúp bạn kiểm tra và phân tích dữ liệu bán hàng một cách tổng quát và chi tiết.]

4. Function để tính tổng số lượng sản phẩm trong một đơn hàng dựa trên mã đơn hàng.
[Function FN_TongSoLuongSanPhamTrongDonHang này có thể được sử dụng trong các stored procedure (SP_) để lấy tổng số lượng sản phẩm trong một đơn hàng, giúp cho việc tính toán và xử lý dữ liệu trở nên thuận tiện hơn.]
```sql
  CREATE FUNCTION FN_TongSoLuongSanPhamTrongDonHang
(
    @MaDonHang INT
)
RETURNS INT
AS
BEGIN
    DECLARE @TongSoLuong INT;
    SELECT @TongSoLuong = SUM(SoLuong)
    FROM ChiTietDonHang
    WHERE MaDonHang = @MaDonHang;
    RETURN ISNULL(@TongSoLuong, 0);
END;
```
[-Hình Kết quả khi chạy Function-] (![image](https://github.com/baolaichi/Quan_Ly_Cua_hang_Noi_That/assets/131328468/140ed078-e7ea-488e-87ea-72a26a0a236e))
                                  



