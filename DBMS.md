# Practical SQL Task

This file defines all SQL tables extracted from the provided document, along with realistic `CREATE TABLE` and `INSERT INTO` statements.

---

## 1️⃣ Table: Region_Sales

```sql
CREATE TABLE Region_Sales (
    Region VARCHAR(50),
    Product VARCHAR(50),
    Sales_Amount INT,
    Year INT
);

INSERT INTO Region_Sales (Region, Product, Sales_Amount, Year) VALUES
('North America', 'Watch', 1500, 2023),
('Europe', 'Mobile', 1200, 2023),
('Asia', 'Watch', 1800, 2023),
('North America', 'TV', 900, 2024),
('Europe', 'Watch', 2000, 2024),
('Asia', 'Mobile', 1000, 2024),
('North America', 'Mobile', 1600, 2023),
('Europe', 'TV', 1500, 2023),
('Asia', 'TV', 1100, 2024),
('North America', 'Watch', 1700, 2024);
```
---
```
CREATE TABLE STU_INFO (
    Rno INT PRIMARY KEY,
    Name VARCHAR(50),
    Branch VARCHAR(10)
);

INSERT INTO STU_INFO (Rno, Name, Branch) VALUES
(101, 'Raju', 'CE'),
(102, 'Amit', 'CE'),
(103, 'Sanjay', 'ME'),
(104, 'Neha', 'EC'),
(105, 'Meera', 'EE'),
(106, 'Mahesh', 'ME');

```
---
```
CREATE TABLE RESULT (
    Rno INT,
    SPI DECIMAL(3,1),
    FOREIGN KEY (Rno) REFERENCES STU_INFO(Rno)
);

INSERT INTO RESULT (Rno, SPI) VALUES
(101, 8.8),
(102, 9.2),
(103, 7.6),
(104, 8.2),
(105, 7.0),
(107, 8.9);
```
---
```
CREATE TABLE EMPLOYEE_MASTER (
    EmployeeNo VARCHAR(10) PRIMARY KEY,
    Name VARCHAR(50),
    ManagerNo VARCHAR(10) NULL
);

INSERT INTO EMPLOYEE_MASTER (EmployeeNo, Name, ManagerNo) VALUES
('E01', 'Tarun', NULL),
('E02', 'Rohan', 'E02'),
('E03', 'Priya', 'E01'),
('E04', 'Milan', 'E03'),
('E05', 'Jay', 'E01'),
('E06', 'Anjana', 'E04');

```
---
```
CREATE TABLE Person_v1 (
    PersonID INT PRIMARY KEY,
    PersonName VARCHAR(100),
    DepartmentID INT NULL,
    Salary INT,
    JoiningDate DATE,
    City VARCHAR(50)
);

INSERT INTO Person_v1 (PersonID, PersonName, DepartmentID, Salary, JoiningDate, City) VALUES
(101, 'Rahul Tripathi', 2, 56000, '2000-01-01', 'Rajkot'),
(102, 'Hardik Pandya', 3, 18000, '2001-09-25', 'Ahmedabad'),
(103, 'Bhavin Kanani', 4, 25000, '2000-05-14', 'Baroda'),
(104, 'Bhoomi Vaishnav', 1, 39000, '2005-02-08', 'Rajkot'),
(105, 'Rohit Topiya', 2, 17000, '2001-07-23', 'Jamnagar'),
(106, 'Priya Menpara', NULL, 9000, '2000-10-18', 'Ahmedabad'),
(107, 'Neha Sharma', 2, 34000, '2002-12-25', 'Rajkot'),
(108, 'Nayan Goswami', 3, 25000, '2001-07-01', 'Rajkot'),
(109, 'Mehul Bhundiya', 4, 13500, '2005-01-09', 'Baroda'),
(110, 'Mohit Maru', 5, 14000, '2000-05-25', 'Jamnagar');
```
---
```
CREATE TABLE Department_v1 (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(50),
    DepartmentCode VARCHAR(10),
    Location VARCHAR(50)
);

INSERT INTO Department_v1 (DepartmentID, DepartmentName, DepartmentCode, Location) VALUES
(1, 'Admin', 'Adm', 'A-Block'),
(2, 'Computer', 'CE', 'C-Block'),
(3, 'Civil', 'CI', 'G-Block'),
(4, 'Electrical', 'EE', 'E-Block'),
(5, 'Mechanical', 'ME', 'B-Block');
```
---
```
CREATE TABLE Person_v2 (
    PersonID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Salary INT,
    JoiningDate DATE,
    DepartmentID INT NULL,
    DesignationID INT NULL
);

INSERT INTO Person_v2 (PersonID, FirstName, LastName, Salary, JoiningDate, DepartmentID, DesignationID) VALUES
(101, 'Rahul', 'Anshu', 56000, '1990-01-01', 1, 12),
(102, 'Hardik', 'Hinsu', 18000, '1990-09-25', 2, 11),
(103, 'Bhavin', 'Kamani', 25000, '1991-05-14', NULL, 11),
(104, 'Bhoomi', 'Patel', 39000, '2014-02-20', 1, 13),
(105, 'Rohit', 'Rajgor', 17000, '1990-07-23', 2, 15),
(106, 'Priya', 'Mehta', 25000, '1990-10-18', 2, NULL),
(107, 'Neha', 'Trivedi', 18000, '2014-02-20', 3, 15);
```
---
```
CREATE TABLE Department_v2 (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(50)
);

INSERT INTO Department_v2 (DepartmentID, DepartmentName) VALUES
(1, 'Admin'),
(2, 'IT'),
(3, 'HR'),
(4, 'Account');
```
---
```
CREATE TABLE Designation (
    DesignationID INT PRIMARY KEY,
    DesignationName VARCHAR(50)
);

INSERT INTO Designation (DesignationID, DesignationName) VALUES
(11, 'Jobber'),
(12, 'Welder'),
(13, 'Clerk'),
(14, 'Manager'),
(15, 'CEO');
```
