# Northwind DB EDA

## Project Overview

**Project Title**: Retail Sales Analysis  
**Database**: [`Northwind`](https://en.wikiversity.org/wiki/Database_Examples/Northwind/MySQL)

This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyze retail sales data. The project involves performing exploratory data analysis (EDA), and answering specific business questions through SQL queries. 

## Objectives

1. Perform basic exploratory data analysis to understand the dataset.
2. Use SQL to answer specific business questions and derive insights from the sales data.

# Data Exploration

```sql
SELECT * FROM Customers;
```
```sql
-- Total revenue
SELECT SUM(OrderDetails.Quantity * products.Price) as Total_Sales
FROM OrderDetails
JOIN products on OrderDetails.ProductID = products.ProductID;
```
```sql
-- queries with where clause
SELECT * FROM Customers WHERE Country = 'USA';
SELECT * FROM Employees WHERE Country = 'UK';
```
```sql
--queries with filter
SELECT * FROM Customers WHERE Country = 'USA' AND City = 'Portland';
SELECT * FROM Employees WHERE Country = 'UK' AND City = 'London';
```
```sql
-- Sales in 1997
SELECT SUM(OrderDetails.Quantity * products.Price) as Total_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
WHERE YEAR(orders.OrderDate) = 1997;
```

```sql
-- sales by especific customer and year
SELECT SUM(OrderDetails.Quantity * products.Price) as Total_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
JOIN Customers on orders.CustomerID = Customers.CustomerID
WHERE Customers.CustomerName = 'Ernst Handel' AND YEAR(orders.OrderDate) = 1997;
```

```sql
-- Total revenue by month/year
SELECT 
    YEAR(orders.OrderDate) AS Year, 
    MONTH(orders.OrderDate) AS Month, 
    SUM(OrderDetails.Quantity * products.Price) as Total_Sales 
FROM orders 
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
GROUP BY YEAR(orders.OrderDate), MONTH(orders.OrderDate)
ORDER BY MONTH(orders.OrderDate);
```

```sql
--Sales by year
SELECT 
    YEAR(orders.OrderDate) AS Year, 
    SUM(OrderDetails.Quantity * products.Price) as Total_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
GROUP BY YEAR(orders.OrderDate)
ORDER BY YEAR(orders.OrderDate);
```
```sql
-- Top 10 customers by revenue
SELECT
    Customer.CustomerName,
    SUM(OrderDetails.Quantity * products.Price) as Total_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
JOIN Customers as Customer on orders.CustomerID = Customer.CustomerID
GROUP BY Customer.CustomerName
ORDER BY Total_Sales DESC
LIMIT 10;
```
```sql
-- Top 10 products by quantity sold
SELECT
    products.ProductName,
    SUM(OrderDetails.Quantity) as Total_Quantity
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
GROUP BY products.ProductName
ORDER BY Total_Quantity DESC
LIMIT 10;
```
```sql
-- Top 10 products by revenue
SELECT
    products.ProductName,
    SUM(OrderDetails.Quantity * products.Price) as Total_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
GROUP BY products.ProductName
ORDER BY Total_Sales DESC
LIMIT 10;
```
```sql
-- Sales by country
SELECT
    Customer.Country,
    SUM(OrderDetails.Quantity * products.Price) as Total_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
JOIN Customers as Customer on orders.CustomerID = Customer.CustomerID
GROUP BY Customer.Country
ORDER BY Total_Sales DESC;
```
```sql
-- Sales by category
SELECT
    Categories.CategoryName,
    SUM(OrderDetails.Quantity * products.Price) as Total_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
JOIN Categories on products.CategoryID = Categories.CategoryID
GROUP BY Categories.CategoryName
ORDER BY Total_Sales DESC;
```
```sql
-- Sales by employee
SELECT
    Employees.LastName,
    Employees.FirstName,
    SUM(OrderDetails.Quantity * products.Price) as Total_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
JOIN Employees on orders.EmployeeID = Employees.EmployeeID
GROUP BY Employees.LastName, Employees.FirstName
ORDER BY Total_Sales DESC;
```
```sql
-- Sales by supplier
SELECT
    Suppliers.SupplierName,
    SUM(OrderDetails.Quantity * products.Price) as Total_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
JOIN Suppliers on products.SupplierID = Suppliers.SupplierID
GROUP BY Suppliers.SupplierName
ORDER BY Total_Sales DESC;
```
```sql
-- Sales by shipper
SELECT
    Shippers.ShipperName,
    SUM(OrderDetails.Quantity * products.Price) as Total_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
JOIN Shippers on orders.ShipperID = Shippers.ShipperID
GROUP BY Shippers.ShipperName
ORDER BY Total_Sales DESC;
```
```sql
-- Sales by customer
SELECT
    Customers.CustomerName,
    SUM(OrderDetails.Quantity * products.Price) as Total_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
JOIN Customers on orders.CustomerID = Customers.CustomerID
GROUP BY Customers.CustomerName
ORDER BY Total_Sales DESC;
```
```sql
-- Sales by product
SELECT
    products.ProductName,
    SUM(OrderDetails.Quantity * products.Price) as Total_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
GROUP BY products.ProductName
ORDER BY Total_Sales DESC;
```
```sql
-- Average sales by product
SELECT
    products.ProductName,
    AVG(OrderDetails.Quantity * products.Price) as Average_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
GROUP BY products.ProductName
ORDER BY Average_Sales DESC;
```
```sql
-- Average sales by customer
SELECT
    Customers.CustomerName,
    AVG(OrderDetails.Quantity * products.Price) as Average_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
JOIN Customers on orders.CustomerID = Customers.CustomerID
GROUP BY Customers.CustomerName
ORDER BY Average_Sales DESC;
```
```sql
-- Average sales by employee
SELECT
    Employees.LastName,
    Employees.FirstName,
    AVG(OrderDetails.Quantity * products.Price) as Average_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
JOIN Employees on orders.EmployeeID = Employees.EmployeeID
GROUP BY Employees.LastName, Employees.FirstName
ORDER BY Average_Sales DESC;
```
```sql
-- Average sales by supplier
SELECT
    Suppliers.SupplierName,
    AVG(OrderDetails.Quantity * products.Price) as Average_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
JOIN Suppliers on products.SupplierID = Suppliers.SupplierID
GROUP BY Suppliers.SupplierName
ORDER BY Average_Sales DESC;
```
```sql
-- Average sales by shipper
SELECT
    Shippers.ShipperName,
    AVG(OrderDetails.Quantity * products.Price) as Average_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
JOIN Shippers on orders.ShipperID = Shippers.ShipperID
GROUP BY Shippers.ShipperName
ORDER BY Average_Sales DESC;
```

### Average sales by category
```sql
SELECT
    Categories.CategoryName,
    AVG(OrderDetails.Quantity * products.Price) as Average_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
JOIN Categories on products.CategoryID = Categories.CategoryID
GROUP BY Categories.CategoryName
ORDER BY Average_Sales DESC;
```

### Average sales by country
```sql
SELECT
    Customers.Country,
    AVG(OrderDetails.Quantity * products.Price) as Average_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
JOIN Customers on orders.CustomerID = Customers.CustomerID
GROUP BY Customers.Country
ORDER BY Average_Sales DESC;
```

### Average sales by month/year
```sql
SELECT 
    YEAR(orders.OrderDate) AS Year, 
    MONTH(orders.OrderDate) AS Month, 
    AVG(OrderDetails.Quantity * products.Price) as Average_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
GROUP BY YEAR(orders.OrderDate), MONTH(orders.OrderDate)
ORDER BY MONTH(orders.OrderDate);
```

### Average sales by year
```sql

SELECT 
    YEAR(orders.OrderDate) AS Year, 
    AVG(OrderDetails.Quantity * products.Price) as Average_Sales
FROM orders
JOIN OrderDetails on orders.OrderID = OrderDetails.OrderID
JOIN products on OrderDetails.ProductID = products.ProductID
GROUP BY YEAR(orders.OrderDate)
ORDER BY YEAR(orders.OrderDate);
```

## Findings

- July 1996 shows high sales volume, likely due to bulk orders placed when the system was initialized.

- Sales remain steady through the second half of 1996, suggesting a consistent customer base.

- There's an observable uptick in December, possibly due to holiday demand.

- The beginning of 1997 continues the upward trend—pointing toward growth in business operations.

- Côte de Blaye (wine) ranks as a top revenue generator despite lower order volume.

- Mid-range products like Grandma's Boysenberry Spread and Chartreuse verte appear often.

- Seafood and cheese products dominate the top ranks, indicating strong demand in these categories.

- USA, Germany, and UK contribute the highest total sales.

- Germany shows frequent smaller orders, while USA orders tend to be fewer but larger, indicating different customer behaviors.

- Some countries like Switzerland or Finland contribute little—potential growth markets or candidates for targeted marketing.

- Robert King and Laura Callahan are top performers by total sales—likely handling high-value clients.

- There's a noticeable drop-off after the top 3 salespeople, indicating a possible training gap or uneven workload distribution.

- Some employees are handling many smaller orders; others fewer but high-value ones
