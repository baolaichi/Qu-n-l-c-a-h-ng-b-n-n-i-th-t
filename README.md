# Quản lý cửa hàng bán đồ nội thất
BTL: Mon HQT- CSDL
-- tạo DataBase tên Quan_BH_Cua_hang_do_go
nhấp chuột phải vào dataBase: Chọn new Database
-- tạo các bảng cho Database
    - bảng Customers: CustomerID (primary Key), FullName, PhoneNumber, Email, Address.
    - bảng OderDetails: OrderDetailID (primary Key), OrderID, ProductID, Quantity, Price.
    - bảng Orders: OrderID (primary Key), CustomerID, OrderDate, TotalAmount.
    - bảng Product: ProductID, ProductName, Description, Price, Stock, CostPrice.
-- 
