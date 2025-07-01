                                               #Task-6(Subqueries and Nested Queries)
# Customer-and-Orders-Database
# 🔍 SQL Subqueries

Subqueries are essential for building complex queries by allowing one query to be nested within another.

# 📁 Project Overview

This section showcases how to write and use **subqueries** in SQL to solve real-world database problems.

Subqueries are powerful tools used to:
- Compare results from different queries
- Filter data using conditions from another table
- Return single or multiple values inside conditions

This project is part of my learning and internship submission, aimed at demonstrating my understanding of database design concepts.

# 📌 Tables:
- Customers
- Orders

# 🧾 SQL Script

Creating the data
```
-- Create Customers table
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Email VARCHAR(100) UNIQUE
);

-- Create Orders table
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    Amount DECIMAL(10, 2),
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```
Inserting the data
```
-- Insert into Customers
INSERT INTO Customers (CustomerID, Name, Email) VALUES
(1, 'Kajal', 'kajal234@gmail.com'),
(2, 'Naved', 'naved764@gmail.com'),
(3, 'Zanib', 'zainb876@gmail.com'),
(4, 'Sonali','sonali980@gmail.com');

-- Insert into Orders
INSERT INTO Orders (OrderID, CustomerID, OrderDate, Amount) VALUES
(101, 1, '2025-06-01', 1500.00),
(102, 2, '2025-06-05', 2000.00),
(103, 3, '2025-06-03', 2500.00),
(104, 4, '2025-06-30', 3000.00);

```
# Subqueries

### 1️⃣ Scalar Subqueries

A **scalar subquery** returns a **single value**, often used in `WHERE`, `SELECT`, or `HAVING` clauses.

```
SELECT Name
FROM Customers
WHERE CustomerID IN (
    SELECT CustomerID
    FROM Orders
    GROUP BY CustomerID
    HAVING SUM(Amount) > (
        SELECT AVG(Amount) FROM Orders
    )
);
```
Output is:-

![image](https://github.com/user-attachments/assets/7acb99ac-0f79-4811-955e-ee0a5dbc241d)

### 2️⃣ Correlated Subqueries

A correlated subquery depends on a value from the outer query.

```
SELECT Name
FROM Customers c
WHERE EXISTS (
    SELECT 1
    FROM Orders o
    WHERE o.CustomerID = c.CustomerID AND o.Amount < 2000
);
```

Output is:-

![image](https://github.com/user-attachments/assets/d5b32543-413f-464f-918e-c824070322f2)

### 3️⃣ Subquery with **IN**

```
SELECT Name
FROM Customers
WHERE CustomerID IN (
    SELECT CustomerID FROM Orders
);
```

Output is:-

![image](https://github.com/user-attachments/assets/b22edcbe-8b7f-4b54-9773-584291e0f30e)


### 4️⃣ Subquery with **EXISTS**

```
SELECT Name
FROM Customers c
WHERE EXISTS (
    SELECT 1 FROM Orders o
    WHERE o.CustomerID = c.CustomerID
);
```

Output is:-

![image](https://github.com/user-attachments/assets/8c8dc0c6-3bac-4ec8-a9e1-312d2040d1dc)

### 5️⃣ Subquery with **=**
```
SELECT Name
FROM Customers
WHERE CustomerID = (
    SELECT TOP 1 CustomerID
    FROM Orders
    ORDER BY Amount DESC
);
```

Output is:-

![image](https://github.com/user-attachments/assets/0969561a-f45b-4394-90ce-6ee2122ea24e)












