# 📊 Advanced Commercial SQL Dashboard

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![SQL](https://img.shields.io/badge/SQL-Advanced_Queries-336791?style=for-the-badge&logo=database&logoColor=white)

> **An interactive, browser-based portfolio project demonstrating end-to-end database architecture, constraint troubleshooting, and advanced Data Query Language (DQL) techniques.**

## 📖 Overview

This project encapsulates a comprehensive case study of a commercial database system (similar to the classic Northwind schema). 

Instead of presenting raw `.sql` files, this repository features a **Single-Page Application (SPA)** that acts as an educational dashboard. It walks the user through the database lifecycle: from initial creation (DDL) and mass data population (DML), to fixing structural integrity issues (`ALTER TABLE`), and finally executing 10 complex business intelligence queries.

---

## 🗄️ Database Schema

The relational database models a complete commercial supply chain featuring 7 interconnected tables:

* **CATEGORIES:** Product classifications.
* **CUSTOMERS:** Client directory and regional data.
* **EMPLOYEES:** Staff hierarchy, including self-referencing `REPORTS_TO` management links.
* **SUPPLIERS:** Vendor directory.
* **PRODUCTS:** Inventory tracking, pricing, and supplier/category mappings.
* **ORDERS:** Transaction headers linking customers to the employees who processed them.
* **ORDER_DETAILS:** Transaction line items detailing quantity, product references, and dynamic discounts.

---

## 🧠 Advanced SQL Techniques Demonstrated

This project showcases solutions to 10 highly specific business constraints, utilizing advanced SQL concepts including:

1.  **Conditional Aggregation:** Pivoting row data into columns using `SUM(CASE WHEN...)` to find yearly order differences.
2.  **Relational Division:** Finding customers who have ordered *every single product* in the catalog using `HAVING COUNT(DISTINCT ...)`.
3.  **Tuple Subqueries:** Comparing multiple columns simultaneously (Country, City, Postal Code) in a single `WHERE` clause.
4.  **Complex JOIN Logic:** Bridging up to 4 tables simultaneously while using `LEFT JOIN`s to preserve zero-value records (e.g., customers with exactly 0 or 1 dessert orders).
5.  **Dynamic Value Categorization:** Using nested `CASE` statements to dynamically apply discount brackets based on aggregated line-item totals.
6.  **Referential Integrity Troubleshooting:** Correcting syntax and structural logic to enforce strict `FOREIGN KEY` constraints post-table creation.

---

## 🚀 Quick Start

This dashboard is built entirely with frontend technologies, requiring no local database server installation to view the code and explanations.

1.  Clone or download this repository.
2.  Locate `advanced_commercial_sql_project.html`.
3.  **Double-click** to open it in any modern web browser (Chrome, Edge, Firefox, Safari).
4.  Use the dark-mode sidebar to navigate between the Schema Definition, the DDL/DML setup scripts, and the 10 Query Solutions.

---

## 💻 Sample Query Highlight

**Objective:** *Display customers from Berlin who have ordered at most 1 (0 or 1) dessert product.*

```sql
SELECT C.CUSTOMER_CODE
FROM CUSTOMERS C
LEFT JOIN ORDERS O ON C.CUSTOMER_CODE = O.CUSTOMER_CODE
LEFT JOIN ORDER_DETAILS OD ON O.ORDER_int = OD.ORDER_int
LEFT JOIN PRODUCTS P ON OD.PRODUCT_REF = P.PRODUCT_REF
LEFT JOIN CATEGORIES CAT ON P.CATEGORY_CODE = CAT.CATEGORY_CODE 
WHERE C.CITY = 'Berlin'
GROUP BY C.CUSTOMER_CODE
HAVING COUNT(DISTINCT CASE WHEN CAT.CATEGORY_NAME = 'Desserts' THEN P.PRODUCT_REF END) <= 1;
