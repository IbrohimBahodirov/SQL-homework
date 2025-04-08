--EASY
BULK INSERT Products
FROM 'C:\Data\products.txt'
WITH (
    FIELDTERMINATOR = ',',
    ROWTERMINATOR = '\n',
    FIRSTROW = 2
);

CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(50),
    Price DECIMAL(10,2)
);

INSERT INTO Products (ProductID, ProductName, Price)
VALUES 
(1, 'Mouse', 15.99),
(2, 'Keyboard', 29.99),
(3, 'Monitor', 199.99);

INSERT INTO Products (ProductID, ProductName, Price)
VALUES (4, 'USB Hub', NULL);  

ALTER TABLE Products
ADD Stock INT NOT NULL;  

ALTER TABLE Products
ADD CONSTRAINT UQ_ProductName UNIQUE (ProductName);


INSERT INTO Products (ProductID, ProductName, Price)
VALUES (5, 'Headphones', 49.99);

CREATE TABLE Categories (
    CategoryID INT PRIMARY KEY,
    CategoryName VARCHAR(50) UNIQUE
);

CREATE TABLE Orders (
    OrderID INT IDENTITY(1,1) PRIMARY KEY,
    OrderDate DATE
);

--MIDDLE


BULK INSERT Products
FROM 'C:\Data\products_data.txt'
WITH (
    FIELDTERMINATOR = ',',    
    ROWTERMINATOR = '\n',     
    FIRSTROW = 2              
);


ALTER TABLE Products
ADD CategoryID INT;


ALTER TABLE Products
ADD CONSTRAINT FK_Products_Categories
FOREIGN KEY (CategoryID) REFERENCES Categories(CategoryID);


ALTER TABLE Products
ADD CONSTRAINT CHK_Price_Positive CHECK (Price > 0);


ALTER TABLE Products
ADD Stock INT NOT NULL DEFAULT 0;


SELECT 
    ProductID, 
    ProductName, 
    ISNULL(Price, 0) AS Price
FROM Products;


CREATE TABLE ExampleKeys (
    ID INT PRIMARY KEY,               
    Email VARCHAR(100) UNIQUE         
);


--HARD


CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    FullName VARCHAR(100),
    Age INT,
    CONSTRAINT CHK_Age_Adult CHECK (Age >= 18)
);


CREATE TABLE InvoiceNumbers (
    InvoiceID INT IDENTITY(100, 10) PRIMARY KEY,
    InvoiceDate DATE
);


CREATE TABLE OrderDetails (
    OrderID INT,
    ProductID INT,
    Quantity INT,
    PRIMARY KEY (OrderID, ProductID)  
);


SELECT 
    COALESCE(NULL, NULL, 'Default Value') AS FirstNonNull,  
    ISNULL(NULL, 'Fallback') AS ReplacedValue               
;


CREATE TABLE Employees (
    EmpID INT PRIMARY KEY,
    FullName VARCHAR(100),
    Email VARCHAR(100) UNIQUE
);


CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    CONSTRAINT FK_Orders_Customers
    FOREIGN KEY (CustomerID)
    REFERENCES Customers(CustomerID)
    ON DELETE CASCADE
    ON UPDATE CASCADE
);
