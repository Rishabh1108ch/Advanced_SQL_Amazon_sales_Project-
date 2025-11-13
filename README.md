# 📊 Amazon Sales SQL Analysis

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

## 🧾 Sample SQL Query

```sql
-- Calculate average return time per category
SELECT 
    category,
    COALESCE(AVG(DATEDIFF(return_date, shipping_date)), 0) AS avg_return_days
FROM sales
GROUP BY category
ORDER BY avg_return_days ASC;
