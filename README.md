# Quan Ly Cua hang do go noi that
BTL: Mon HQT- CSDL
///////////////////////////
Họ và tên: Lại Chí Bảo   //
Lớp: K57KMT.01           //
MSSV: K215520216829      //
///////////////////////////


- Tạo Database: Quan_BH_Cua_hang_do_go
  - Customer(CustomerID[primary], FullName, PhoneNumber, Email, Address)
  - OderDetails(OrderDetailID[primary], OrderID, ProductID, Quantity, Price)
  - Order(OrderID[primary], CustomerID, OrderDate, TotalAmount)
  - Products(ProductID[primary], ProductName, Description, Price, Stock, CostPrice)
 
     Thêm dữ liệu mẫu vào bảng Customers
     Thêm dữ liệu mẫu vào bảng Products
     Thêm dữ liệu mẫu vào bảng Orders
     Thêm dữ liệu mẫu vào bảng OrderDetails

  ![image](https://github.com/baolaichi/Quan_Ly_Cua_hang_Noi_That/assets/131328468/52013722-b5a8-4257-aa9f-19b3843cc376)
- Tạo GridView: SoLuongHangBan
  ![image](https://github.com/baolaichi/Quan_Ly_Cua_hang_Noi_That/assets/131328468/b8e410c9-392b-4b38-8f2a-caaee172d039)

- Tạo trigger
CREATE TRIGGER trg_CheckPriceBeforeInsert
ON OrderDetails
FOR INSERT, UPDATE
AS
BEGIN
    DECLARE @ProductID INT, @Price DECIMAL(18, 2), @CostPrice DECIMAL(18, 2);
    
    SELECT @ProductID = i.ProductID, @Price = i.Price
    FROM inserted i;
    
    SELECT @CostPrice = p.CostPrice
    FROM Products p
    WHERE p.ProductID = @ProductID;
    
    IF @Price < @CostPrice
    BEGIN
        ROLLBACK TRANSACTION;
        RAISERROR('Giá bán thấp hơn giá nhập, vui lòng kiểm tra lại.', 16, 1);
    END
END;
-- Thêm dữ liệu mẫu vào bảng OrderDetails
-- để kiểm tra tigger 
-- Giá bán cao hơn giá nhập (1500000)
INSERT INTO OrderDetails (OrderID, ProductID, Quantity, Price)
VALUES (1, 1, 1, 2000000);

-- Thêm dữ liệu mẫu vào bảng OrderDetails
-- Giá bán thấp hơn giá nhập (1500000)
INSERT INTO OrderDetails (OrderID, ProductID, Quantity, Price)
VALUES (1, 1, 1, 1400000);

-- thủ tục tính toán số lỗ là bao nhiêu
CREATE PROCEDURE CalculateLosses
AS
BEGIN
    -- Tạo bảng tạm để lưu kết quả
    CREATE TABLE #Losses (
        OrderID INT,
        ProductID INT,
        ProductName NVARCHAR(100),
        Quantity INT,
        SellingPrice DECIMAL(18, 2),
		CostPrice DECIMAL(18, 2),
        Loss DECIMAL(18, 2)
    );

    DECLARE @OrderID INT, @ProductID INT, @Quantity INT, @SellingPrice DECIMAL(18, 2), @CostPrice DECIMAL(18, 2), @ProductName NVARCHAR(100), @Loss DECIMAL(18, 2);
    
    -- Khai báo cursor để duyệt qua các đơn hàng
    DECLARE order_cursor CURSOR FOR
    SELECT od.OrderID, od.ProductID, od.Quantity, od.Price AS SellingPrice, p.CostPrice, p.ProductName
    FROM OrderDetails od
    JOIN Products p ON od.ProductID = p.ProductID;
    
    OPEN order_cursor;
    
    FETCH NEXT FROM order_cursor INTO @OrderID, @ProductID, @Quantity, @SellingPrice, @CostPrice, @ProductName;
    
    WHILE @@FETCH_STATUS = 0
    BEGIN
        IF @SellingPrice < @CostPrice
        BEGIN
            SET @Loss = (@CostPrice - @SellingPrice) * @Quantity;
	    
            -- Chèn kết quả vào bảng tạm
            INSERT INTO #Losses (OrderID, ProductID, ProductName, Quantity, SellingPrice, CostPrice, Loss)
            VALUES (@OrderID, @ProductID, @ProductName, @Quantity, @SellingPrice, @CostPrice, @Loss);
        END
        
        FETCH NEXT FROM order_cursor INTO @OrderID, @ProductID, @Quantity, @SellingPrice, @CostPrice, @ProductName;
    END
    
    CLOSE order_cursor;
    DEALLOCATE order_cursor;
    

    -- Truy vấn bảng tạm để hiển thị kết quả
    SELECT * FROM #Losses;

    -- Xóa bảng tạm
    DROP TABLE #Losses;
END;

-- chạy thủ tục
EXEC CalculateLosses;

  
  


