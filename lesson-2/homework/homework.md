-- 1. Create Employees table
CREATE TABLE Employees (
    EmpID INT,
    Name VARCHAR(50),
    Salary DECIMAL(10, 2)
);

-- 2. Insert three records (single-row and multiple-row)
INSERT INTO Employees (EmpID, Name, Salary) VALUES (1, 'Alice', 5000.00);
INSERT INTO Employees (EmpID, Name, Salary) 
VALUES 
    (2, 'Bob', 6000.00),
    (3, 'Charlie', 5500.00);

-- 3. Update Salary where EmpID = 1
UPDATE Employees SET Salary = 5200.00 WHERE EmpID = 1;

-- 4. Delete record where EmpID = 2
DELETE FROM Employees WHERE EmpID = 2;

-- 5. DELETE vs TRUNCATE vs DROP
-- Create a test table
CREATE TABLE TestTable (ID INT, Name VARCHAR(50));
INSERT INTO TestTable VALUES (1, 'Test'), (2, 'Sample');

-- DELETE
DELETE FROM TestTable WHERE ID = 1;

-- TRUNCATE
TRUNCATE TABLE TestTable;

-- DROP
DROP TABLE TestTable;

-- 6. Modify Name to VARCHAR(100)
ALTER TABLE Employees ALTER COLUMN Name VARCHAR(100);

-- 7. Add Department column
ALTER TABLE Employees ADD Department VARCHAR(50);

-- 8. Change Salary type to FLOAT
ALTER TABLE Employees ALTER COLUMN Salary FLOAT;

-- 9. Create Departments table
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(50)
);

-- 10. Remove all records from Employees (but keep structure)
DELETE FROM Employees;

-- Assuming another table like ExistingDepartments with similar structure
-- 1. Insert into Departments using SELECT
INSERT INTO Departments (DepartmentID, DepartmentName)
SELECT DeptID, DeptName FROM ExistingDepartments;

-- 2. Update employees with Salary > 5000
UPDATE Employees SET Department = 'Management' WHERE Salary > 5000;

-- 3. Remove all employees but keep structure
DELETE FROM Employees;

-- 4. Drop Department column
ALTER TABLE Employees DROP COLUMN Department;

-- 5. Rename Employees to StaffMembers
EXEC sp_rename 'Employees', 'StaffMembers';

-- 6. Drop Departments table
DROP TABLE Departments;

-- 1. Create Products table
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100),
    Category VARCHAR(50),
    Price DECIMAL(10, 2),
    CreatedAt DATETIME
);

-- 2. Add CHECK constraint to Price
ALTER TABLE Products 
ADD CONSTRAINT chk_price_positive CHECK (Price > 0);

-- 3. Add StockQuantity with DEFAULT 50
ALTER TABLE Products 
ADD StockQuantity INT DEFAULT 50;

-- 4. Rename Category to ProductCategory
EXEC sp_rename 'Products.Category', 'ProductCategory', 'COLUMN';

-- 5. Insert 5 records
INSERT INTO Products (ProductID, ProductName, ProductCategory, Price, CreatedAt)
VALUES 
    (1, 'Laptop', 'Electronics', 1000.00, GETDATE()),
    (2, 'Phone', 'Electronics', 600.00, GETDATE()),
    (3, 'Desk', 'Furniture', 150.00, GETDATE()),
    (4, 'Chair', 'Furniture', 100.00, GETDATE()),
    (5, 'Pen', 'Stationery', 2.50, GETDATE());

-- 6. SELECT INTO backup
SELECT * INTO Products_Backup FROM Products;

-- 7. Rename Products to Inventory
EXEC sp_rename 'Products', 'Inventory';

-- 8. Change Price to FLOAT
ALTER TABLE Inventory ALTER COLUMN Price FLOAT;

-- 9. Add IDENTITY column (Note: You can't add IDENTITY directly; need a workaround)
-- Create new table with IDENTITY
CREATE TABLE Inventory_New (
    ProductCode INT IDENTITY(1000, 5),
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100),
    ProductCategory VARCHAR(50),
    Price FLOAT,
    CreatedAt DATETIME,
    StockQuantity INT DEFAULT 50
);

-- Copy data
INSERT INTO Inventory_New (ProductID, ProductName, ProductCategory, Price, CreatedAt, StockQuantity)
SELECT ProductID, ProductName, ProductCategory, Price, CreatedAt, StockQuantity FROM Inventory;

-- Drop old table and rename
DROP TABLE Inventory;
EXEC sp_rename 'Inventory_New', 'Inventory';
