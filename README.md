# 📚 Library Management System — Data Analysis SQL Project

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-17-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-Data%20Analysis-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)
![Level](https://img.shields.io/badge/Level-Intermediate-yellow?style=for-the-badge)

---

## 📖 Project Overview

This project presents a fully designed and implemented **Library Management System** built with **PostgreSQL**. It covers the complete data lifecycle — from relational database design and schema creation to data insertion, querying, and structured SQL-based data analysis.

The system simulates a real-world library environment where books are issued to members, managed by employees across multiple branches, and returned — with all relationships enforced through proper **foreign key constraints**.

> 🎯 **Goal:** Demonstrate practical SQL skills including database design, data manipulation, joins, aggregations, and analytical querying for a data analyst portfolio.

---

## 🖼️ Project Screenshots

### 📌 Library System ERD (Entity Relationship Diagram)
![ERD](ERD%20DB.JPG)

### 📌 Database Schema Overview
![Schema](Library%20Management%20System.png)

---

## 🗄️ Database Schema

The system consists of **6 interrelated tables:**

| Table | Description |
|-------|-------------|
| `branch` | Library branch locations and manager details |
| `employees` | Staff working across different branches |
| `members` | Registered library members |
| `books` | Book inventory with ISBN, category, and rental price |
| `issued_status` | Records of books issued to members |
| `return_status` | Records of books returned by members |

### 🔗 Table Relationships

```
branch ──────< employees
                  │
                  └──────< issued_status >────── members
                                │
                             books
                                │
                          return_status
```

---

## 📂 Project Structure

```
Library_Management_System_Data_Analysis_SQL_Project/
│
├── library_managment_system.sql   -- Schema creation & table setup
├── insert_queries.sql             -- Data insertion for all 6 tables
├── books.csv                      -- Books dataset
├── branch.csv                     -- Branch dataset
├── employees.csv                  -- Employees dataset
├── members.csv                    -- Members dataset
├── issued_status.csv              -- Issued status dataset
├── return_status.csv              -- Return status dataset
├── ERD DB.JPG                     -- Entity Relationship Diagram
├── Library Management System.png  -- Database schema screenshot
└── README.md                      -- Project documentation
```

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **PostgreSQL 17** | Database engine |
| **pgAdmin 4** | Database management & query execution |
| **SQL** | Data definition, manipulation & analysis |

---

## 🔍 SQL Operations & Analysis Tasks

### ✅ Phase 1 — Database Setup (DDL)
- Created all 6 tables with proper data types and constraints
- Applied `ALTER TABLE` to refine column types post-creation
- Enforced **Foreign Key constraints** across all related tables

### ✅ Phase 2 — Data Insertion (DML)
- Inserted complete datasets into all 6 tables
- Imported CSV data using PostgreSQL import functionality
- Resolved foreign key dependency issues during import

### ✅ Phase 3 — Data Analysis (DQL)

| Task | Description | SQL Concepts Used |
|------|-------------|-------------------|
| Task 1 | Retrieve all books in a specific category | `SELECT`, `WHERE` |
| Task 2 | Find members who registered in last 180 days | `CURRENT_DATE`, `INTERVAL` |
| Task 3 | List employees with salary above average | `Subquery`, `AVG` |
| Task 4 | Count total books issued per member | `GROUP BY`, `COUNT` |
| Task 5 | Members who issued more than 1 book | `HAVING`, `COUNT` |
| Task 6 | Books with rental price above average | `Subquery`, `AVG` |
| Task 7 | List books not yet returned | `LEFT JOIN`, `IS NULL` |
| Task 8 | Branch performance report | `JOIN`, `SUM`, `GROUP BY` |
| Task 9 | Employee book processing count | `JOIN`, `COUNT`, `GROUP BY` |
| Task 10 | Create active members summary table | `CTAS`, `INTERVAL` |

---

## 🗃️ Key SQL Concepts Demonstrated

```sql
-- Example: Find members with overdue books (30+ days)
SELECT 
    ist.issued_member_id,
    m.member_name,
    bk.book_title,
    ist.issued_date,
    CURRENT_DATE - ist.issued_date AS overdue_days
FROM issued_status AS ist
JOIN members AS m ON m.member_id = ist.issued_member_id
JOIN books AS bk ON bk.isbn = ist.issued_book_isbn
LEFT JOIN return_status AS rs ON rs.issued_id = ist.issued_id
WHERE rs.return_date IS NULL
  AND (CURRENT_DATE - ist.issued_date) > 30
ORDER BY overdue_days DESC;
```

```sql
-- Example: Branch Performance Report using CTAS
CREATE TABLE branch_reports AS
SELECT 
    b.branch_id,
    b.manager_id,
    COUNT(ist.issued_id)   AS books_issued,
    COUNT(rs.return_id)    AS books_returned,
    SUM(bk.rental_price)   AS total_revenue
FROM issued_status AS ist
JOIN employees AS e ON e.emp_id = ist.issued_emp_id
JOIN branch AS b ON e.branch_id = b.branch_id
LEFT JOIN return_status AS rs ON rs.issued_id = ist.issued_id
JOIN books AS bk ON ist.issued_book_isbn = bk.isbn
GROUP BY b.branch_id, b.manager_id;
```

---

## ▶️ How to Run This Project

**Step 1 — Clone the Repository**
```bash
git clone https://github.com/AhsanTestOps/Library_Management_System_Data_Analysis_SQL_Project.git
```

**Step 2 — Set Up the Database**

Open pgAdmin 4, create a new database called `library_system_management`, then run:
```sql
library_managment_system.sql  -- Run this first
```

**Step 3 — Insert the Data**
```sql
insert_queries.sql  -- Run this second
```

**Step 4 — Run Analysis Queries**

Open the query tool in pgAdmin and run any of the analysis queries to explore the data.

---

## 📊 Key Findings & Insights

- 📌 Tracked book issuance and return patterns across multiple branches
- 📌 Identified overdue books and calculated days overdue per member
- 📌 Analyzed branch performance based on revenue and book activity
- 📌 Found top performing employees by number of books processed
- 📌 Monitored member registration trends over time

---

## 🤝 Connect With Me

If you found this project helpful or have any feedback, feel free to connect!

[![GitHub](https://img.shields.io/badge/GitHub-AhsanTestOps-black?style=for-the-badge&logo=github)](https://github.com/AhsanTestOps)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

⭐ **If you found this project useful, please consider giving it a star!** ⭐
