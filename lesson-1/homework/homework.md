create database SchoolDB;
use SchoolDB;

create table Students(
    id INT PRIMARY KEY ,
    name VARCHAR(50),
    age TINYINT
);

SELECT Top 10 percent [EmployeeKey]
      ,[FirstName]
      ,[LastName]
      ,[MiddleName]
      ,[VacationHours]
       ,[SalesPersonFlag]
      ,[DepartmentName]
    FROM [AdventureWorksDW2019].[dbo].[DimEmployee]
  order by VacationHours desc


  select [FirstName],[LastName],EmployeeKey from [AdventureWorksDW2019].[dbo].[DimEmployee]
  order by EmployeeKey
offset 10 row fetch next 10 row only


select distinct DepartmentName from  [AdventureWorksDW2019].[dbo].[DimEmployee]

create table student ( fname varchar(60),mname varchar(50),lname varchar(50))

insert into student values ('Joe','doe','Smith'),(null,'doe','Smith'),(null,null,'Smith'),(null,null,null)


select isnull(fname,'Hello')  from student
select * from student
select coalesce(fname,mname,lname) from student

select * from [AdventureWorksDW2019].[dbo].[DimEmployee]
where   ( DepartmentName = 'marketing'   or DepartmentName = 'Production') and VacationHours > 30




select * from [AdventureWorksDW2019].[dbo].[DimEmployee]
where    DepartmentName not in ('Production','marketing','Finance') and MaritalStatus != 'S'



use f25_lesson04


--SQL -- 

--- MS SQL -- SQL SERVER
--- PL SQL -- Oracle --
---PostgreSQL --- 
--- MY SQL -- 
--- MangoDB -- Nosql 



--- server --

---SSMS -- PgAdmin,Azure Data Studio, SQLite




----- Char, Varchar


-----
--VarChar -- variable char -- varchar(100)
--char --- fixed -- char(100) --- 

---nchar --- natitioanl char -- 
---nvarchar -- 

create schema lesson4

create table lesson4.employee (EmpId int, EmpName varchar(50),Salary decimal(10,2))


insert into lesson4.employee values (1,'John',2000)


insert into lesson4.employee (EmpId,EmpName) values (1,'John'),(2,'Alex')

insert into lesson4.employee
select 1,'Sara',1000
union all
select 1,'Sara',1000

select * from lesson4.employee


select * into employee3 from lesson4.employee
where 1=2

select * from employee3

--- primary key, foreign key, check, default, not null, unique


select * from customer

truncate table customer

select * from lesson4.employee


delete lesson4.employee


bulk insert customer
from 'C:\Users\Maab LLC\Desktop\maab_files\F25\F25_SQL\lesson04\Customer.txt'
with
(
firstrow=2,
fieldterminator=',',
rowterminator='\n'
)
