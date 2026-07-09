# Customers

| CustomerID | CustomerName | Email                                     | City      |
| ---------- | ------------ | ----------------------------------------- | --------- |
| 1          | Rahul Sharma | [rahul@gmail.com](mailto:rahul@gmail.com) | Delhi     |
| 2          | Amit Patel   | [amit@gmail.com](mailto:amit@gmail.com)   | Mumbai    |
| 3          | Priya Singh  | [priya@gmail.com](mailto:priya@gmail.com) | Pune      |
| 4          | Neha Verma   | [neha@gmail.com](mailto:neha@gmail.com)   | Ahmedabad |
| 5          | John Thomas  | [john@gmail.com](mailto:john@gmail.com)   | Bangalore |
| 6          | Riya Shah    | [riya@gmail.com](mailto:riya@gmail.com)   | Surat     |

---

# Categories

| CategoryID | CategoryName |
| ---------- | ------------ |
| 1          | Electronics  |
| 2          | Accessories  |
| 3          | Furniture    |
| 4          | Books        |

---

# Products

| ProductID | ProductName | CategoryID | Price |
| --------- | ----------- | ---------- | ----: |
| 101       | Laptop      | 1          | 65000 |
| 102       | Mouse       | 2          |   800 |
| 103       | Keyboard    | 2          |  1500 |
| 104       | Monitor     | 1          | 12000 |
| 105       | Chair       | 3          |  4500 |
| 106       | Table       | 3          |  7000 |
| 107       | SQL Book    | 4          |   600 |
| 108       | Java Book   | 4          |   750 |

---

# Orders

| OrderID | CustomerID | OrderDate  |
| ------- | ---------- | ---------- |
| 1001    | 1          | 2025-01-10 |
| 1002    | 2          | 2025-01-12 |
| 1003    | 1          | 2025-02-01 |
| 1004    | 3          | 2025-02-15 |
| 1005    | 5          | 2025-03-01 |
| 1006    | 4          | 2025-03-10 |

---

# OrderItems

| OrderItemID | OrderID | ProductID | Quantity |
| ----------- | ------- | --------- | -------: |
| 1           | 1001    | 101       |        1 |
| 2           | 1001    | 102       |        2 |
| 3           | 1002    | 104       |        1 |
| 4           | 1002    | 103       |        1 |
| 5           | 1003    | 107       |        3 |
| 6           | 1004    | 105       |        2 |
| 7           | 1004    | 106       |        1 |
| 8           | 1005    | 101       |        1 |
| 9           | 1005    | 108       |        2 |
| 10          | 1006    | 102       |        5 |
| 11          | 1006    | 103       |        2 |
| 12          | 1006    | 104       |        1 |

---
