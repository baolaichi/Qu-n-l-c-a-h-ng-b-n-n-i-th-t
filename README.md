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


 
  


