# Quan Ly Cua hang do go noi that
BTL: Mon HQT- CSDL
--Thông Tin Cá nhân--
- Họ và tên: Lại Chí Bảo   
- Lớp: K57KMT.01           
- MSSV: K215520216829
      
I, Mô tả hệ thống (Quản lý thông tin cửa hàng nội thất)
-1, Các chức năng
	Bài toán xây dựng CSDL để quản lý cửa hàng gỗ
 - Quản lý hàng hóa: Thêm loại hàng mới, sửa hàng hóa, xóa 1 mặt hàng, liệt kê danh sách các mặt hàng tại cửa hàng.
 - Quản lý hóa đơn bán: Thêm 1 hóa đơn, xóa 1 hóa đơn, Sửa thông tin của hóa đơn
-2, Báo cáo
 - Báo hàng bị bán với giá thấp so với giá nhập
 - Báo cáo số lượng hàng hóa khi có đơn hàng mới
 - Tổng doanh thu của cửa hàng trong một tháng
-3, Các bảng của hệ thống được lập
 - KhachHang:
   + KhachHangID là khóa chính để xác định duy nhất mỗi khách hàng.
   + TenKhachHang và SoDienThoai là bắt buộc vì đây là thông tin cơ bản và quan trọng của khách hàng.
   + DiaChi và Email là tùy chọn vì không phải lúc nào cũng cần thiết phải nhập thông tin này.
   + 
     ![image](https://github.com/baolaichi/Quan_Ly_Cua_hang_Noi_That/assets/131328468/2103f36f-fef6-4041-a5fd-99fda784c2b8)
                            -Bảng Khách hàng-
 - SanPham
   + SanPhamID là khóa chính để xác định duy nhất mỗi sản phẩm.
   + TenSanPham, GiaGoc và SoLuongTonKho là bắt buộc vì đây là thông tin cơ bản và quan trọng của sản phẩm.
   + 
		![image](https://github.com/baolaichi/Quan_Ly_Cua_hang_Noi_That/assets/131328468/c3d41df5-0429-4218-bcd8-d7b2ffaa4429)
                                                -Bảng Sản Phẩm-
 - DonHang
   + DonHangID là khóa chính để xác định duy nhất mỗi đơn hàng.
   + KhachHangID là khóa ngoại để xác định khách hàng đặt hàng.
   + NgayDatHang là bắt buộc vì cần biết ngày nào đơn hàng được tạo.
   + TongTien được tính tự động dựa trên chi tiết đơn hàng.
                ![image](https://github.com/baolaichi/Quan_Ly_Cua_hang_Noi_That/assets/131328468/5be8df01-91ed-431d-9398-b3f9bb5ecd1d)
                                    -Bảng Đơn hàng-

     			
 -ChiTietDonHang
   + ChiTietID là khóa chính để xác định duy nhất mỗi chi tiết đơn hàng.
   + DonHangID là khóa ngoại để xác định đơn hàng chứa chi tiết này.
   + SanPhamID là khóa ngoại để xác định sản phẩm trong chi tiết đơn hàng.
   + SoLuong và GiaBan là bắt buộc vì cần biết thông tin chi tiết của sản phẩm trong đơn hàng.
                  ![image](https://github.com/baolaichi/Quan_Ly_Cua_hang_Noi_That/assets/131328468/7abf7f72-5e1a-4f1e-a2d9-e8a595aa2e9b)
     					-Bảng Chi tiết đơn hàng-

-II, Các SP của các chức năng
-1, thêm, sửa, xóa đơn hàng. có chức năng:
	[Thêm đơn hàng: Thêm dữ liệu mới vào DonHang và ChiTietDonHang.
	Sửa đơn hàng: Cập nhật thông tin trong DonHang và xóa rồi thêm lại các chi tiết đơn hàng.
	Xóa đơn hàng: Xóa dữ liệu từ cả hai bảng DonHang và ChiTietDonHang.]
 
CREATE PROCEDURE sp_DonHang
    @action NVARCHAR(10),
    @DonHangID INT = NULL,
    @KhachHangID INT = NULL,
    @NgayDatHang DATE = NULL,
    @ChiTiet ChiTietDonHangType READONLY = NULL
AS
BEGIN
    IF @action = 'INSERT'
    BEGIN
        DECLARE @TongTien DECIMAL(18, 2);
        SET @TongTien = 0;
  	-- Tạo đơn hàng mới
        INSERT INTO DonHang (KhachHangID, NgayDatHang, TongTien)
        VALUES (@KhachHangID, @NgayDatHang, @TongTien);
  	-- Lấy ID của đơn hàng vừa tạo
        SET @DonHangID = SCOPE_IDENTITY();
  	-- Thêm chi tiết đơn hàng và tính tổng tiền
        DECLARE @SanPhamID INT, @SoLuong INT, @GiaBan DECIMAL(18, 2);
        DECLARE cur CURSOR FOR
        SELECT SanPhamID, SoLuong, GiaBan FROM @ChiTiet;
        OPEN cur;
        FETCH NEXT FROM cur INTO @SanPhamID, @SoLuong, @GiaBan;
        WHILE @@FETCH_STATUS = 0
        BEGIN
            INSERT INTO ChiTietDonHang (DonHangID, SanPhamID, SoLuong, GiaBan)
            VALUES (@DonHangID, @SanPhamID, @SoLuong, @GiaBan);
            SET @TongTien = @TongTien + (@GiaBan * @SoLuong);
            FETCH NEXT FROM cur INTO @SanPhamID, @SoLuong, @GiaBan;
        END;
        CLOSE cur;
        DEALLOCATE cur;
 	-- Cập nhật tổng tiền của đơn hàng
        UPDATE DonHang
        SET TongTien = @TongTien
        WHERE DonHangID = @DonHangID;
	 SELECT @DonHangID AS DonHangID;
    END
    ELSE IF @action = 'UPDATE'
    BEGIN
        DECLARE @TongTien DECIMAL(18, 2);
        SET @TongTien = 0;
  	-- Cập nhật thông tin đơn hàng
        UPDATE DonHang
        SET KhachHangID = @KhachHangID, NgayDatHang = @NgayDatHang
        WHERE DonHangID = @DonHangID;
  	-- Xóa chi tiết đơn hàng cũ
        DELETE FROM ChiTietDonHang
        WHERE DonHangID = @DonHangID;
   	-- Thêm chi tiết đơn hàng mới và tính tổng tiền
        DECLARE @SanPhamID INT, @SoLuong INT, @GiaBan DECIMAL(18, 2);
        DECLARE cur CURSOR FOR
        SELECT SanPhamID, SoLuong, GiaBan FROM @ChiTiet;
        OPEN cur;
        FETCH NEXT FROM cur INTO @SanPhamID, @SoLuong, @GiaBan;
        WHILE @@FETCH_STATUS = 0
        BEGIN
            INSERT INTO ChiTietDonHang (DonHangID, SanPhamID, SoLuong, GiaBan)
            VALUES (@DonHangID, @SanPhamID, @SoLuong, @GiaBan);
            SET @TongTien = @TongTien + (@GiaBan * @SoLuong);
            FETCH NEXT FROM cur INTO @SanPhamID, @SoLuong, @GiaBan;
        END;
        CLOSE cur;
        DEALLOCATE cur;
 	 -- Cập nhật tổng tiền của đơn hàng
        UPDATE DonHang
        SET TongTien = @TongTien
        WHERE DonHangID = @DonHangID;
    END
    ELSE IF @action = 'DELETE'
    BEGIN
  	-- Xóa chi tiết đơn hàng trước
        DELETE FROM ChiTietDonHang
        WHERE DonHangID = @DonHangID;
  	-- Xóa đơn hàng
        DELETE FROM DonHang
        WHERE DonHangID = @DonHangID;
    END
    ELSE IF @action = 'REPORT'
    BEGIN
        SELECT * FROM DonHang;
    END
END;


-2, Thêm, Sửa, Xóa sản phẩm. có các chức năng:
	[Thêm một dòng mới vào bảng SanPham với thông tin về tên sản phẩm, giá và số lượng.
	 Cập nhật thông tin của một sản phẩm đã có trong bảng SanPham dựa trên SanPhamID.
	 Xóa một sản phẩm khỏi bảng SanPham dựa trên SanPhamID.]
     	 
CREATE PROCEDURE sp_SanPham
    @action NVARCHAR(10),
    @SanPhamID INT = NULL,
    @TenSanPham NVARCHAR(100) = NULL,
    @Gia DECIMAL(18, 2) = NULL,
    @SoLuong INT = NULL
AS
BEGIN
    IF @action = 'INSERT'
    BEGIN
        INSERT INTO SanPham (TenSanPham, Gia, SoLuong)
        VALUES (@TenSanPham, @Gia, @SoLuong);
    END
    ELSE IF @action = 'UPDATE'
    BEGIN
        UPDATE SanPham
        SET TenSanPham = @TenSanPham,
            Gia = @Gia,
            SoLuong = @SoLuong
        WHERE SanPhamID = @SanPhamID;
    END
    ELSE IF @action = 'DELETE'
    BEGIN
        DELETE FROM SanPham
        WHERE SanPhamID = @SanPhamID;
    END
    ELSE IF @action = 'REPORT'
    BEGIN
        SELECT * FROM SanPham;
    END
END;
GO

-3, Trigger để cập nhật số lượng sản phẩm khi có đơn hàng mới(nó sẽ báo cáo cho ta lại xem còn số lượng đơn hàng khi nhận được một đơn mua mơi)

[Trigger trg_UpdateSanPhamSoLuong
Mục đích: Cập nhật số lượng sản phẩm trong bảng SanPham khi có đơn hàng mới được thêm vào.
Loại trigger: AFTER INSERT ON ChiTietDonHang
Cách hoạt động:
	Trigger này được kích hoạt sau khi một bản ghi được chèn vào bảng ChiTietDonHang.
	Khi một đơn hàng mới được thêm vào (được lưu trong DonHang và chi tiết đơn hàng trong ChiTietDonHang), số lượng các sản phẩm liên quan được giảm đi theo số lượng được bán 	trong chi tiết đơn hàng.
Cụ thể, trigger này thực hiện các bước sau:
	Lấy SanPhamID và SoLuong từ bảng inserted (là bảng ảo chứa các hàng đã chèn vào ChiTietDonHang).
	Cập nhật số lượng của sản phẩm tương ứng trong bảng SanPham bằng cách trừ đi SoLuong đã bán.
	Dữ liệu inserted cung cấp thông tin về sản phẩm đã bán, trigger sẽ cập nhật số lượng trong bảng SanPham một cách tự động mỗi khi có đơn hàng mới được thêm vào.]
 
CREATE TRIGGER trg_UpdateSanPhamSoLuong
ON ChiTietDonHang
AFTER INSERT
AS
BEGIN
    DECLARE @SanPhamID INT, @SoLuong INT;
    SELECT @SanPhamID = i.SanPhamID, @SoLuong = i.SoLuong
    FROM inserted i;
    UPDATE SanPham
    SET SoLuong = SoLuong - @SoLuong
    WHERE SanPhamID = @SanPhamID;
END;
GO

-4, Trigger để kiểm tra giá bán xem có thấp hơn giá gốc không(Báo cáo cho người dùng khi nhập vào giá bán thấp hơn giá nhập)

[Mục đích: Kiểm tra và báo lỗi nếu giá bán của sản phẩm trong đơn hàng mới thêm vào thấp hơn giá gốc của sản phẩm.
Loại trigger: INSTEAD OF INSERT ON ChiTietDonHang
Cách hoạt động:
   Trigger này được kích hoạt thay thế thao tác chèn vào bảng ChiTietDonHang nếu điều kiện kiểm tra không được đáp ứng.
   Khi một đơn hàng mới được thêm vào (ChiTietDonHang), trigger này kiểm tra từng sản phẩm trong đơn hàng:
	Lấy SanPhamID và GiaBan từ inserted (bảng ảo chứa các hàng được chèn vào ChiTietDonHang).
	Kiểm tra xem giá bán (GiaBan) của sản phẩm có nhỏ hơn giá gốc (GiaGoc) hay không trong bảng SanPham.
	Nếu giá bán nhỏ hơn giá gốc, trigger sẽ gửi một lỗi (RAISERROR) và quay lại giao dịch (ROLLBACK), ngăn không cho đơn hàng được thêm vào.
	Nếu không có lỗi, trigger chuyển tiếp dữ liệu từ inserted vào bảng ChiTietDonHang, cho phép thực hiện việc chèn dữ liệu một cách bình thường.]

CREATE TRIGGER trg_KiemTraGiaBan
ON ChiTietDonHang
INSTEAD OF INSERT
AS
BEGIN
    DECLARE @SanPhamID INT, @GiaBan DECIMAL(18, 2);
  -- Lặp qua các bản ghi trong bảng inserted
    DECLARE insert_cursor CURSOR FOR
    SELECT SanPhamID, GiaBan
    FROM inserted;
    OPEN insert_cursor;
    FETCH NEXT FROM insert_cursor INTO @SanPhamID, @GiaBan;
    WHILE @@FETCH_STATUS = 0
    BEGIN
  -- Kiểm tra giá bán với giá gốc
        IF EXISTS (
            SELECT 1
            FROM SanPham
            WHERE SanPhamID = @SanPhamID AND @GiaBan < GiaGoc
        )
        BEGIN
   -- Giá bán thấp hơn giá gốc, báo lỗi và rollback giao dịch
            RAISERROR('Giá bán thấp hơn giá gốc!', 16, 1);
            ROLLBACK TRANSACTION;
            RETURN;
        END
        FETCH NEXT FROM insert_cursor INTO @SanPhamID, @GiaBan;
    END;
    CLOSE insert_cursor;
    DEALLOCATE insert_cursor;
   -- Nếu không có lỗi, chèn dữ liệu vào bảng ChiTietDonHang
    INSERT INTO ChiTietDonHang (DonHangID, SanPhamID, SoLuong, GiaBan)
    SELECT DonHangID, SanPhamID, SoLuong, GiaBan
    FROM inserted;
END;
GO

-- [Các trigger giúp đảm bảo tính toàn vẹn dữ liệu và thực hiện các hành động tự động khi có sự thay đổi trong các bảng liên quan, như thêm đơn hàng, kiểm tra giá bán, và cập nhật số lượng sản phẩm bán ra.]


-5, Cursor để tính tổng tiền các mặt hàng được bán trong tháng.(Báo cáo cho ta xem số doanh thu của tháng là bao nhiêu)
	[CURSOR để lặp qua từng dòng kết quả trả về từ các truy vấn hoặc từ bảng biến bảng (table variable)
	 CURSOR được sử dụng để duyệt qua từng dòng kết quả hoặc từng phần tử trong bảng biến để thực hiện các thao tác xử lý dữ liệu như tính tổng tiền, thêm chi tiết đơn hàng, 	và cập nhật thông tin đơn hàng.]

CREATE PROCEDURE sp_TinhTongTienTheoThang @Thang INT, @Nam INT
AS
BEGIN
    DECLARE @TongTien DECIMAL(18, 2);
    SET @TongTien = 0.0;
    DECLARE cur CURSOR FOR
    SELECT ct.GiaBan * ct.SoLuong
    FROM ChiTietDonHang ct
    JOIN DonHang dh ON ct.DonHangID = dh.DonHangID
    WHERE MONTH(dh.NgayDatHang) = @Thang AND YEAR(dh.NgayDatHang) = @Nam;
    OPEN cur;
    FETCH NEXT FROM cur INTO @TongTien;
    WHILE @@FETCH_STATUS = 0
    BEGIN
        SET @TongTien = @TongTien + @TongTien;
        FETCH NEXT FROM cur INTO @TongTien;
    END;
    CLOSE cur;
    DEALLOCATE cur;
    SELECT @TongTien AS TongTienBanHang;
END;
GO


  


