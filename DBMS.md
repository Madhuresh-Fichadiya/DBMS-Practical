---

# 📘 LEVEL 1 — 2 TABLE JOINS

---

# A) Without Aggregation (2 Queries)

## 1. Display customer details with their orders.
<details>
<summary>Solution</summary>
```sql
SELECT
    c.CustomerID,
    c.CustomerName,
    o.OrderID,
    o.OrderDate
FROM Customers c
JOIN Orders o
ON c.CustomerID = o.CustomerID;
```
</details>
---

## 2. Display product name with category.
<details>
<summary>Solution</summary>
```sql
SELECT
    p.ProductName,
    p.Price,
    c.CategoryName
FROM Products p
JOIN Categories c
ON p.CategoryID = c.CategoryID;
```
</details>
---

# B) With Aggregation (2 Queries)

## 1. Number of orders placed by each customer.
<details>
<summary>Solution</summary>
```sql
SELECT
    c.CustomerName,
    COUNT(o.OrderID) AS TotalOrders
FROM Customers c
LEFT JOIN Orders o
ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerName;
```
</details>
---

## 2. Average product price in each category.
<details>
<summary>Solution</summary>
```sql
SELECT
    c.CategoryName,
    AVG(p.Price) AS AveragePrice
FROM Categories c
JOIN Products p
ON c.CategoryID = p.CategoryID
GROUP BY c.CategoryName;
```
</details>
---

# C) CTE + Window Functions (2 Queries)
<details>
<summary>Solution</summary>
## 1. Rank customers based on number of orders.

```sql
WITH CustomerOrders AS
(
    SELECT
        c.CustomerName,
        COUNT(o.OrderID) AS TotalOrders
    FROM Customers c
    LEFT JOIN Orders o
    ON c.CustomerID=o.CustomerID
    GROUP BY c.CustomerName
)

SELECT *,
DENSE_RANK() OVER(ORDER BY TotalOrders DESC) Ranking
FROM CustomerOrders;
```
</details>
---

## 2. Rank products by price within category.
<details>
<summary>Solution</summary>
```sql
SELECT
    p.ProductName,
    c.CategoryName,
    p.Price,

    DENSE_RANK() OVER(
        PARTITION BY c.CategoryName
        ORDER BY p.Price DESC
    ) PriceRank

FROM Products p
JOIN Categories c
ON p.CategoryID=c.CategoryID;
```
</details>
---

# 📘 LEVEL 2 — 3 TABLE JOINS

Customers → Orders → OrderItems

---

# A) Without Aggregation

## 1.
<details>
<summary>Solution</summary>
```sql
SELECT
    c.CustomerName,
    o.OrderID,
    oi.ProductID,
    oi.Quantity
FROM Customers c
JOIN Orders o
ON c.CustomerID=o.CustomerID

JOIN OrderItems oi
ON o.OrderID=oi.OrderID;
```
</details>

---

## 2.
<details>
<summary>Solution</summary>
```sql
SELECT
    c.CustomerName,
    o.OrderDate,
    oi.Quantity
FROM Customers c
JOIN Orders o
ON c.CustomerID=o.CustomerID

JOIN OrderItems oi
ON o.OrderID=oi.OrderID;
```
</details>
---

# B) With Aggregation

## 1. Total quantity purchased by each customer.
<details>
<summary>Solution</summary>
```sql
SELECT
    c.CustomerName,
    SUM(oi.Quantity) TotalItems
FROM Customers c
JOIN Orders o
ON c.CustomerID=o.CustomerID

JOIN OrderItems oi
ON o.OrderID=oi.OrderID

GROUP BY c.CustomerName;
```
</details>
---

## 2. Number of products in each order.
<details>
<summary>Solution</summary>
```sql
SELECT
    o.OrderID,
    COUNT(oi.ProductID) TotalProducts
FROM Orders o
JOIN Customers c
ON c.CustomerID=o.CustomerID

JOIN OrderItems oi
ON o.OrderID=oi.OrderID

GROUP BY o.OrderID;
```
</details>
---

# C) CTE + Window

## 1.
<details>
<summary>Solution</summary>
```sql
WITH CustomerQty AS
(
SELECT
c.CustomerName,
SUM(oi.Quantity) Qty

FROM Customers c
JOIN Orders o
ON c.CustomerID=o.CustomerID

JOIN OrderItems oi
ON o.OrderID=oi.OrderID

GROUP BY c.CustomerName
)

SELECT *,
ROW_NUMBER() OVER(ORDER BY Qty DESC)
FROM CustomerQty;
```
</details>
---

## 2.
<details>
<summary>Solution</summary>
```sql
SELECT
c.CustomerName,
o.OrderDate,
oi.Quantity,

SUM(oi.Quantity)
OVER(PARTITION BY c.CustomerName)
AS TotalPurchased

FROM Customers c

JOIN Orders o
ON c.CustomerID=o.CustomerID

JOIN OrderItems oi
ON o.OrderID=oi.OrderID;
```
</details>
---

# 📘 LEVEL 3 — 4 TABLE JOINS

Customers → Orders → OrderItems → Products

---

# A) Without Aggregation
<details>
<summary>Solution</summary>
## 1.

```sql
SELECT
c.CustomerName,
o.OrderID,
p.ProductName,
oi.Quantity

FROM Customers c

JOIN Orders o
ON c.CustomerID=o.CustomerID

JOIN OrderItems oi
ON o.OrderID=oi.OrderID

JOIN Products p
ON oi.ProductID=p.ProductID;
```
</details>
---

## 2.
<details>
<summary>Solution</summary>
```sql
SELECT
c.CustomerName,
o.OrderDate,
p.ProductName,
p.Price

FROM Customers c

JOIN Orders o
ON c.CustomerID=o.CustomerID

JOIN OrderItems oi
ON o.OrderID=oi.OrderID

JOIN Products p
ON oi.ProductID=p.ProductID;
```
</details>
---

# B) Aggregation

## 1.
<details>
<summary>Solution</summary>
```sql
SELECT
c.CustomerName,
SUM(oi.Quantity*p.Price) TotalSpent

FROM Customers c

JOIN Orders o
ON c.CustomerID=o.CustomerID

JOIN OrderItems oi
ON o.OrderID=oi.OrderID

JOIN Products p
ON oi.ProductID=p.ProductID

GROUP BY c.CustomerName;
```
</details>
---

## 2.
<details>
<summary>Solution</summary>
```sql
SELECT
p.ProductName,
SUM(oi.Quantity) TotalSold

FROM Products p

JOIN OrderItems oi
ON p.ProductID=oi.ProductID

JOIN Orders o
ON oi.OrderID=o.OrderID

JOIN Customers c
ON o.CustomerID=c.CustomerID

GROUP BY p.ProductName;
```
</details>
---

# C) CTE + Window

## 1.
<details>
<summary>Solution</summary>
```sql
WITH Sales AS
(
SELECT
c.CustomerName,
SUM(oi.Quantity*p.Price) Amount

FROM Customers c

JOIN Orders o
ON c.CustomerID=o.CustomerID

JOIN OrderItems oi
ON o.OrderID=oi.OrderID

JOIN Products p
ON oi.ProductID=p.ProductID

GROUP BY c.CustomerName
)

SELECT *,
DENSE_RANK() OVER(ORDER BY Amount DESC)
FROM Sales;
```
</details>
---

## 2.
<details>
<summary>Solution</summary>
```sql
SELECT
c.CustomerName,
p.ProductName,
p.Price,

AVG(p.Price)
OVER(PARTITION BY c.CustomerName)
AvgPrice

FROM Customers c

JOIN Orders o
ON c.CustomerID=o.CustomerID

JOIN OrderItems oi
ON o.OrderID=oi.OrderID

JOIN Products p
ON oi.ProductID=p.ProductID;
```
</details>
---

# 📘 LEVEL 4 — 5 TABLE JOINS

Customers → Orders → OrderItems → Products → Categories

---

# A) Without Aggregation

## 1.
<details>
<summary>Solution</summary>
```sql
SELECT
c.CustomerName,
p.ProductName,
cat.CategoryName,
oi.Quantity

FROM Customers c

JOIN Orders o
ON c.CustomerID=o.CustomerID

JOIN OrderItems oi
ON o.OrderID=oi.OrderID

JOIN Products p
ON oi.ProductID=p.ProductID

JOIN Categories cat
ON p.CategoryID=cat.CategoryID;
```
</details>
---

## 2.
<details>
<summary>Solution</summary>
```sql
SELECT
o.OrderID,
c.CustomerName,
cat.CategoryName,
p.ProductName,
p.Price

FROM Customers c

JOIN Orders o
ON c.CustomerID=o.CustomerID

JOIN OrderItems oi
ON o.OrderID=oi.OrderID

JOIN Products p
ON oi.ProductID=p.ProductID

JOIN Categories cat
ON p.CategoryID=cat.CategoryID;
```
</details>
---

# B) Aggregation

## 1.
<details>
<summary>Solution</summary>
```sql
SELECT
cat.CategoryName,
SUM(oi.Quantity*p.Price) Sales

FROM Categories cat

JOIN Products p
ON cat.CategoryID=p.CategoryID

JOIN OrderItems oi
ON p.ProductID=oi.ProductID

JOIN Orders o
ON oi.OrderID=o.OrderID

JOIN Customers c
ON o.CustomerID=c.CustomerID

GROUP BY cat.CategoryName;
```
</details>
---

## 2.
<details>
<summary>Solution</summary>
```sql
SELECT
c.CustomerName,
cat.CategoryName,
SUM(oi.Quantity*p.Price) Amount

FROM Customers c

JOIN Orders o
ON c.CustomerID=o.CustomerID

JOIN OrderItems oi
ON o.OrderID=oi.OrderID

JOIN Products p
ON oi.ProductID=p.ProductID

JOIN Categories cat
ON p.CategoryID=cat.CategoryID

GROUP BY
c.CustomerName,
cat.CategoryName;
```
</details>
---

# C) CTE + Window

## 1. Highest spending customer in each category.
<details>
<summary>Solution</summary>
```sql
WITH CustomerSales AS
(
SELECT
cat.CategoryName,
c.CustomerName,
SUM(oi.Quantity*p.Price) Amount

FROM Customers c

JOIN Orders o
ON c.CustomerID=o.CustomerID

JOIN OrderItems oi
ON o.OrderID=oi.OrderID

JOIN Products p
ON oi.ProductID=p.ProductID

JOIN Categories cat
ON p.CategoryID=cat.CategoryID

GROUP BY
cat.CategoryName,
c.CustomerName
)

SELECT *,
DENSE_RANK()
OVER(
PARTITION BY CategoryName
ORDER BY Amount DESC
) Ranking

FROM CustomerSales;
```
</details>
---

## 2. Running sales total by category.
<details>
<summary>Solution</summary>
```sql
SELECT
cat.CategoryName,
c.CustomerName,
SUM(oi.Quantity*p.Price) Amount,

SUM(SUM(oi.Quantity*p.Price))
OVER(
PARTITION BY cat.CategoryName
ORDER BY c.CustomerName
) RunningTotal

FROM Customers c

JOIN Orders o
ON c.CustomerID=o.CustomerID

JOIN OrderItems oi
ON o.OrderID=oi.OrderID

JOIN Products p
ON oi.ProductID=p.ProductID

JOIN Categories cat
ON p.CategoryID=cat.CategoryID

GROUP BY
cat.CategoryName,
c.CustomerName;
```
</details>
