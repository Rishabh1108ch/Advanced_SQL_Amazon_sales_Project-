# 💳 Advanced SQL Project — Amazon-Style E-Commerce Analysis

## 📘 Project Overview

A comprehensive SQL project analyzing **Amazon sales data** using advanced SQL techniques such as window functions, joins, CTEs, aggregations, and date functions to derive meaningful business insights.

---

## 📂 Data

- **Dataset:** Internal Amazon-style sample dataset  
- **Tables Included:** `sales`, `products`, `categories`, `regions`  
- **Total Rows:** ~10,000  
- **Columns:** 15+ attributes including product, category, pricing, dates, region, etc.  
- **Missing Values Handling:** Managed using `COALESCE()` and filtering logic  

---

## 🔍 Business Problem

The goal is to answer key business questions:

- Which categories generate the most revenue?  
- What is the average shipping time?  
- Which regions are underperforming?  
- Which products have high return rates?  
- What are the monthly sales trends?  

---

## 📊 Analysis Performed

### 📦 Category-Level Insights  
- Revenue per category  
- Fastest/slowest shipping categories  
- Highest return-rate categories  

### 🌍 Regional Insights  
- Orders by region  
- Revenue distribution  
- Region-wise shipping delay  

### 🛒 Product Performance  
- Best-selling items  
- Low-performing/slow-moving SKUs  
- Return-prone products  

### 📆 Time Series Insights  
- Monthly & yearly revenue  
- Sales trend analysis  
- Seasonal patterns  

---

## 🧠 SQL Concepts Used

- **Window Functions:**  
  `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, `OVER(PARTITION BY ...)`  

- **Aggregate Functions:**  
  `SUM()`, `AVG()`, `COUNT()`, `MIN()`, `MAX()`  

- **Joins:**  
  INNER JOIN, LEFT JOIN, SELF JOIN  

- **CTEs & Subqueries:**  
  For modular, readable analysis  

- **Date Functions:**  
  `DATEDIFF()`, `YEAR()`, `MONTH()`, `EXTRACT()`  

- **Data Cleaning:**  
  `COALESCE()`, trimming, filtering  

---


---

## 📘 About this Project

This project analyzes a large e-commerce dataset (21,000+ records across 9 interrelated tables) that simulates real-world Amazon business challenges. It demonstrates advanced SQL skills to extract actionable business insights across domains such as sales, customers, products, returns, payments, shipping, sellers, and inventory.

**Key Highlights**
- **Scale:** 21,000+ records, 9 tables  
- **Techniques:** CTEs, Window functions (`LAG`, `DENSE_RANK`, etc.), subqueries, stored procedures  
- **Business value:** Sales trends, profit margin analysis, inventory alerts, seller & customer performance, shipping analytics, return & fraud detection  
- **DBMS used:** Microsoft SQL Server (T-SQL) — SSMS recommended

---

## 🎯 Project Objective

Help Amazon stakeholders (sellers, logistics partners, internal teams) make data-driven decisions to:

- Increase sales  
- Improve inventory management  
- Enhance customer satisfaction & retention  
- Optimize shipping & logistics  
- Reduce fraud & returns

---

## 🗂 Dataset Overview

**Tables (9):**
- `Customers`  
- `Products`  
- `Categories`  
- `Sellers`  
- `Orders`  
- `OrderItems` (or `Order_Details`)  
- `Shipping`  
- `Payments`  
- `Inventory`

**Size & Shape**
- 21,000+ records combined across tables  
- Typical columns: `order_id`, `customer_id`, `product_id`, `category_id`, `seller_id`, `order_date`, `shipping_date`, `return_date`, `quantity`, `price`, `cost`, `payment_status`, `warehouse_id`, `stock_qty`, `restock_date`, etc.

---

## 🧭 Business Problems / Tasks (22)

1. **Fix schema:** change `Orders.order_id` from `MONEY` → `INT`.  
2. **Top 10 products by total sales value.** (name, qty sold, total sales value)  
3. **Total revenue by category** with % contribution to total.  
4. **Average order value (AOV) per customer** — include only customers with > 5 orders.  
5. **Monthly total sales** for the past year (current_month_sales, last_month_sales).  
6. **Customers registered but never ordered** — list details & time since registration.  
7. **Best-selling product per state** (product + total sales in state).  
8. **Least-selling product per state** (product + total sales in state).  
9. **Customer lifetime sales** — total order value per customer and rank by CLV.  
10. **Products with stock < threshold (e.g., <10)** — include last restock date & warehouse.  
11. **Orders with shipping date > 4 days after order date** — include customer & delivery provider.  
12. **Payment success percentage** for all orders — breakdown by payment status.  
13. **Top 5 sellers by total sales value** — include successful vs failed orders and % successful.  
14. **Product profit margin** (price − cost), rank by margin.  
15. **Top 10 products by number of returns** — show return rate as % of units sold.  
16. **Sellers with no sales in last 6 months** — include last sale date and lifetime sales.  
17. **Customer return classification:** if >5 returns → `Returning`, else `New`. (customer id, name, total orders, total returns)  
18. **Top 5 customers by number of orders for each state** — include order count & total sales.  
19. **Total revenue by shipping provider** — include number of orders handled & average delivery time.  
20. **Top 10 products with largest revenue decline (2022 → 2023)** — include 2022 revenue, 2023 revenue, decline ratio (rounded).  
21. **Inventory update function/procedure** — when product sold, decrement inventory quantity.  
22. **Stored procedure for periodic inventory alerts / restock suggestions** (optional extension).

---

## 🧾 Sample SQL snippets (T-SQL)

### 1) Fix `order_id` data type (example)
```sql
-- Example: change order_id from MONEY to INT (T-SQL approach)
ALTER TABLE Orders
ADD order_id_tmp INT;

UPDATE Orders
SET order_id_tmp = TRY_CAST(order_id AS INT);

ALTER TABLE Orders DROP COLUMN order_id;
EXEC sp_rename 'Orders.order_id_tmp', 'order_id', 'COLUMN';
-- Add constraints/index after verifying data

