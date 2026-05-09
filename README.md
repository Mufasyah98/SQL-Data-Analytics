# 🗄️ SQL Basics for Database Querying & Data Management
### *Case Study 1 — MyShop Sdn Bhd | Retail Sales Analysis*

<p align="center">
  <img src="https://img.shields.io/badge/MySQL-8.0-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL 8.0"/>
  <img src="https://img.shields.io/badge/Level-Beginner%20to%20Intermediate-2E5FA3?style=for-the-badge" alt="Level"/>
  <img src="https://img.shields.io/badge/Dataset-2%2C256%20rows-F4A700?style=for-the-badge" alt="Dataset"/>
  <img src="https://img.shields.io/badge/License-MIT-1E8449?style=for-the-badge" alt="License"/>
</p>

<p align="center">
  <strong>A complete, hands-on SQL training course built around a realistic Malaysian retail dataset.</strong><br/>
  From installation → schema design → querying → business analysis → insights.
</p>

---

## 📋 Table of Contents

- [About This Course](#-about-this-course)
- [Learning Outcomes](#-learning-outcomes)
- [Course Materials](#-course-materials)
- [Dataset Overview](#-dataset-overview)
- [Database Schema](#-database-schema)
- [Course Structure](#-course-structure)
- [Getting Started](#-getting-started)
- [SQL Quick Reference](#-sql-quick-reference)
- [Practice Exercises](#-practice-exercises)
- [Instructor Information](#-instructor-information)

---

## 📖 About This Course

This repository contains all training materials for the **SQL Basics for Database Querying & Data Management** course delivered by Fakhrul Syahmi, Data Consultant & Certified Trainer.

The course is built around **Case Study 1: MyShop Sdn Bhd** — a simulated Malaysian retail company. Instead of abstract exercises, every query you write answers a real business question about customers, products, orders, and revenue.

**Suitable for:**
- Corporate professionals with no prior SQL experience
- Data analysts upskilling in MySQL
- Anyone moving from Excel to databases
- Students in data science or business analytics programmes

**Prerequisites:** Basic computer literacy. No prior SQL or programming experience required.

---

## 🎯 Learning Outcomes

By the end of this course, participants will be able to:

| # | Skill | Phase |
|---|-------|-------|
| 1 | Set up a MySQL database from scratch with correct schema and constraints | Phase 1 |
| 2 | Import structured CSV data into relational tables in the correct FK order | Phase 1 |
| 3 | Explore schema structure, distributions, and data quality before querying | Phase 2 |
| 4 | Write `SELECT`, `WHERE`, `JOIN`, `GROUP BY`, `ORDER BY`, and `LIMIT` queries | Phase 3 |
| 5 | Apply date filtering, aggregate functions, and anti-join patterns | Phase 3 |
| 6 | Use CTEs (`WITH`), `CASE WHEN`, and `CREATE VIEW` for advanced analysis | Phase 4 |
| 7 | Translate SQL query results into business insights and recommendations | Phase 5 |

---

## 📦 Course Materials

All files are included in this repository:

```
📁 sql-basics-myshop/
│
├── 📄 README.md                                  ← You are here
│
├── 📂 dataset/
│   ├── myshop_customers.csv                      ← 200 customer records
│   ├── myshop_products.csv                       ← 100 products (10 categories)
│   ├── myshop_orders.csv                         ← 600 orders (2020–2024)
│   ├── myshop_order_items.csv                    ← 1,356 line items
│   └── myshop_import.sql                         ← Schema creation + import guide
│
├── 📂 slides/
│   ├── MyShop_SQL_CaseStudy1_Trainer_Deck.pptx   ← Trainer edition (with notes)
│   └── MyShop_SQL_CaseStudy1_Participant_Deck.pptx ← Participant workbook
│
└── 📂 docs/
    ├── MySQL_Installation_Tutorial.docx           ← Setup guide (Step 1 → Ready)
    ├── SQL_CaseStudies_Collection.docx            ← All 5 case studies with solutions
    └── MyShop_SQL_FullTutorial.docx               ← Full end-to-end tutorial document
```

---

## 📊 Dataset Overview

The **MyShop Sdn Bhd** dataset simulates a mid-sized Malaysian retail company operating across Peninsular Malaysia and East Malaysia.

| Table | Rows | Description |
|-------|------|-------------|
| `customers` | 200 | Malaysian customers across 20 cities |
| `products` | 100 | 10 products × 10 categories |
| `orders` | 600 | Orders placed from 2020 to 2024 |
| `order_items` | 1,356 | Individual product line items per order |
| **Total** | **2,256** | |

**What makes this dataset realistic:**
- 🇲🇾 **Malaysian context** — names (Malay, Chinese, Indian), real cities (KL, Penang, JB, Ipoh, etc.), RM pricing
- 🛍️ **10 product categories** — Electronics, Clothing, Health & Wellness, F&B, Automotive, and more
- 📦 **Mixed order statuses** — Completed, Processing, Shipped, Cancelled, Refunded
- 💳 **5 payment methods** — Online Banking, Credit Card, Debit Card, E-Wallet, Cash on Delivery
- 🏆 **Loyalty patterns** — 40 customers have higher purchase frequency (realistic distribution)
- 💰 **Discounts** — ~20% of line items carry 5–20% promotional discounts

---

## 🗂️ Database Schema

```sql
┌──────────────────┐        ┌──────────────────┐
│   customers      │        │   products       │
├──────────────────┤        ├──────────────────┤
│ customer_id (PK) │        │ product_id  (PK) │
│ full_name        │        │ product_name     │
│ email            │        │ category         │
│ phone            │        │ unit_price       │
│ city             │        │ stock_quantity   │
│ join_date        │        │ is_active        │
└────────┬─────────┘        └────────┬─────────┘
         │ 1                         │ 1
         │                           │
         │ N                         │ N
┌────────┴─────────┐        ┌────────┴─────────┐
│   orders         │        │   order_items    │
├──────────────────┤        ├──────────────────┤
│ order_id    (PK) │ 1───N  │ item_id     (PK) │
│ customer_id (FK) │        │ order_id    (FK) │
│ order_date       │        │ product_id  (FK) │
│ status           │        │ quantity         │
│ payment_method   │        │ unit_price       │
│ total_amount     │        │ discount         │
└──────────────────┘        │ subtotal         │
                            └──────────────────┘
```

**Relationship Summary:**
- One **customer** can place many **orders** (1:N)
- One **order** can contain many **order_items** (1:N)
- One **product** can appear in many **order_items** (1:N)

---

## 🗓️ Course Structure

The course follows a 5-phase workflow that mirrors real-world data analyst practice:

### Phase 1 — Database Setup & Import
> *"Build the foundation before writing a single query."*

| Step | Task | Key Command |
|------|------|-------------|
| 1 | Create database & tables | `CREATE DATABASE`, `CREATE TABLE` |
| 2 | Import CSV files (in FK order) | Workbench Import Wizard |
| 3 | Verify row counts | `SELECT COUNT(*) ... UNION ALL` |
| 4 | Add performance indexes | `CREATE INDEX` |

⚠️ **Import order:** `customers` → `products` → `orders` → `order_items`

---

### Phase 2 — Schema Exploration
> *"Know your data before you trust your results."*

```sql
-- Always start here
DESCRIBE customers;
SELECT * FROM orders LIMIT 10;
SELECT status, COUNT(*) FROM orders GROUP BY status;
SELECT MIN(order_date), MAX(order_date) FROM orders;
```

---

### Phase 3 — Core SQL Tasks (5 Queries)

| Task | Business Question | Concepts |
|------|------------------|----------|
| **Task 1** | List all customers from Kuala Lumpur | `SELECT`, `WHERE`, `ORDER BY` |
| **Task 2** | Total revenue per product category | `JOIN`, `GROUP BY`, `SUM()` |
| **Task 3** | Top 5 customers by total spending | `TOP-N`, `LIMIT`, `ROUND()` |
| **Task 4** | Orders placed in Q1 2024 | `BETWEEN`, date functions |
| **Task 5** | Customers who never placed an order | `LEFT JOIN`, Anti-Join, `IS NULL` |

#### Task 1 — Example
```sql
SELECT customer_id, full_name, email, phone
FROM   customers
WHERE  city = 'Kuala Lumpur'
ORDER  BY full_name ASC;
```

#### Task 2 — Example
```sql
SELECT   p.category,
         COUNT(DISTINCT o.order_id)     AS total_orders,
         SUM(oi.quantity)               AS units_sold,
         ROUND(SUM(oi.subtotal), 2)     AS net_revenue
FROM     order_items  oi
JOIN     products     p  ON oi.product_id = p.product_id
JOIN     orders       o  ON oi.order_id   = o.order_id
WHERE    o.status = 'Completed'
GROUP BY p.category
ORDER BY net_revenue DESC;
```

#### Task 5 — Anti-Join Pattern
```sql
SELECT c.customer_id, c.full_name, c.city
FROM   customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE  o.order_id IS NULL
ORDER  BY c.join_date DESC;
```

---

### Phase 4 — Advanced Analysis (8 Queries)

| Analysis | Business Question | Key Concept |
|----------|-----------------|-------------|
| A1 | Monthly revenue trend 2022–2024 | `DATE_FORMAT`, time series |
| A2 | Best-selling products by revenue & volume | Multi-table `JOIN` + `LIMIT` |
| A3 | Customer segmentation | `WITH` CTE + `CASE WHEN` |
| A4 | Discount impact on revenue | Conditional aggregation |
| A5 | Sales by city & region | Geographic grouping |
| A6 | Payment method preference | Distribution analysis |
| A7 | Order cancellation rate | `CASE WHEN` in aggregate |
| A8 | Reusable sales dashboard | `CREATE VIEW` |

#### A3 — CTE Segmentation Example
```sql
WITH customer_orders AS (
    SELECT c.customer_id, c.full_name,
           COUNT(o.order_id)   AS order_count,
           SUM(o.total_amount) AS lifetime_value
    FROM   customers c
    LEFT JOIN orders o ON c.customer_id = o.customer_id
      AND o.status = 'Completed'
    GROUP BY c.customer_id, c.full_name
)
SELECT customer_id, full_name, order_count,
       CASE
           WHEN order_count = 0  THEN 'Inactive'
           WHEN order_count = 1  THEN 'One-Time Buyer'
           WHEN order_count <= 3 THEN 'Occasional Buyer'
           WHEN order_count <= 6 THEN 'Regular Customer'
           ELSE                       'Loyal / VIP'
       END AS segment
FROM customer_orders
ORDER BY order_count DESC;
```

#### A8 — Create a Reusable VIEW
```sql
CREATE OR REPLACE VIEW vw_sales_summary AS
SELECT o.order_id, o.order_date,
       DATE_FORMAT(o.order_date, '%Y-%m') AS order_month,
       o.status, o.payment_method,
       c.full_name AS customer_name, c.city,
       p.product_name, p.category,
       oi.quantity, oi.discount, oi.subtotal AS line_total
FROM   orders o
JOIN   customers   c  ON o.customer_id = c.customer_id
JOIN   order_items oi ON o.order_id    = oi.order_id
JOIN   products    p  ON oi.product_id = p.product_id;

-- Use the view (no JOIN required!)
SELECT category, SUM(line_total) AS revenue
FROM   vw_sales_summary
WHERE  status = 'Completed'
GROUP  BY category
ORDER  BY revenue DESC;
```

---

### Phase 5 — Business Insights

> *"SQL is a tool — the value lies in the question you ask."*

| SQL Finding | Business Insight | Recommended Action |
|-------------|-----------------|-------------------|
| X% customers never ordered | Lost acquisition investment | Re-engagement email + first-order discount |
| Top 5 = Y% of revenue | High revenue concentration risk | VIP loyalty tier with exclusive perks |
| Electronics = #1 category | High-value category drives revenue | More inventory + homepage feature |
| Q4 revenue spike | Clear seasonal demand peak | Pre-load stock 6 weeks before Q4 |
| Cancel rate > 8% | Post-purchase abandonment | Survey customers; check logistics |
| Credit Card: highest avg value | Premium buyers prefer cards | Instalment plans for items > RM200 |

**Executive KPI Summary Query:**
```sql
SELECT
    (SELECT COUNT(*) FROM customers)                           AS total_customers,
    (SELECT COUNT(DISTINCT customer_id) FROM orders
     WHERE  status = 'Completed')                             AS active_buyers,
    (SELECT ROUND(SUM(total_amount), 2) FROM orders
     WHERE  status = 'Completed')                             AS total_revenue_rm,
    (SELECT ROUND(AVG(total_amount), 2) FROM orders
     WHERE  status = 'Completed')                             AS avg_order_value_rm,
    (SELECT COUNT(*) FROM products WHERE is_active = 1)        AS active_products,
    (SELECT MIN(order_date) FROM orders)                       AS data_from,
    (SELECT MAX(order_date) FROM orders)                       AS data_to;
```

---

## 🚀 Getting Started

### Prerequisites

- Windows 10 / 11 (64-bit)
- [MySQL 8.0 Community Server](https://dev.mysql.com/downloads/installer/) — full installer (~450 MB)
- [MySQL Workbench 8.0](https://dev.mysql.com/downloads/workbench/) — included in Developer Default install

> 📖 See `docs/MySQL_Installation_Tutorial.docx` for the full step-by-step installation guide.

---

### Step 1 — Install MySQL

```
1. Download MySQL Installer from: https://dev.mysql.com/downloads/installer/
2. Run as Administrator → Choose "Developer Default" setup type
3. Set root password (save it securely!)
4. Complete installation → MySQL80 service starts automatically
```

Verify installation:
```bash
mysql --version
# Expected: mysql  Ver 8.0.xx Distrib 8.0.xx, for Win64 (x86_64)
```

---

### Step 2 — Clone This Repository

```bash
git clone https://github.com/fakhrulsyahmi/sql-basics-myshop.git
cd sql-basics-myshop
```

Or download as ZIP → extract to a local folder.

---

### Step 3 — Create the Database Schema

Open MySQL Workbench → connect to `localhost:3306` → open a new Query tab → run:

```sql
-- Copy and run the full contents of: dataset/myshop_import.sql
SOURCE /path/to/dataset/myshop_import.sql;
```

Or copy-paste the script directly into the Workbench query editor.

---

### Step 4 — Import the CSV Files

Import **in this exact order** (foreign key constraints require it):

| Order | File | Target Table |
|-------|------|-------------|
| 1st | `myshop_customers.csv` | `customers` |
| 2nd | `myshop_products.csv` | `products` |
| 3rd | `myshop_orders.csv` | `orders` |
| 4th | `myshop_order_items.csv` | `order_items` |

**How to import in Workbench:**
1. Expand `myshop_db` in the Schemas panel
2. Right-click the target table → **Table Data Import Wizard**
3. Browse to the CSV file → Next
4. Verify column mapping → Next → Execute
5. Repeat for each table

---

### Step 5 — Verify Your Setup

```sql
USE myshop_db;

SELECT 'customers'   AS table_name, COUNT(*) AS rows FROM customers   UNION ALL
SELECT 'products',                  COUNT(*)          FROM products     UNION ALL
SELECT 'orders',                    COUNT(*)          FROM orders       UNION ALL
SELECT 'order_items',               COUNT(*)          FROM order_items;
```

**Expected output:**

```
+--------------+------+
| table_name   | rows |
+--------------+------+
| customers    |  200 |
| products     |  100 |
| orders       |  600 |
| order_items  | 1356 |
+--------------+------+
```

✅ If all counts match, you are ready to start querying!

---

## 📚 SQL Quick Reference

### Clause Order (Always Follow This)

```sql
SELECT   columns
FROM     table
JOIN     other_table ON condition
WHERE    filter_condition
GROUP BY grouping_column
HAVING   aggregate_filter
ORDER BY sort_column DESC
LIMIT    n;
```

### Essential Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `SELECT` | Retrieve columns | `SELECT name, city FROM customers` |
| `WHERE` | Filter rows | `WHERE city = 'Kuala Lumpur'` |
| `INNER JOIN` | Matching rows only | `JOIN products p ON oi.product_id = p.product_id` |
| `LEFT JOIN` | All left rows + matches | `LEFT JOIN orders o ON c.customer_id = o.customer_id` |
| `GROUP BY` | Group for aggregation | `GROUP BY category` |
| `HAVING` | Filter grouped results | `HAVING SUM(total) > 1000` |
| `ORDER BY` | Sort results | `ORDER BY revenue DESC` |
| `LIMIT` | Restrict row count | `LIMIT 10` |
| `CASE WHEN` | Conditional logic | `CASE WHEN qty > 5 THEN 'High' ELSE 'Low' END` |
| `WITH` | Named subquery (CTE) | `WITH cte AS (SELECT ...) SELECT * FROM cte` |
| `CREATE VIEW` | Save reusable query | `CREATE VIEW vw_name AS SELECT ...` |

### Date Functions

```sql
YEAR(date)                    -- → 2024
MONTH(date)                   -- → 3
QUARTER(date)                 -- → 1
DATE_FORMAT(date, '%Y-%m')    -- → '2024-03'
MONTHNAME(date)               -- → 'March'
DATEDIFF(date1, date2)        -- → days between
CURDATE()                     -- → today's date
NOW()                         -- → current datetime
```

### Common Mistakes to Avoid

```sql
-- ❌ WRONG: String without quotes
WHERE city = Kuala Lumpur

-- ✅ CORRECT: Always quote strings
WHERE city = 'Kuala Lumpur'

-- ❌ WRONG: Missing column in GROUP BY
SELECT name, SUM(amount) FROM orders GROUP BY id

-- ✅ CORRECT: All non-aggregate columns in GROUP BY
SELECT name, SUM(amount) FROM orders GROUP BY id, name

-- ❌ WRONG: WHERE on aggregate
WHERE SUM(total_amount) > 1000

-- ✅ CORRECT: HAVING for aggregates
GROUP BY customer_id HAVING SUM(total_amount) > 1000
```

---

## 💪 Practice Exercises

Work through these exercises in order after completing each phase:

### Beginner
1. List all customers from Penang sorted by `join_date` newest first
2. Find all products in the `Electronics` category priced above RM100
3. Count how many orders exist per `status`
4. Find products with `stock_quantity` below 50

### Intermediate
5. Calculate total revenue per city (Completed orders only)
6. Find the top 3 products by units sold in the `Health & Wellness` category
7. List customers who joined in 2023 but have never placed an order
8. Calculate the average order value per payment method

### Advanced
9. Rank customers by lifetime spending within each city using `RANK() OVER (PARTITION BY city ORDER BY SUM(total_amount) DESC)`
10. Calculate month-over-month revenue growth % using `LAG()` window function
11. Find the most commonly co-purchased product pairs using a self-join on `order_items`
12. Calculate each customer's days between first and last order using `DATEDIFF(MAX(order_date), MIN(order_date))`

---

## 🛠️ Troubleshooting

| Problem | Likely Cause | Fix |
|---------|-------------|-----|
| `Can't connect (10061)` | MySQL service not running | Open Services → Start MySQL80 |
| `Access denied for 'root'` | Wrong password | Reset via `ALTER USER` (see install tutorial) |
| `mysql not recognized` | MySQL not in PATH | Add `C:\Program Files\MySQL\MySQL Server 8.0\bin` to System PATH |
| FK error during import | Wrong import order | Truncate table, re-import in correct sequence |
| `Table doesn't exist` | Wrong database selected | Run `USE myshop_db;` first |
| `ERROR 1055 GROUP BY` | Incomplete GROUP BY | Add all non-aggregate SELECT columns to GROUP BY |

---

## 👨‍💼 Instructor Information

<table>
  <tr>
    <td><strong>Name</strong></td>
    <td>Fakhrul Syahmi</td>
  </tr>
  <tr>
    <td><strong>Role</strong></td>
    <td>Data Consultant & Certified Trainer</td>
  </tr>
  <tr>
    <td><strong>Specialisation</strong></td>
    <td>Data Analytics · Business Intelligence · AI Workplace Productivity</td>
  </tr>
  <tr>
    <td><strong>Tools</strong></td>
    <td>MySQL · Power BI · Excel · Looker Studio · Power Platform · Python</td>
  </tr>
  <tr>
    <td><strong>Clients</strong></td>
    <td>Perodua · Bank Rakyat · TNB · Teleperformance · HELP University</td>
  </tr>
  <tr>
    <td><strong>Email</strong></td>
    <td><a href="mailto:mufasyahcons@gmail.com">mufasyahcons@gmail.com</a></td>
  </tr>
</table>

---

## 📄 License

This training material is © 2026 Fakhrul Syahmi. All rights reserved.

The dataset included in this repository is **synthetic** — generated for training purposes only. Any resemblance to real persons, companies, or transactions is coincidental.

You may use and adapt these materials for **non-commercial educational purposes** with attribution.

---

<p align="center">
  <em>Built with ❤️ for the Malaysian data community</em><br/>
  <strong>SQL Basics for Database Querying & Data Management — Case Study 1: MyShop Sdn Bhd</strong>
</p>
