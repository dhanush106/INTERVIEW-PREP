# 📘 TCS PRIME — THE ULTIMATE SQL INTERVIEW HANDBOOK
### For TCS Prime · TCS Digital · TCS Ninja · Service-Based & Product Company SQL Interviews

> **How to use this handbook:** Read top to bottom the first time. On revision, jump straight to **Section 25 (Cheat Sheet)** and **Section 26 (Last-Minute Revision)**. All queries in this handbook run against the sample tables defined in **Section 0** — keep that section open in a second tab while practicing.

---

## 📑 TABLE OF CONTENTS

| # | Section |
|---|---------|
| 0 | Sample Tables & Data (used throughout) |
| 1 | SQL Fundamentals |
| 2 | DDL — Data Definition Language |
| 3 | DML — Data Manipulation Language |
| 4 | DQL — Data Query Language |
| 5 | Operators |
| 6 | Functions (Aggregate, String, Date, Numeric, JSON) |
| 7 | Grouping — GROUP BY, HAVING, ROLLUP, CUBE, GROUPING SETS |
| 8 | Joins |
| 9 | Subqueries |
| 10 | Set Operations |
| 11 | CTE & Recursive CTE |
| 12 | Window Functions |
| 13 | Views |
| 14 | Indexes |
| 15 | Transactions & ACID |
| 16 | Stored Procedures, Functions, Triggers, Cursors |
| 17 | Normalization |
| 18 | Query Optimization |
| 19 | Query Question Bank (Salary, Duplicates, Top-N, Running Totals...) |
| 20 | Output Prediction Questions |
| 21 | Scenario-Based Questions |
| 22 | Tricky SQL Questions (X vs Y) |
| 23 | Most-Asked TCS Interview Questions |
| 24 | Common SQL Errors & Fixes |
| 25 | SQL Cheat Sheet |
| 26 | Last-Minute Revision Lists |

---

# SECTION 0 — SAMPLE TABLES & DATA

> ⚠️ **Every query in this handbook runs on these exact tables.** Interviewers love asking "what if there's a NULL here" or "what if two people tie" — so the sample data is deliberately designed with **duplicates, ties, and NULLs** built in.

## 0.1 Employee

```sql
CREATE TABLE Employee (
    emp_id       INT PRIMARY KEY,
    emp_name     VARCHAR(50),
    dept_id      INT,
    designation  VARCHAR(50),
    salary       DECIMAL(10,2),
    manager_id   INT,
    hire_date    DATE,
    gender       CHAR(1),
    city         VARCHAR(30)
);
```

| emp_id | emp_name | dept_id | designation | salary | manager_id | hire_date | gender | city |
|---|---|---|---|---|---|---|---|---|
| 1 | Aarav Sharma | 10 | Software Engineer | 55000 | 5 | 2019-03-14 | M | Bangalore |
| 2 | Diya Patel | 10 | Software Engineer | 62000 | 5 | 2020-07-01 | F | Bangalore |
| 3 | Rohan Mehta | 20 | Business Analyst | 58000 | 6 | 2018-11-23 | M | Pune |
| 4 | Isha Kapoor | 20 | Business Analyst | 58000 | 6 | 2021-01-15 | F | Pune |
| 5 | Vikram Nair | 10 | Team Lead | 95000 | 8 | 2015-06-10 | M | Bangalore |
| 6 | Ananya Rao | 20 | Team Lead | 90000 | 8 | 2016-04-20 | F | Pune |
| 7 | Karan Singh | 30 | QA Engineer | 48000 | 9 | 2022-02-01 | M | Chennai |
| 8 | Priya Iyer | 10 | Manager | 120000 | NULL | 2012-01-05 | F | Bangalore |
| 9 | Suresh Kumar | 30 | Manager | 115000 | 8 | 2013-09-19 | M | Chennai |
| 10 | Meera Joshi | 40 | HR Executive | 50000 | 8 | 2020-10-30 | F | Mumbai |
| 11 | Arjun Reddy | 30 | QA Engineer | 48000 | 9 | 2022-02-01 | M | Chennai |
| 12 | Neha Verma | NULL | Intern | 25000 | 5 | 2023-06-01 | F | Bangalore |

**Deliberate design notes:** Karan(7) & Arjun(11) tie on salary 48000 → used for RANK vs DENSE_RANK. Rohan(3) & Isha(4) tie on 58000. Priya(8) has `manager_id = NULL` → the CEO / top of hierarchy. Neha(12) has `dept_id = NULL` → used for outer-join / missing-department demos.

## 0.2 Department

```sql
CREATE TABLE Department (
    dept_id     INT PRIMARY KEY,
    dept_name   VARCHAR(50),
    location    VARCHAR(30)
);
```

| dept_id | dept_name | location |
|---|---|---|
| 10 | Engineering | Bangalore |
| 20 | Business | Pune |
| 30 | Quality | Chennai |
| 40 | Human Resources | Mumbai |
| 50 | Finance | Delhi |

**Design note:** dept 50 (Finance) has **zero employees** → used for "departments with no employees" queries.

## 0.3 Student

| student_id | student_name | class | marks | city |
|---|---|---|---|---|
| 101 | Aditi | 10A | 92 | Bangalore |
| 102 | Rahul | 10A | 85 | Pune |
| 103 | Sneha | 10B | 92 | Chennai |
| 104 | Manish | 10B | 76 | Mumbai |
| 105 | Pooja | 10A | NULL | Bangalore |
| 106 | Kunal | 10B | 88 | Delhi |

## 0.4 Customers

| customer_id | customer_name | city | country | signup_date |
|---|---|---|---|---|
| 1 | Global Traders | Mumbai | India | 2018-05-01 |
| 2 | Sunrise Retail | Delhi | India | 2019-02-15 |
| 3 | Ocean Exports | Chennai | India | 2020-08-10 |
| 4 | Metro Mart | Bangalore | India | 2021-01-01 |
| 5 | Nova Enterprises | Pune | India | 2022-03-20 |

**Design note:** Nova Enterprises(5) has **no orders** → used for LEFT JOIN / NOT EXISTS demos.

## 0.5 Orders

| order_id | customer_id | order_date | amount | product_id | status |
|---|---|---|---|---|---|
| 1001 | 1 | 2023-01-10 | 25000 | 501 | Delivered |
| 1002 | 2 | 2023-01-15 | 12000 | 502 | Delivered |
| 1003 | 1 | 2023-02-05 | 8000 | 503 | Cancelled |
| 1004 | 3 | 2023-02-20 | 45000 | 501 | Delivered |
| 1005 | 2 | 2023-03-01 | 6000 | 504 | Pending |
| 1006 | 4 | 2023-03-15 | 15000 | 502 | Delivered |
| 1007 | 1 | 2023-04-01 | 30000 | 505 | Delivered |

## 0.6 Products

| product_id | product_name | category | price |
|---|---|---|---|
| 501 | Laptop | Electronics | 55000 |
| 502 | Office Chair | Furniture | 8000 |
| 503 | Wireless Mouse | Electronics | 800 |
| 504 | Notebook | Stationery | 50 |
| 505 | Monitor | Electronics | 12000 |

## 0.7 Sales

| sale_id | product_id | sale_date | quantity | amount | region |
|---|---|---|---|---|---|
| 1 | 501 | 2023-01-05 | 2 | 110000 | North |
| 2 | 502 | 2023-01-10 | 5 | 40000 | South |
| 3 | 501 | 2023-02-01 | 1 | 55000 | North |
| 4 | 503 | 2023-02-15 | 10 | 8000 | East |
| 5 | 501 | 2023-03-01 | 3 | 165000 | West |
| 6 | 504 | 2023-03-10 | 20 | 1000 | South |

## 0.8 Movies & Actors

**Movies**

| movie_id | title | genre | release_year | rating |
|---|---|---|---|---|
| 1 | Inception | Sci-Fi | 2010 | 8.8 |
| 2 | The Dark Knight | Action | 2008 | 9.0 |
| 3 | Interstellar | Sci-Fi | 2014 | 8.6 |
| 4 | Dunkirk | War | 2017 | 7.9 |
| 5 | Tenet | Sci-Fi | 2020 | 7.5 |

**Actors**

| actor_id | actor_name | movie_id | role |
|---|---|---|---|
| 1 | Actor A (Lead1) | 1 | Cobb |
| 2 | Actor B (Lead2) | 2 | Batman |
| 3 | Actor C (Lead3) | 3 | Cooper |
| 4 | Actor D (Lead4) | 4 | Commander |
| 5 | Actor E (Lead5) | 5 | Protagonist |
| 6 | Actor D (Lead4) | 5 | Neil |

**Design note:** Actor D appears in **two movies** (movie 4 and 5) → used for "actor with most movies" queries.

## 0.9 Bank (Accounts) & Transactions

**Bank**

| account_id | customer_id | account_type | balance | branch |
|---|---|---|---|---|
| A001 | 1 | Savings | 55000 | Mumbai Branch |
| A002 | 2 | Current | 120000 | Delhi Branch |
| A003 | 3 | Savings | 8000 | Chennai Branch |
| A004 | 1 | Current | 250000 | Mumbai Branch |

**Transactions**

| txn_id | account_id | txn_date | txn_type | amount |
|---|---|---|---|---|
| T1 | A001 | 2023-01-05 | Deposit | 20000 |
| T2 | A001 | 2023-01-10 | Withdrawal | 5000 |
| T3 | A002 | 2023-01-12 | Deposit | 50000 |
| T4 | A003 | 2023-02-01 | Deposit | 8000 |
| T5 | A001 | 2023-02-05 | Deposit | 15000 |
| T6 | A004 | 2023-02-10 | Withdrawal | 20000 |

## 0.10 Salary (Monthly Payroll)

| emp_id | month | basic | hra | bonus | total |
|---|---|---|---|---|---|
| 1 | 2023-01 | 45000 | 8000 | 2000 | 55000 |
| 1 | 2023-02 | 45000 | 8000 | 2000 | 55000 |
| 2 | 2023-01 | 50000 | 9000 | 3000 | 62000 |
| 5 | 2023-01 | 75000 | 15000 | 5000 | 95000 |

## 0.11 Attendance

| emp_id | attend_date | status |
|---|---|---|
| 1 | 2023-01-02 | Present |
| 1 | 2023-01-03 | Absent |
| 2 | 2023-01-02 | Present |
| 2 | 2023-01-03 | Present |
| 7 | 2023-01-02 | Present |
| 7 | 2023-01-03 | Present |
| 7 | 2023-01-04 | Present |

**Design note:** emp 7 has **3 consecutive Present days** → used for "streak" queries.

## 0.12 Hospital (Doctors & Patients)

**Doctors**

| doctor_id | doctor_name | specialization |
|---|---|---|
| D1 | Dr. Anil | Cardiology |
| D2 | Dr. Sunita | Neurology |
| D3 | Dr. Vivek | Orthopedics |

**Patients**

| patient_id | patient_name | disease | doctor_id | admit_date | discharge_date |
|---|---|---|---|---|---|
| P1 | Ramesh | Heart Disease | D1 | 2023-01-01 | 2023-01-10 |
| P2 | Sita | Migraine | D2 | 2023-02-01 | 2023-02-03 |
| P3 | Geeta | Fracture | D3 | 2023-03-01 | 2023-03-15 |
| P4 | Manoj | Heart Disease | D1 | 2023-04-01 | NULL |

**Design note:** P4 has `discharge_date = NULL` → still admitted, used for NULL-handling demos.

## 0.13 Library

| book_id | book_title | author | issued_to | issue_date | return_date |
|---|---|---|---|---|---|
| B1 | Wings of Fire | Kalam | Ravi | 2023-01-01 | 2023-01-15 |
| B2 | Sapiens | Harari | Meera | 2023-01-05 | NULL |
| B3 | Atomic Habits | Clear | Ravi | 2023-02-01 | 2023-02-20 |
| B4 | 1984 | Orwell | Meera | 2023-02-10 | 2023-02-25 |

## 0.14 Company & Project

**Company**

| company_id | company_name | industry | revenue_cr |
|---|---|---|---|
| C1 | TCS | IT Services | 250000 |
| C2 | Infosys | IT Services | 180000 |
| C3 | Wipro | IT Services | 90000 |

**Project**

| project_id | project_name | emp_id | start_date | end_date | budget |
|---|---|---|---|---|---|
| PR1 | Banking Migration | 1 | 2023-01-01 | 2023-06-30 | 500000 |
| PR2 | Retail Analytics | 3 | 2023-02-01 | 2023-08-31 | 350000 |
| PR3 | Banking Migration | 2 | 2023-01-15 | 2023-06-30 | 500000 |
| PR4 | HR Portal | 10 | 2023-03-01 | 2023-05-30 | 100000 |

## 0.15 Manager (derived from Employee)

> 📝 **Interview tip:** Most real schemas do **not** keep a separate `Manager` table — a manager is just an `Employee` row referenced by another employee's `manager_id` (a **self-referencing foreign key**). If an interviewer says "assume a Manager table", you can create it as a view:

```sql
CREATE VIEW Manager AS
SELECT DISTINCT m.emp_id, m.emp_name, m.designation, m.dept_id
FROM Employee e
JOIN Employee m ON e.manager_id = m.emp_id;
```

## 0.16 City & Country

**Country**

| country_id | country_name | continent |
|---|---|---|
| CN1 | India | Asia |
| CN2 | USA | North America |

**City**

| city_id | city_name | state | country_id |
|---|---|---|---|
| CT1 | Mumbai | Maharashtra | CN1 |
| CT2 | Bangalore | Karnataka | CN1 |
| CT3 | Pune | Maharashtra | CN1 |
| CT4 | Chennai | Tamil Nadu | CN1 |

---

# SECTION 1 — SQL FUNDAMENTALS

## 1.1 What is SQL?

**Definition:** SQL (Structured Query Language) is a **declarative** language used to store, retrieve, manipulate, and manage data in a relational database. "Declarative" means you tell SQL *what* data you want, not *how* to fetch it — the database engine decides the "how" via its query optimizer.

**Why it's used:** It's the universal interface between applications and relational data — almost every backend, from a college ERP to a bank's core system, talks to its database in SQL.

**History (quick):** Developed at IBM in the early 1970s (originally SEQUEL) for System R, standardized by ANSI in 1986 and ISO in 1987. Current standard: SQL:2016 / SQL:2023, which added JSON and property-graph query features.

## 1.2 Database vs DBMS vs RDBMS

| Term | Meaning | Example |
|---|---|---|
| **Database** | An organized collection of data | An `employees.db` file |
| **DBMS** | Software that manages databases (may or may not be relational) | MongoDB, Redis, MySQL |
| **RDBMS** | DBMS based on the **relational model** — data stored in tables with rows/columns, relationships via keys | MySQL, PostgreSQL, Oracle, SQL Server |

> 💡 **Interview tip:** If asked "difference between DBMS and RDBMS", the #1 answer they want is: **RDBMS enforces relationships via keys and supports normalization/ACID; plain DBMS (like a flat file system) does not.**

## 1.3 SQL Architecture — How SQL Works Internally

```
 Client (App / SSMS / psql)
        │  SQL query sent over network
        ▼
 ┌───────────────────────────────┐
 │        Query Processor        │
 │  1. Parser (syntax check)     │
 │  2. Binder (semantic check —  │
 │     do tables/columns exist?) │
 │  3. Optimizer (choose the     │
 │     cheapest execution plan)  │
 └───────────────────────────────┘
        ▼
 ┌───────────────────────────────┐
 │      Execution Engine         │
 │  Reads/writes via Storage     │
 │  Engine, uses Buffer/Cache    │
 └───────────────────────────────┘
        ▼
 ┌───────────────────────────────┐
 │   Storage Engine (Disk/SSD)   │
 │   Tables, Indexes, Logs       │
 └───────────────────────────────┘
        ▼
      Result Set → back to Client
```

**Step-by-step:** Parser checks grammar → Binder resolves object names and types → Optimizer generates multiple candidate execution plans and picks the lowest-cost one using table statistics → Execution engine runs the plan, pulling pages through the buffer pool → Result set streamed back to the client.

## 1.4 SQL Standards & Dialects

| Database | Dialect Name | Notable Differences |
|---|---|---|
| MySQL | — | `LIMIT`, `IFNULL()`, backticks for identifiers, weaker window function support pre-8.0 |
| PostgreSQL | — | `LIMIT`/`OFFSET`, `ILIKE`, very rich window/JSON support, strictest standards compliance |
| SQL Server | T-SQL | `TOP`, `ISNULL()`, square brackets `[ ]` for identifiers, `IDENTITY` |
| Oracle | PL/SQL | `ROWNUM`/`FETCH FIRST`, `NVL()`, sequences instead of auto-increment |

> 📝 **TCS interviews are usually Oracle or MySQL-flavored.** Learn `NVL` (Oracle) *and* `IFNULL`/`COALESCE` (portable) — interviewers like to see you know the **portable, ANSI-standard option** even if you mention the vendor-specific one.

## 1.5 SQL Query Processing Order (⭐ Extremely frequently asked)

SQL is **written** in this order:
```
SELECT → FROM → JOIN → WHERE → GROUP BY → HAVING → ORDER BY → LIMIT
```

But it is **logically executed** in this order:

```
1. FROM         (identify base tables)
2. JOIN         (combine tables)
3. WHERE        (filter rows BEFORE grouping)
4. GROUP BY     (form groups)
5. HAVING       (filter groups AFTER grouping)
6. SELECT       (compute expressions, aliases)
7. DISTINCT     (remove duplicate rows)
8. ORDER BY     (sort)
9. LIMIT/OFFSET (paginate)
```

> ⚠️ **This single fact explains at least 10 different "tricky" interview questions** — why you can't use a `SELECT` alias in `WHERE`, why `WHERE` can't filter on aggregates, why `HAVING` can, etc. Memorize this order cold.

**Common mistake:** Writing `WHERE COUNT(*) > 1` — fails, because `WHERE` runs before aggregation exists. Must use `HAVING COUNT(*) > 1`.

## 1.6 Execution Plan

**Definition:** A tree of operations (scans, joins, sorts) the optimizer decided is cheapest to run your query.

```sql
EXPLAIN SELECT * FROM Employee WHERE dept_id = 10;         -- MySQL / PostgreSQL
EXPLAIN PLAN FOR SELECT * FROM Employee WHERE dept_id = 10; -- Oracle
```

Look for: **Seq Scan / Full Table Scan** (bad on large tables) vs **Index Scan / Index Seek** (good), estimated rows, and cost.

---

# SECTION 2 — DDL (Data Definition Language)

DDL statements define/modify the **structure** of database objects. They are **auto-committed** in most RDBMS (you cannot roll them back inside an ordinary transaction in MySQL, though Postgres allows transactional DDL).

## 2.1 CREATE

```sql
CREATE TABLE Department (
    dept_id   INT PRIMARY KEY,
    dept_name VARCHAR(50) NOT NULL,
    location  VARCHAR(30)
);
```

## 2.2 ALTER

```sql
ALTER TABLE Employee ADD COLUMN email VARCHAR(100);          -- add column
ALTER TABLE Employee DROP COLUMN email;                       -- drop column
ALTER TABLE Employee MODIFY COLUMN salary DECIMAL(12,2);      -- MySQL/Oracle: change type
ALTER TABLE Employee ALTER COLUMN salary TYPE NUMERIC(12,2);  -- PostgreSQL
ALTER TABLE Employee RENAME COLUMN emp_name TO full_name;
```

## 2.3 DROP vs TRUNCATE vs DELETE (⭐ #1 most-asked comparison)

| Aspect | DROP | TRUNCATE | DELETE |
|---|---|---|---|
| Type | DDL | DDL | DML |
| Removes | Entire table structure + data | All rows, keeps structure | Rows (optionally filtered by WHERE) |
| WHERE clause | ❌ No | ❌ No | ✅ Yes |
| Rollback | ❌ No (auto-commit) | ❌ Usually no (some DBs allow within a txn) | ✅ Yes |
| Triggers fired | No | No | Yes |
| Resets identity/auto-increment | N/A | ✅ Yes | ❌ No |
| Speed | Fast | Very fast (deallocates pages) | Slow (row-by-row, logged) |

> 🎯 **Interview one-liner:** *"DELETE is DML, logs each row, and can be rolled back; TRUNCATE is DDL, deallocates the whole data page at once and resets identity; DROP removes the table definition itself."*

## 2.4 RENAME

```sql
RENAME TABLE Employee TO Staff;              -- MySQL
ALTER TABLE Employee RENAME TO Staff;        -- PostgreSQL / Oracle
```

## 2.5 Constraints

| Constraint | Purpose | Example |
|---|---|---|
| `NOT NULL` | Column cannot store NULL | `salary DECIMAL NOT NULL` |
| `UNIQUE` | No duplicate values allowed | `email VARCHAR(100) UNIQUE` |
| `PRIMARY KEY` | Uniquely identifies a row = `UNIQUE + NOT NULL` | `emp_id INT PRIMARY KEY` |
| `FOREIGN KEY` | Enforces referential integrity to another table | `dept_id INT REFERENCES Department(dept_id)` |
| `CHECK` | Enforces a boolean condition | `CHECK (salary > 0)` |
| `DEFAULT` | Supplies a value when none is given | `status VARCHAR(20) DEFAULT 'Pending'` |
| `AUTO_INCREMENT` (MySQL) / `IDENTITY` (SQL Server) / `SERIAL` (Postgres) / sequence (Oracle) | Auto-generates surrogate keys | `emp_id INT AUTO_INCREMENT` |

```sql
CREATE TABLE Employee (
    emp_id     INT PRIMARY KEY AUTO_INCREMENT,
    emp_name   VARCHAR(50) NOT NULL,
    dept_id    INT,
    salary     DECIMAL(10,2) CHECK (salary > 0),
    status     VARCHAR(20) DEFAULT 'Active',
    email      VARCHAR(100) UNIQUE,
    FOREIGN KEY (dept_id) REFERENCES Department(dept_id)
);
```

## 2.6 Key Types (⭐ frequently confused)

| Key | Meaning |
|---|---|
| **Super Key** | Any column (or set of columns) that can uniquely identify a row — may have extra, unnecessary columns |
| **Candidate Key** | A *minimal* super key — no redundant column can be removed. A table can have multiple candidate keys |
| **Primary Key** | The candidate key **chosen** to be the main identifier |
| **Alternate Key** | Candidate key(s) **not** chosen as primary key |
| **Composite Key** | A primary key made of **2+ columns together** (e.g., `(student_id, subject_id)` in a marks table) |

**Real example:** In `Employee`, both `emp_id` and `email` can uniquely identify a row → both are **candidate keys**. We pick `emp_id` as **primary key**, so `email` becomes an **alternate key**.

> 📝 **Interview tip:** They love asking *"Can a table have more than one primary key?"* — Answer: **No, only one**, but it can be a **composite** primary key spanning multiple columns.

---

# SECTION 3 — DML (Data Manipulation Language)

## 3.1 INSERT

```sql
-- Single row
INSERT INTO Employee (emp_id, emp_name, dept_id, salary, manager_id, hire_date, gender, city)
VALUES (13, 'Farhan Khan', 10, 60000, 5, '2023-07-01', 'M', 'Bangalore');

-- Multiple rows in one statement (bulk insert)
INSERT INTO Employee (emp_id, emp_name, dept_id, salary, manager_id, hire_date, gender, city)
VALUES
  (14, 'Sana Ali', 20, 61000, 6, '2023-07-05', 'F', 'Pune'),
  (15, 'Devansh Rao', 30, 47000, 9, '2023-07-10', 'M', 'Chennai');

-- Insert from another table (INSERT ... SELECT)
INSERT INTO Manager_Backup (emp_id, emp_name)
SELECT emp_id, emp_name FROM Employee WHERE designation = 'Manager';
```

**Why bulk insert matters:** A single multi-row `INSERT` is **much faster** than N separate `INSERT` statements, because it parses/plans/commits once instead of N times.

## 3.2 UPDATE

```sql
UPDATE Employee
SET salary = salary * 1.10
WHERE dept_id = 10;
```

> ⚠️ **Common mistake:** Forgetting the `WHERE` clause updates **every row** in the table. Always run the equivalent `SELECT` with the same `WHERE` first to confirm the row count.

## 3.3 DELETE

```sql
DELETE FROM Employee WHERE emp_id = 15;
```

## 3.4 MERGE / UPSERT (⭐ frequently asked in product-company rounds)

**Definition:** MERGE combines INSERT + UPDATE (and optionally DELETE) into a single atomic statement based on whether a matching row exists — commonly called "UPSERT".

```sql
-- Standard SQL / Oracle / SQL Server style
MERGE INTO Employee AS tgt
USING Staging_Employee AS src
ON tgt.emp_id = src.emp_id
WHEN MATCHED THEN
    UPDATE SET tgt.salary = src.salary
WHEN NOT MATCHED THEN
    INSERT (emp_id, emp_name, dept_id, salary)
    VALUES (src.emp_id, src.emp_name, src.dept_id, src.salary);
```

```sql
-- PostgreSQL / MySQL style upsert
INSERT INTO Employee (emp_id, emp_name, salary)
VALUES (1, 'Aarav Sharma', 60000)
ON CONFLICT (emp_id)                 -- PostgreSQL
DO UPDATE SET salary = EXCLUDED.salary;

INSERT INTO Employee (emp_id, emp_name, salary)
VALUES (1, 'Aarav Sharma', 60000)
ON DUPLICATE KEY UPDATE salary = VALUES(salary);  -- MySQL
```

## 3.5 RETURNING (PostgreSQL / Oracle)

```sql
DELETE FROM Employee WHERE emp_id = 15 RETURNING emp_id, emp_name;
UPDATE Employee SET salary = salary * 1.1 WHERE dept_id = 10 RETURNING emp_id, salary;
```
Returns the affected rows without a separate `SELECT` — useful in application code to confirm what changed.

## 3.6 DML Interview Questions

**Q1: What happens if you run `UPDATE` without `WHERE`?**
Every row in the table gets updated — a very common production incident.

**Q2: Difference between `INSERT INTO ... VALUES` and `INSERT INTO ... SELECT`?**
The first inserts literal values; the second inserts the result set of a query (copying/transforming data from another table).

**Q3: Is DML auto-committed?**
No (except in MySQL with autocommit=1 by default) — DML changes are only permanent after `COMMIT` in a transactional context.

---

# SECTION 4 — DQL (Data Query Language)

## 4.1 Basic SELECT

```sql
SELECT emp_name, salary FROM Employee WHERE dept_id = 10 ORDER BY salary DESC;
```

## 4.2 DISTINCT

```sql
SELECT DISTINCT dept_id FROM Employee;
```
**Output:** `10, 20, 30, 40, NULL` (NULL is treated as one distinct value in DISTINCT/GROUP BY — a classic trick question).

## 4.3 ORDER BY

```sql
SELECT emp_name, salary FROM Employee ORDER BY salary DESC, emp_name ASC;
```
Sorts by salary descending; ties broken alphabetically by name. **NULLs sort last by default in MySQL/SQL Server ASC order, but first in Oracle/PostgreSQL ASC order** — a genuine cross-database trap. Use `NULLS LAST` / `NULLS FIRST` explicitly (PostgreSQL/Oracle) when it matters.

## 4.4 LIMIT / OFFSET / TOP / FETCH (pagination — dialect differences)

| Goal | MySQL/Postgres | SQL Server | Oracle 12c+ |
|---|---|---|---|
| Top 3 rows | `LIMIT 3` | `TOP 3` (in SELECT) | `FETCH FIRST 3 ROWS ONLY` |
| Skip 5, take 3 | `LIMIT 3 OFFSET 5` | `OFFSET 5 ROWS FETCH NEXT 3 ROWS ONLY` | `OFFSET 5 ROWS FETCH NEXT 3 ROWS ONLY` |

```sql
-- Top 3 highest paid employees (MySQL/Postgres)
SELECT emp_name, salary FROM Employee ORDER BY salary DESC LIMIT 3;
```

## 4.5 Aliases

```sql
SELECT emp_name AS "Employee Name", salary * 12 AS annual_salary
FROM Employee;
```
> ⚠️ **Trap:** You **cannot** use a `SELECT` alias inside the `WHERE` clause of the same query (WHERE executes before SELECT — see Section 1.5). You **can** use it in `ORDER BY` because ORDER BY runs after SELECT.

## 4.6 CASE Expression

```sql
SELECT emp_name, salary,
  CASE
    WHEN salary >= 90000 THEN 'Senior'
    WHEN salary >= 55000 THEN 'Mid'
    ELSE 'Junior'
  END AS band
FROM Employee;
```

## 4.7 NULL-Handling Functions (⭐ heavily asked, dialect-specific)

| Function | Available In | Behavior |
|---|---|---|
| `COALESCE(a, b, c, ...)` | ANSI standard, all DBs | Returns first non-NULL value from the list |
| `IFNULL(a, b)` | MySQL | Returns `b` if `a` is NULL (2-argument only) |
| `NVL(a, b)` | Oracle | Same as IFNULL, Oracle syntax |
| `ISNULL(a, b)` | SQL Server | Same idea (careful: also a *test* function in MySQL, `ISNULL(x)` returns boolean there!) |
| `NULLIF(a, b)` | ANSI standard | Returns NULL if `a = b`, else returns `a` — used to avoid divide-by-zero |

```sql
SELECT emp_name, COALESCE(manager_id, 0) AS manager_or_zero FROM Employee;

-- NULLIF avoiding divide by zero
SELECT emp_name, salary / NULLIF(bonus, 0) AS ratio FROM Employee_Bonus;
```

> 🎯 **Tricky Q:** *"IFNULL vs ISNULL vs COALESCE — which should you use in a portable script?"* → **COALESCE**, because it's ANSI standard and works identically across MySQL, PostgreSQL, SQL Server, and Oracle; the others are vendor-specific.

---

# SECTION 5 — OPERATORS

## 5.1 Comparison & Logical

`=, !=/<>, >, <, >=, <=, AND, OR, NOT`

## 5.2 IN / NOT IN

```sql
SELECT emp_name FROM Employee WHERE dept_id IN (10, 30);
SELECT emp_name FROM Employee WHERE dept_id NOT IN (10, 30);
```
> ⚠️ **Classic trap:** `NOT IN` with a subquery that can return **NULL** silently returns **zero rows** for the whole query (because `x <> NULL` is UNKNOWN, not TRUE, for every comparison). Covered in depth in Section 22 (Tricky Questions).

## 5.3 LIKE / ILIKE & Wildcards

```sql
SELECT emp_name FROM Employee WHERE emp_name LIKE 'A%';   -- starts with A
SELECT emp_name FROM Employee WHERE emp_name LIKE '%a';   -- ends with a
SELECT emp_name FROM Employee WHERE emp_name LIKE '_o%';  -- 2nd letter is 'o'
SELECT * FROM Customers WHERE customer_name ILIKE 'global%'; -- PostgreSQL: case-insensitive LIKE
```
`%` = any number of characters, `_` = exactly one character.

## 5.4 BETWEEN

```sql
SELECT emp_name, salary FROM Employee WHERE salary BETWEEN 50000 AND 90000;
```
**Inclusive** on both ends (equivalent to `salary >= 50000 AND salary <= 90000`).

## 5.5 ANY / ALL

```sql
-- Employees earning more than ANY (i.e., at least one) employee in dept 30
SELECT emp_name, salary FROM Employee
WHERE salary > ANY (SELECT salary FROM Employee WHERE dept_id = 30);

-- Employees earning more than ALL employees in dept 30 (i.e., more than the max)
SELECT emp_name, salary FROM Employee
WHERE salary > ALL (SELECT salary FROM Employee WHERE dept_id = 30);
```
`> ANY` ≈ greater than the **minimum** of the list. `> ALL` ≈ greater than the **maximum** of the list.

## 5.6 EXISTS / NOT EXISTS

```sql
-- Customers who have placed at least one order
SELECT c.customer_name FROM Customers c
WHERE EXISTS (SELECT 1 FROM Orders o WHERE o.customer_id = c.customer_id);

-- Customers with NO orders (Nova Enterprises)
SELECT c.customer_name FROM Customers c
WHERE NOT EXISTS (SELECT 1 FROM Orders o WHERE o.customer_id = c.customer_id);
```
`EXISTS` stops scanning as soon as it finds **one** matching row — often faster than `IN` for large correlated checks, and (unlike `NOT IN`) is **NULL-safe**.

## 5.7 IS NULL / IS NOT NULL

```sql
SELECT emp_name FROM Employee WHERE manager_id IS NULL;   -- Priya Iyer (the CEO)
SELECT emp_name FROM Employee WHERE dept_id IS NOT NULL;
```
> ⚠️ `salary = NULL` **never** returns TRUE — you must use `IS NULL`. NULL represents "unknown", and unknown = unknown is still unknown, not true.

## 5.8 Regular Expressions

```sql
SELECT emp_name FROM Employee WHERE emp_name REGEXP '^[AD]';   -- MySQL: starts with A or D
SELECT emp_name FROM Employee WHERE emp_name ~ '^[AD]';        -- PostgreSQL
```

---

# SECTION 6 — FUNCTIONS

## 6.1 Aggregate Functions

| Function | Purpose | Ignores NULL? |
|---|---|---|
| `COUNT(*)` | Counts **all rows** including NULLs | No |
| `COUNT(column)` | Counts **non-NULL** values in that column | Yes |
| `SUM(column)` | Total | Yes |
| `AVG(column)` | Average | Yes (divides by non-NULL count only) |
| `MAX(column)` / `MIN(column)` | Highest/lowest value | Yes |

```sql
SELECT COUNT(*) AS total_students, COUNT(marks) AS students_with_marks
FROM Student;
-- Output: total_students = 6, students_with_marks = 5 (Pooja's NULL marks excluded)
```

> 🎯 **Interview classic:** *"COUNT(*) vs COUNT(column) vs COUNT(1)?"* → `COUNT(*)` counts rows regardless of NULLs; `COUNT(column)` skips NULLs in that column; `COUNT(1)` behaves identically to `COUNT(*)` (counts rows) — the `1` is just a constant per row, and modern optimizers treat both the same, so there's **no real performance difference** in any modern engine.

## 6.2 String Functions

```sql
SELECT UPPER(emp_name), LOWER(emp_name) FROM Employee;
SELECT LENGTH(emp_name) FROM Employee;              -- MySQL/Postgres (LEN in SQL Server)
SELECT CONCAT(emp_name, ' - ', designation) FROM Employee;
SELECT SUBSTRING(emp_name, 1, 3) FROM Employee;     -- first 3 chars
SELECT TRIM('  Aarav  ');                            -- removes leading/trailing spaces
SELECT REPLACE(emp_name, 'Sharma', 'Verma') FROM Employee;
SELECT LEFT(emp_name, 3), RIGHT(emp_name, 3) FROM Employee;  -- MySQL/SQL Server
```

## 6.3 Numeric Functions

```sql
SELECT ROUND(58333.333, 2);   -- 58333.33
SELECT CEIL(58333.1), FLOOR(58333.9);   -- 58334, 58333
SELECT ABS(-500);             -- 500
SELECT MOD(10, 3);            -- 1  (or 10 % 3)
SELECT POWER(2, 10);          -- 1024
```

## 6.4 Date Functions

```sql
SELECT NOW();                                    -- current date+time (MySQL/Postgres)
SELECT SYSDATE FROM DUAL;                        -- Oracle
SELECT GETDATE();                                -- SQL Server

SELECT DATEDIFF(day, '2023-01-01', '2023-06-30');        -- SQL Server: days between
SELECT DATEDIFF('2023-06-30', '2023-01-01');              -- MySQL: days between
SELECT ('2023-06-30'::date - '2023-01-01'::date);         -- PostgreSQL

SELECT DATE_ADD(hire_date, INTERVAL 1 YEAR) FROM Employee;  -- MySQL
SELECT hire_date + INTERVAL '1 year' FROM Employee;          -- PostgreSQL

SELECT EXTRACT(YEAR FROM hire_date) AS join_year FROM Employee;
SELECT MONTHNAME(hire_date), DAYNAME(hire_date) FROM Employee; -- MySQL
```

**Real example — employee age & tenure:**
```sql
SELECT emp_name,
       TIMESTAMPDIFF(YEAR, hire_date, CURDATE()) AS years_of_service   -- MySQL
FROM Employee;
```

## 6.5 Conversion / Formatting Functions

```sql
SELECT CAST(salary AS VARCHAR(20)) FROM Employee;
SELECT CONVERT(VARCHAR, salary) FROM Employee;          -- SQL Server
SELECT TO_CHAR(hire_date, 'DD-MON-YYYY') FROM Employee; -- Oracle/Postgres
SELECT FORMAT(salary, 2) FROM Employee;                  -- SQL Server: 55,000.00
```

## 6.6 JSON Functions (modern SQL, product-company favorite)

```sql
-- PostgreSQL
SELECT data->>'name' AS name FROM Orders_Json;
SELECT jsonb_build_object('id', order_id, 'amount', amount) FROM Orders;

-- MySQL
SELECT JSON_EXTRACT(data, '$.name') FROM Orders_Json;
SELECT JSON_OBJECT('id', order_id, 'amount', amount) FROM Orders;
```

## 6.7 Window / Ranking Functions — *previewed here, full depth in Section 12*

```sql
SELECT emp_name, salary,
       RANK() OVER (ORDER BY salary DESC) AS rnk
FROM Employee;
```

> 📝 **Interview tip:** If asked to name function *categories*, list them in this order: **Aggregate → Scalar (string/numeric/date) → Conversion → NULL-handling → Window/Ranking → JSON**. Interviewers are checking breadth as much as depth.

---

# SECTION 7 — GROUPING: GROUP BY, HAVING, ROLLUP, CUBE, GROUPING SETS

## 7.1 GROUP BY

**Definition:** Collapses multiple rows sharing the same value(s) into a single summary row, typically paired with aggregate functions.

```sql
SELECT dept_id, COUNT(*) AS emp_count, AVG(salary) AS avg_salary
FROM Employee
GROUP BY dept_id;
```

**Output:**
| dept_id | emp_count | avg_salary |
|---|---|---|
| 10 | 4 | 83000 |
| 20 | 2 | 58000 |
| 30 | 3 | 70333.33 |
| 40 | 1 | 50000 |
| NULL | 1 | 25000 |

**Rule:** Every non-aggregated column in `SELECT` **must** appear in `GROUP BY` (ANSI standard; MySQL is lenient about this by default but it's still bad practice).

## 7.2 HAVING vs WHERE (⭐ top interview trap)

```sql
-- Departments with more than 2 employees
SELECT dept_id, COUNT(*) AS emp_count
FROM Employee
GROUP BY dept_id
HAVING COUNT(*) > 2;
```

| | WHERE | HAVING |
|---|---|---|
| Filters | Individual rows | Groups (after aggregation) |
| Runs | Before GROUP BY | After GROUP BY |
| Can use aggregate functions? | ❌ No | ✅ Yes |

## 7.3 ROLLUP

**Definition:** Produces subtotal rows plus a grand total, in a hierarchical fashion (left to right).

```sql
SELECT dept_id, designation, SUM(salary) AS total_salary
FROM Employee
GROUP BY ROLLUP(dept_id, designation);
```
Produces: one row per `(dept_id, designation)`, then a subtotal per `dept_id` (designation = NULL), then a grand total (both NULL).

## 7.4 CUBE

**Definition:** Like ROLLUP, but generates subtotals for **every possible combination** of the grouping columns, not just the hierarchical ones.

```sql
SELECT dept_id, designation, SUM(salary) AS total_salary
FROM Employee
GROUP BY CUBE(dept_id, designation);
```
Adds subtotals by `designation` alone too (which ROLLUP would not).

## 7.5 GROUPING SETS

**Definition:** Lets you specify **exactly** which grouping combinations you want, instead of the full hierarchy (ROLLUP) or all combinations (CUBE).

```sql
SELECT dept_id, designation, SUM(salary) AS total_salary
FROM Employee
GROUP BY GROUPING SETS ((dept_id), (designation), ());
```

> 📝 **Interview tip:** `ROLLUP(a,b) ⊂ CUBE(a,b) ⊂ arbitrary GROUPING SETS`. If asked "which is most flexible?" → **GROUPING SETS**, because ROLLUP and CUBE are really just shorthand for common GROUPING SETS patterns.

**Common mistake:** Confusing which column becomes `NULL` for a subtotal row vs. an actual NULL value in the data. Use `GROUPING(column)` function to disambiguate — it returns 1 if the NULL is a subtotal marker, 0 if it's a genuine data NULL.

---

# SECTION 8 — JOINS ⭐ (the single most-asked SQL topic in TCS interviews)

## 8.1 Visual Overview

```
   Employee (E)              Department (D)
   ┌─────────────┐           ┌─────────────┐
   │  dept_id=10 │◄─────────►│  dept_id=10 │   ← matches on both sides
   │  dept_id=20 │◄─────────►│  dept_id=20 │
   │  dept_id=30 │◄─────────►│  dept_id=30 │
   │  dept_id=40 │◄─────────►│  dept_id=40 │
   │  dept_id=NULL (Neha)    │  dept_id=50 (Finance, no employees)
   └─────────────┘           └─────────────┘

  INNER JOIN   →  only rows that match on both sides           (10,20,30,40)
  LEFT JOIN    →  all Employee rows + matches (unmatched → NULL Dept cols) (+ Neha)
  RIGHT JOIN   →  all Department rows + matches                (+ Finance/dept 50)
  FULL JOIN    →  all rows from both sides                      (+ Neha + Finance)
```

## 8.2 INNER JOIN

```sql
SELECT e.emp_name, d.dept_name
FROM Employee e
INNER JOIN Department d ON e.dept_id = d.dept_id;
```
**Output:** 11 rows (all employees **except** Neha, whose `dept_id` is NULL and matches nothing).

## 8.3 LEFT (OUTER) JOIN

```sql
SELECT e.emp_name, d.dept_name
FROM Employee e
LEFT JOIN Department d ON e.dept_id = d.dept_id;
```
**Output:** All 12 employees; Neha's row shows `dept_name = NULL`.

**Real use case:** "List all customers and their orders, including customers who never ordered."
```sql
SELECT c.customer_name, o.order_id, o.amount
FROM Customers c
LEFT JOIN Orders o ON c.customer_id = o.customer_id;
```
Nova Enterprises appears with `order_id = NULL`.

## 8.4 RIGHT (OUTER) JOIN

```sql
SELECT e.emp_name, d.dept_name
FROM Employee e
RIGHT JOIN Department d ON e.dept_id = d.dept_id;
```
**Output:** All 5 departments; Finance (50) shows `emp_name = NULL` (no employees).

> 📝 **Interview tip:** `RIGHT JOIN` is rarely used in practice because `A RIGHT JOIN B` = `B LEFT JOIN A` — most style guides ban RIGHT JOIN for readability. Know it, but prefer LEFT JOIN by flipping table order.

## 8.5 FULL (OUTER) JOIN

```sql
SELECT e.emp_name, d.dept_name
FROM Employee e
FULL JOIN Department d ON e.dept_id = d.dept_id;
```
**Output:** All employees + all departments; Neha (NULL dept) and Finance (NULL employee) both appear.

> ⚠️ **MySQL does not support `FULL JOIN` natively.** Emulate it with `UNION`:
```sql
SELECT e.emp_name, d.dept_name FROM Employee e LEFT JOIN Department d ON e.dept_id = d.dept_id
UNION
SELECT e.emp_name, d.dept_name FROM Employee e RIGHT JOIN Department d ON e.dept_id = d.dept_id;
```

## 8.6 CROSS JOIN

**Definition:** Cartesian product — every row of table A paired with every row of table B. No `ON` clause.

```sql
SELECT e.emp_name, p.product_name
FROM Employee e CROSS JOIN Products p;
-- 12 employees × 5 products = 60 rows
```

**Real use case:** Generating all possible (employee, month) combos for an attendance calendar.

## 8.7 SELF JOIN (⭐ extremely common — Manager hierarchy)

```sql
SELECT e.emp_name AS employee, m.emp_name AS manager
FROM Employee e
LEFT JOIN Employee m ON e.manager_id = m.emp_id;
```
**Output (sample):**
| employee | manager |
|---|---|
| Aarav Sharma | Vikram Nair |
| Vikram Nair | Priya Iyer |
| Priya Iyer | NULL |

**Why `LEFT JOIN` and not `INNER JOIN`?** Priya Iyer has `manager_id = NULL`; an INNER JOIN would drop her row entirely, but we still want to see her as "no manager" (CEO).

## 8.8 NATURAL JOIN

```sql
SELECT * FROM Employee NATURAL JOIN Department;
```
Automatically joins on **all** identically-named columns. **Interview tip:** Almost never used in production — if both tables happen to share an unrelated column name (e.g., both have `updated_at`), you silently get wrong results. Always prefer explicit `ON`.

## 8.9 EQUI JOIN vs NON-EQUI JOIN

```sql
-- Equi Join: uses "="
SELECT e.emp_name, d.dept_name FROM Employee e JOIN Department d ON e.dept_id = d.dept_id;

-- Non-Equi Join: uses any operator other than "="
SELECT e.emp_name, s.grade
FROM Employee e
JOIN SalaryGrade s ON e.salary BETWEEN s.min_salary AND s.max_salary;
```

## 8.10 SEMI JOIN & ANTI JOIN (concept, implemented via EXISTS/IN)

SQL has no `SEMI JOIN` keyword — it's a **concept** implemented with `EXISTS`/`IN`: return rows from A that **have a match** in B, **without duplicating A's rows** even if B has multiple matches, and **without pulling any columns from B**.

```sql
-- Semi Join: customers who placed at least one order (each customer appears once)
SELECT c.* FROM Customers c WHERE EXISTS (SELECT 1 FROM Orders o WHERE o.customer_id = c.customer_id);

-- Anti Join: customers who never ordered
SELECT c.* FROM Customers c WHERE NOT EXISTS (SELECT 1 FROM Orders o WHERE o.customer_id = c.customer_id);
```
> 🎯 **Why not just use `INNER JOIN` + `DISTINCT`?** If a customer has 3 orders, an `INNER JOIN` returns 3 rows for that customer; a semi-join (via `EXISTS`) returns exactly 1. This distinction is a favorite "gotcha" in senior interviews.

## 8.11 Joins — Common Mistakes

1. Forgetting `ON` condition → accidental cross join (Cartesian explosion).
2. Using `WHERE` instead of `ON` for the join condition in an **outer** join — this silently converts it back into an inner join (because `WHERE` filters out the NULL-padded rows).
3. Joining on columns of different data types (e.g., `VARCHAR` vs `INT`) causing implicit conversion and killing index usage.
4. Not handling duplicate rows caused by a "fan-out" join (joining to a table with multiple matching rows inflates aggregates — always aggregate the many-side **before** joining, or use `DISTINCT`/window functions carefully).

## 8.12 Joins — Follow-up Interview Questions

- "Can you join more than 2 tables?" → Yes, chain multiple `JOIN` clauses; the engine processes them left to right (logically) based on the optimizer's chosen order.
- "Which is faster — JOIN or subquery?" → Depends on the optimizer; modern engines often rewrite subqueries into joins internally. Don't assume JOIN is always faster — check the execution plan.
- "What is a fan-out / fan trap?" → When joining one row to multiple matching rows on the "many" side inflates SUM/COUNT unexpectedly; fix by pre-aggregating the many-side in a subquery/CTE before joining.

---

# SECTION 9 — SUBQUERIES

## 9.1 Scalar Subquery

**Definition:** Returns exactly one row, one column — usable anywhere a single value is expected.

```sql
SELECT emp_name, salary,
  (SELECT AVG(salary) FROM Employee) AS company_avg
FROM Employee;
```

## 9.2 Nested Subquery (non-correlated)

```sql
-- Employees earning above the company average
SELECT emp_name, salary FROM Employee
WHERE salary > (SELECT AVG(salary) FROM Employee);
```
Runs **once**, independently of the outer query.

## 9.3 Correlated Subquery ⭐

**Definition:** References a column from the outer query — so it must (logically) re-run **once per outer row**.

```sql
-- Employees earning more than their own department's average
SELECT e1.emp_name, e1.salary, e1.dept_id
FROM Employee e1
WHERE e1.salary > (
    SELECT AVG(e2.salary) FROM Employee e2 WHERE e2.dept_id = e1.dept_id
);
```
**Step-by-step:** For each outer row `e1`, the inner query computes the average salary of `e1`'s department, then compares. Diya Patel (62000) > dept-10 avg (83000)? No. Vikram Nair (95000) > 83000? Yes → included.

> ⚠️ **Performance consideration:** A naive correlated subquery can be **O(n × m)** — it *looks* like it re-runs per row, though modern optimizers often rewrite it internally into a join/semi-join for better performance. Still, on interview whiteboard, explain the conceptual "runs once per outer row" cost, then mention the optimizer may rewrite it.

## 9.4 Subquery in FROM (Inline View / Derived Table)

```sql
SELECT dept_id, avg_sal
FROM (
    SELECT dept_id, AVG(salary) AS avg_sal FROM Employee GROUP BY dept_id
) AS dept_avg
WHERE avg_sal > 60000;
```
Every derived table **must** have an alias (`dept_avg` here) — a very common syntax error for beginners.

## 9.5 Subquery with EXISTS / ANY / ALL — see Sections 5.5 & 5.6.

## 9.6 Complex Interview Question — Second Highest Salary via Subquery

```sql
SELECT MAX(salary) AS second_highest
FROM Employee
WHERE salary < (SELECT MAX(salary) FROM Employee);
```
**Explanation:** Inner query finds the overall max (120000, Priya). Outer query finds the max salary **strictly less than** that (95000, Vikram) → second highest.

## 9.7 Subqueries — Common Mistakes
- Returning more than one row from a scalar subquery context → runtime error ("subquery returns more than 1 row").
- Forgetting to alias a derived table (`FROM (SELECT ...)` with no alias) → syntax error in most databases.
- Using a correlated subquery when a JOIN/window function would be clearer and faster.

---

# SECTION 10 — SET OPERATIONS

| Operation | Behavior | Removes Duplicates? |
|---|---|---|
| `UNION` | Combines rows from two queries | ✅ Yes |
| `UNION ALL` | Combines rows from two queries | ❌ No (faster — no dedup pass) |
| `INTERSECT` | Rows present in **both** queries | ✅ Yes |
| `EXCEPT` (ANSI/Postgres/SQL Server) / `MINUS` (Oracle) | Rows in first query **not** in second | ✅ Yes |

**Rule for all set ops:** Both queries must have the **same number of columns** with **compatible data types**, in the same order.

```sql
-- All cities where either employees or customers are located
SELECT city FROM Employee
UNION
SELECT city FROM Customers;

-- Employees who are also (hypothetically) customers, by name match
SELECT emp_name FROM Employee
INTERSECT
SELECT customer_name FROM Customers;

-- Cities with employees but NOT used by customers
SELECT city FROM Employee
EXCEPT
SELECT city FROM Customers;
```

> 🎯 **Interview one-liner:** *"UNION ALL is faster than UNION because UNION has to sort/hash the combined set to remove duplicates — if you know there won't be duplicates (or don't care), always prefer UNION ALL."*

---

# SECTION 11 — CTE (Common Table Expressions)

## 11.1 Basic CTE (`WITH`)

**Definition:** A named, temporary result set defined with `WITH`, readable only within the statement that follows it — improves readability over nested subqueries.

```sql
WITH DeptAvg AS (
    SELECT dept_id, AVG(salary) AS avg_salary
    FROM Employee
    GROUP BY dept_id
)
SELECT e.emp_name, e.salary, d.avg_salary
FROM Employee e
JOIN DeptAvg d ON e.dept_id = d.dept_id
WHERE e.salary > d.avg_salary;
```

**Why use a CTE over a subquery?** Same execution semantics in most engines, but far more readable — especially when you reference the same derived set **multiple times**, or chain several CTEs together.

## 11.2 Multiple CTEs

```sql
WITH DeptAvg AS (
    SELECT dept_id, AVG(salary) AS avg_salary FROM Employee GROUP BY dept_id
),
HighEarners AS (
    SELECT e.emp_name, e.salary, e.dept_id
    FROM Employee e JOIN DeptAvg d ON e.dept_id = d.dept_id
    WHERE e.salary > d.avg_salary
)
SELECT * FROM HighEarners ORDER BY salary DESC;
```

## 11.3 Recursive CTE ⭐ (top-5 most-asked advanced topic)

**Definition:** A CTE that references **itself**, used to walk hierarchical/graph data — e.g., an employee-manager org chart.

```sql
WITH RECURSIVE OrgChart AS (
    -- Anchor member: the top of the hierarchy (CEO, no manager)
    SELECT emp_id, emp_name, manager_id, 1 AS level
    FROM Employee
    WHERE manager_id IS NULL

    UNION ALL

    -- Recursive member: join back to OrgChart to go one level deeper
    SELECT e.emp_id, e.emp_name, e.manager_id, oc.level + 1
    FROM Employee e
    JOIN OrgChart oc ON e.manager_id = oc.emp_id
)
SELECT * FROM OrgChart ORDER BY level;
```
> ⚠️ Oracle uses `WITH ... ` + `CONNECT BY PRIOR` instead of `WITH RECURSIVE`:
```sql
SELECT emp_id, emp_name, LEVEL
FROM Employee
START WITH manager_id IS NULL
CONNECT BY PRIOR emp_id = manager_id;
```

**Step-by-step:** Anchor picks Priya Iyer (level 1, no manager). Recursive step joins `Employee` to the *previous* result on `manager_id = emp_id`, adding everyone who reports to someone already in the set, incrementing `level`. This repeats until no new rows are found (Vikram/Ananya at level 2, Aarav/Diya/etc. at level 3).

**Output (partial):**
| emp_name | level |
|---|---|
| Priya Iyer | 1 |
| Vikram Nair | 2 |
| Ananya Rao | 2 |
| Suresh Kumar | 2 |
| Meera Joshi | 2 |
| Aarav Sharma | 3 |
| Diya Patel | 3 |
| Neha Verma | 3 |
| Karan Singh | 3 |
| Arjun Reddy | 3 |

**Common mistake:** Forgetting a **termination condition** in the recursive branch → infinite loop (most DBs cap recursion depth and will error out, e.g., MySQL's `cte_max_recursion_depth`).

**Interview tip:** Always mention you'd add `MAXRECURSION` (SQL Server) or check `cte_max_recursion_depth` (MySQL) as a safety net in production recursive CTEs over untrusted hierarchy data (to guard against cyclic manager references).

---

# SECTION 12 — WINDOW FUNCTIONS ⭐⭐⭐ (the #1 differentiator topic in 2024-2026 interviews)

## 12.1 Concept

**Definition:** A window function performs a calculation **across a set of rows related to the current row** ("the window") **without collapsing them into a single row** the way `GROUP BY` does. Every input row keeps its own output row.

**Syntax:**
```sql
<function>() OVER (
    [PARTITION BY column(s)]   -- optional: split into groups
    [ORDER BY column(s)]       -- optional: define row order within partition
    [ROWS/RANGE BETWEEN ... ]  -- optional: define the "frame" of rows to consider
)
```

## 12.2 ROW_NUMBER vs RANK vs DENSE_RANK ⭐ (guaranteed interview question)

```sql
SELECT emp_name, dept_id, salary,
       ROW_NUMBER() OVER (ORDER BY salary DESC) AS rn,
       RANK()       OVER (ORDER BY salary DESC) AS rnk,
       DENSE_RANK() OVER (ORDER BY salary DESC) AS drnk
FROM Employee;
```

**Output (using our tie between Karan & Arjun at 48000, and Rohan & Isha at 58000):**

| emp_name | salary | rn | rnk | drnk |
|---|---|---|---|---|
| Priya Iyer | 120000 | 1 | 1 | 1 |
| Suresh Kumar | 115000 | 2 | 2 | 2 |
| Vikram Nair | 95000 | 3 | 3 | 3 |
| Ananya Rao | 90000 | 4 | 4 | 4 |
| Diya Patel | 62000 | 5 | 5 | 5 |
| Rohan Mehta | 58000 | 6 | 6 | 6 |
| Isha Kapoor | 58000 | 7 | 6 | 6 |
| Aarav Sharma | 55000 | 8 | 8 | 7 |
| Meera Joshi | 50000 | 9 | 9 | 8 |
| Karan Singh | 48000 | 10 | 10 | 9 |
| Arjun Reddy | 48000 | 11 | 10 | 9 |
| Neha Verma | 25000 | 12 | 12 | 10 |

**Explanation of the tie behavior:**
- `ROW_NUMBER()` — always unique, arbitrarily breaks ties (Rohan gets 6, Isha gets 7).
- `RANK()` — ties get the **same rank**, but the **next rank skips** (Isha also gets 6, then Aarav jumps to 8, skipping 7).
- `DENSE_RANK()` — ties get the same rank, and the **next rank does not skip** (Aarav gets 7, right after 6).

> 🎯 **This is quite possibly the single most-repeated SQL interview question at TCS.** Memorize the tie-breaking difference cold.

## 12.3 NTILE

```sql
SELECT emp_name, salary, NTILE(4) OVER (ORDER BY salary DESC) AS quartile
FROM Employee;
```
Splits 12 rows into 4 roughly-equal buckets (3 rows each) — used for quartile/percentile bucketing.

## 12.4 LEAD & LAG

```sql
SELECT emp_name, salary,
       LAG(salary, 1) OVER (ORDER BY salary DESC) AS prev_salary,
       LEAD(salary, 1) OVER (ORDER BY salary DESC) AS next_salary
FROM Employee;
```
`LAG` looks at the **previous** row, `LEAD` looks at the **next** row — hugely useful for month-over-month comparisons, detecting jumps, or finding consecutive dates.

**Real use case — find salary difference vs previous employee in rank order:**
```sql
SELECT emp_name, salary,
       salary - LAG(salary) OVER (ORDER BY salary DESC) AS gap_from_prev
FROM Employee;
```

## 12.5 FIRST_VALUE & LAST_VALUE

```sql
SELECT emp_name, dept_id, salary,
       FIRST_VALUE(emp_name) OVER (PARTITION BY dept_id ORDER BY salary DESC) AS top_earner_in_dept
FROM Employee;
```
> ⚠️ **Classic LAST_VALUE trap:** By default the window **frame** for `LAST_VALUE` is `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` — meaning it returns the *current row's own value*, not the true last row of the partition! Fix by explicitly widening the frame:
```sql
LAST_VALUE(emp_name) OVER (
    PARTITION BY dept_id ORDER BY salary DESC
    ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
) AS lowest_earner_in_dept
```

## 12.6 Running Total (SUM ... OVER)

```sql
SELECT order_id, customer_id, amount,
       SUM(amount) OVER (ORDER BY order_date) AS running_total
FROM Orders;
```

## 12.7 Moving Average

```sql
SELECT sale_date, amount,
       AVG(amount) OVER (ORDER BY sale_date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS moving_avg_3
FROM Sales;
```
Averages the current row plus the 2 preceding rows (a 3-row moving average).

## 12.8 PARTITION BY — the "GROUP BY that doesn't collapse rows"

```sql
SELECT emp_name, dept_id, salary,
       AVG(salary) OVER (PARTITION BY dept_id) AS dept_avg
FROM Employee;
```
Every row keeps `emp_name`, but `dept_avg` repeats the department's average on every row of that department — impossible to do this cleanly with plain `GROUP BY` without a self-join.

## 12.9 Frame Clause — ROWS vs RANGE

| Clause | Meaning |
|---|---|
| `ROWS BETWEEN 1 PRECEDING AND CURRENT ROW` | Physical row count window |
| `RANGE BETWEEN 1 PRECEDING AND CURRENT ROW` | Logical value-based window (ties share the same frame) |

> 📝 **Interview tip:** If two rows have the **same** `ORDER BY` value, `RANGE` treats them as being in the **same** frame position (peer group), while `ROWS` treats them strictly by physical row order. This distinction trips up even experienced candidates.

## 12.10 Most-Asked Window Function Interview Questions

1. **"2nd highest salary per department"** — use `DENSE_RANK()` partitioned by department, filter `WHERE drnk = 2` in an outer query (window functions cannot be used directly in `WHERE` — see Section 22).
2. **"Difference between window function and GROUP BY?"** — GROUP BY collapses rows to one per group; a window function keeps every row and adds a computed column alongside it.
3. **"Can you use a window function in the WHERE clause?"** — No. Window functions are logically computed **after** WHERE (in the SELECT-adjacent phase), so you must wrap the query in a CTE/subquery and filter in the outer query.

---

# SECTION 13 — VIEWS

## 13.1 Simple View

**Definition:** A named, stored `SELECT` query that behaves like a virtual table — doesn't store data itself (except materialized views), always reflects live underlying data.

```sql
CREATE VIEW HighEarners AS
SELECT emp_name, dept_id, salary FROM Employee WHERE salary > 60000;

SELECT * FROM HighEarners;
```

## 13.2 Complex View (joins/aggregates)

```sql
CREATE VIEW DeptSalarySummary AS
SELECT d.dept_name, COUNT(e.emp_id) AS headcount, AVG(e.salary) AS avg_salary
FROM Department d
LEFT JOIN Employee e ON d.dept_id = e.dept_id
GROUP BY d.dept_name;
```
A view built on a join/aggregate is generally **not updatable** directly (you can't `INSERT` into it) because the engine can't unambiguously map a new row back to the base tables.

## 13.3 Materialized View

**Definition:** Unlike a normal view, a materialized view **physically stores** the query result and must be manually or automatically **refreshed**. Trades data freshness for query speed.

```sql
CREATE MATERIALIZED VIEW DeptSalarySummary_MV AS
SELECT dept_id, AVG(salary) AS avg_salary FROM Employee GROUP BY dept_id;

REFRESH MATERIALIZED VIEW DeptSalarySummary_MV;   -- PostgreSQL / Oracle
```

## 13.4 Indexed View (SQL Server term for a materialized view with a unique clustered index)

## 13.5 Views — Advantages & Disadvantages

| Advantages | Disadvantages |
|---|---|
| Simplifies complex queries for end users | Adds a layer of abstraction that can hide performance issues |
| Provides a security layer (expose only certain columns/rows) | Not always updatable (joins/aggregates) |
| Logical data independence — base table changes don't break consumers | Materialized views need refresh scheduling, can serve stale data |

> 🎯 **Interview one-liner:** *"A view is a stored query, always live; a materialized view is a stored result, physically persisted and refreshed on a schedule — use materialized views when the underlying query is expensive and slight staleness is acceptable."*

---

# SECTION 14 — INDEXES

## 14.1 What Is an Index?

**Definition:** A separate data structure (usually a B-Tree) that lets the database find rows **without scanning the entire table**, at the cost of extra storage and slower writes (every `INSERT`/`UPDATE`/`DELETE` must also update the index).

## 14.2 Types of Indexes

| Type | Description |
|---|---|
| **Clustered** | Determines the **physical storage order** of table rows. Only **one** per table (usually the primary key). |
| **Non-Clustered** | A separate structure with pointers back to the actual rows; a table can have **many**. |
| **Composite** | An index on **multiple columns** together — order of columns matters a lot (leftmost-prefix rule). |
| **Unique** | Guarantees no duplicate values, in addition to speeding up lookups. |
| **B-Tree** | The default/general-purpose index type; balanced tree, great for range queries (`>`, `<`, `BETWEEN`). |
| **Hash** | Great for exact-match `=` lookups; useless for range queries. |
| **Bitmap** | Efficient for columns with **low cardinality** (few distinct values, e.g., gender); common in Oracle data warehouses. |
| **Covering Index** | An index that contains **all columns** needed by a query, so the engine never touches the base table at all. |
| **Partial / Filtered** | An index built on only a **subset** of rows matching a condition (e.g., `WHERE status = 'Active'`) — smaller and faster for that specific filter. |

```sql
CREATE INDEX idx_emp_dept ON Employee(dept_id);                      -- simple index
CREATE UNIQUE INDEX idx_emp_email ON Employee(email);                 -- unique index
CREATE INDEX idx_emp_dept_salary ON Employee(dept_id, salary);        -- composite
CREATE INDEX idx_active_orders ON Orders(customer_id) WHERE status = 'Pending';  -- partial (PostgreSQL)
```

## 14.3 Leftmost-Prefix Rule (⭐ frequently tested)

Given `INDEX(dept_id, salary)`:
- `WHERE dept_id = 10` → ✅ uses index
- `WHERE dept_id = 10 AND salary > 50000` → ✅ uses index fully
- `WHERE salary > 50000` (dept_id not specified) → ❌ index **cannot** be used, because the leftmost column (`dept_id`) isn't part of the filter.

## 14.4 When Indexes Help vs Hurt

| Helps | Hurts |
|---|---|
| Columns frequently used in `WHERE`, `JOIN`, `ORDER BY` | Columns that are rarely queried but frequently updated |
| High-cardinality columns (many distinct values) | Very low-cardinality columns (unless using a bitmap index) |
| Read-heavy tables | Write-heavy tables (each index slows down INSERT/UPDATE/DELETE) |

## 14.5 Interview Tips & Common Mistakes

- Applying a function to an indexed column in `WHERE` (e.g., `WHERE UPPER(emp_name) = 'AARAV'`) **disables** normal index usage unless you build a function-based index.
- Over-indexing a table hurts write performance — index everything you query, nothing more.
- `CREATE INDEX` doesn't need to be re-run after data changes — indexes are maintained automatically, incrementally, by the engine on every write.

---

# SECTION 15 — TRANSACTIONS & ACID

## 15.1 ACID Properties

| Property | Meaning |
|---|---|
| **Atomicity** | A transaction is all-or-nothing — either every statement in it succeeds, or none do |
| **Consistency** | A transaction moves the database from one valid state to another, never violating constraints |
| **Isolation** | Concurrent transactions don't interfere with each other's intermediate state |
| **Durability** | Once committed, changes survive even a crash/power loss (written to durable storage/log) |

## 15.2 COMMIT / ROLLBACK / SAVEPOINT

```sql
BEGIN TRANSACTION;
UPDATE Bank SET balance = balance - 5000 WHERE account_id = 'A001';
SAVEPOINT before_credit;
UPDATE Bank SET balance = balance + 5000 WHERE account_id = 'A002';

-- If something goes wrong after the debit but before the credit:
ROLLBACK TO SAVEPOINT before_credit;

COMMIT;   -- makes everything since BEGIN permanent
-- or ROLLBACK;  -- undoes everything since BEGIN
```

**Real-world example:** A bank transfer **must** debit one account and credit another as a single atomic unit — if the credit fails after the debit succeeds, `ROLLBACK` prevents money from silently vanishing.

## 15.3 Isolation Levels & Read Phenomena

| Isolation Level | Dirty Read | Non-Repeatable Read | Phantom Read |
|---|---|---|---|
| Read Uncommitted | ✅ Possible | ✅ Possible | ✅ Possible |
| Read Committed | ❌ Prevented | ✅ Possible | ✅ Possible |
| Repeatable Read | ❌ Prevented | ❌ Prevented | ✅ Possible (varies by engine — MySQL InnoDB actually prevents most phantoms here via gap locks) |
| Serializable | ❌ Prevented | ❌ Prevented | ❌ Prevented |

**Definitions:**
- **Dirty Read:** Reading data another transaction has changed but **not yet committed** (which might later be rolled back).
- **Non-Repeatable Read:** Reading the same row twice in one transaction and getting **different values** because another transaction updated and committed in between.
- **Phantom Read:** Re-running the same query and getting a **different set of rows** (new rows appeared/disappeared) because another transaction inserted/deleted matching rows in between.

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;   -- SQL Server / Postgres
```

## 15.4 Locking & Deadlock

**Deadlock:** Two transactions each hold a lock the other needs, and each waits forever for the other to release it. The database detects this cycle and **kills one transaction** (the "deadlock victim") to break the cycle.

```
Txn A: locks Row 1, wants Row 2
Txn B: locks Row 2, wants Row 1
   → Circular wait → Deadlock → DB rolls back one transaction automatically
```
**Best practice:** Always acquire locks on multiple resources **in the same order** across all transactions to avoid circular waits.

## 15.5 MVCC (Multi-Version Concurrency Control)

**Definition:** Instead of blocking readers with locks, the database keeps multiple **versions** of a row — a reader sees the version that was committed **at the start of its transaction**, while writers create new versions. This is how PostgreSQL, Oracle, and MySQL InnoDB achieve high concurrency (readers don't block writers, and vice versa).

## 15.6 Common Interview Questions

- **"What's the default isolation level in MySQL InnoDB?"** → Repeatable Read.
- **"What's the default in PostgreSQL/Oracle/SQL Server?"** → Read Committed.
- **"How do you prevent lost updates?"** → Use `SELECT ... FOR UPDATE` (pessimistic locking) or optimistic concurrency (a version/timestamp column checked on UPDATE).

---

# SECTION 16 — STORED PROCEDURES, FUNCTIONS, TRIGGERS, CURSORS

## 16.1 Stored Procedure

```sql
DELIMITER //
CREATE PROCEDURE GiveRaise(IN p_dept_id INT, IN p_percent DECIMAL(5,2))
BEGIN
    UPDATE Employee
    SET salary = salary * (1 + p_percent/100)
    WHERE dept_id = p_dept_id;
END //
DELIMITER ;

CALL GiveRaise(10, 10.0);   -- 10% raise for dept 10
```

## 16.2 User-Defined Function (UDF)

```sql
CREATE FUNCTION GetAnnualSalary(p_monthly DECIMAL(10,2))
RETURNS DECIMAL(12,2)
DETERMINISTIC
BEGIN
    RETURN p_monthly * 12;
END;

SELECT emp_name, GetAnnualSalary(salary) FROM Employee;
```

| Stored Procedure | Function |
|---|---|
| May or may not return a value | Must return exactly one value (or table for TVFs) |
| Can perform DML (INSERT/UPDATE/DELETE) | Generally cannot modify data (in most DBs) |
| Called with `CALL`/`EXEC` | Called inline inside a `SELECT`/expression |

## 16.3 Triggers

```sql
CREATE TRIGGER trg_salary_audit
AFTER UPDATE ON Employee
FOR EACH ROW
BEGIN
    IF OLD.salary <> NEW.salary THEN
        INSERT INTO Salary_Audit(emp_id, old_salary, new_salary, changed_at)
        VALUES (OLD.emp_id, OLD.salary, NEW.salary, NOW());
    END IF;
END;
```
Fires automatically on `INSERT`/`UPDATE`/`DELETE` — common uses: auditing, enforcing complex business rules, maintaining denormalized summary columns.

> ⚠️ **Interview tip:** Overusing triggers makes systems hard to debug (hidden side effects) — mention this trade-off if asked "when should you avoid triggers?"

## 16.4 Cursors

```sql
DECLARE emp_cursor CURSOR FOR SELECT emp_id, salary FROM Employee WHERE dept_id = 10;
OPEN emp_cursor;
FETCH NEXT FROM emp_cursor INTO @id, @sal;
WHILE @@FETCH_STATUS = 0
BEGIN
    -- row-by-row processing
    FETCH NEXT FROM emp_cursor INTO @id, @sal;
END
CLOSE emp_cursor;
DEALLOCATE emp_cursor;
```
**Interview tip:** Cursors process **row-by-row** (RBAR — "Row By Agonizing Row") and are almost always **slower** than a set-based `UPDATE`/`JOIN`. Interviewers want to hear: *"I'd avoid a cursor here and use a set-based UPDATE instead, unless the logic genuinely can't be expressed declaratively."*

## 16.5 Temporary Tables

```sql
CREATE TEMPORARY TABLE Temp_HighEarners AS
SELECT * FROM Employee WHERE salary > 60000;
-- Automatically dropped at the end of the session
```

## 16.6 Dynamic SQL & Prepared Statements

```sql
SET @sql = CONCAT('SELECT * FROM Employee WHERE dept_id = ', dept_id_variable);
PREPARE stmt FROM @sql;
EXECUTE stmt;
DEALLOCATE PREPARE stmt;
```
**Why prepared statements matter:** They separate SQL structure from data values, which the database driver binds safely — the standard defense against **SQL injection**. Never build dynamic SQL via raw string concatenation of user input.

---

# SECTION 17 — NORMALIZATION

## 17.1 Why Normalize?

**Definition:** The process of organizing columns/tables to minimize data redundancy and avoid update/insert/delete anomalies.

## 17.2 Normal Forms

| Form | Rule | Example Fix |
|---|---|---|
| **1NF** | Every column holds atomic (indivisible) values; no repeating groups | Split a `phone_numbers = "999,888"` column into separate rows/table |
| **2NF** | 1NF + every non-key column depends on the **whole** primary key (relevant when key is composite) | In a `(student_id, subject_id) → teacher_name` table, if `teacher_name` depends only on `subject_id`, move it to a separate `Subject` table |
| **3NF** | 2NF + no **transitive** dependency (non-key column depending on another non-key column) | If `dept_location` depends on `dept_id`, not directly on `emp_id`, move it to `Department` table |
| **BCNF** | Stricter 3NF — every determinant must be a candidate key | Resolves edge cases 3NF misses when there are multiple overlapping candidate keys |
| **4NF** | No multi-valued dependencies | An employee having independent lists of "skills" and "languages" shouldn't be cross-joined into one table |
| **5NF** | No join dependency that isn't implied by candidate keys | Rare in practice — decomposing tables that can be reconstructed via join without redundancy |

## 17.3 Worked Example — Employee/Department 3NF violation

**Unnormalized (violates 3NF):**
| emp_id | emp_name | dept_id | dept_name | dept_location |
|---|---|---|---|---|

Here, `dept_name` and `dept_location` depend on `dept_id` (a non-key column), **not directly** on `emp_id` — a transitive dependency. Fix: split into `Employee(emp_id, emp_name, dept_id)` and `Department(dept_id, dept_name, dept_location)` — exactly our Section 0 schema.

## 17.4 Denormalization

**Definition:** Deliberately reintroducing redundancy (e.g., storing `dept_name` directly on the `Employee` row) to **avoid joins** and speed up reads — a common trade-off in reporting/analytics tables (star schemas) where read speed matters more than update anomalies.

> 🎯 **Interview one-liner:** *"Normalize for OLTP systems (transactional, frequent writes) to avoid anomalies; denormalize for OLAP/reporting systems (read-heavy) to avoid expensive joins."*

## 17.5 Common Interview Questions

- "Give a real example violating 2NF." → A composite key `(order_id, product_id)` where `product_name` depends only on `product_id`, not on the full composite key.
- "What anomaly does normalization prevent?" → **Insertion anomaly** (can't add a department without an employee), **Update anomaly** (must update dept_name in every employee row), **Deletion anomaly** (deleting the last employee in a department loses the department's info entirely).

---

# SECTION 18 — QUERY OPTIMIZATION

## 18.1 Reading an Execution Plan

```sql
EXPLAIN ANALYZE
SELECT emp_name FROM Employee WHERE dept_id = 10;
```
Look for: **Seq Scan/Full Table Scan** (reads every row — bad on large tables) vs **Index Scan/Index Seek** (uses an index — good), and the **estimated vs actual row count** (a big mismatch signals stale statistics).

## 18.2 Common Optimization Techniques

1. **Index the right columns** — those in `WHERE`, `JOIN ON`, `ORDER BY`, `GROUP BY`.
2. **Avoid `SELECT *`** — fetch only needed columns; enables covering indexes and reduces I/O.
3. **Avoid functions on indexed columns** in `WHERE` (`WHERE YEAR(hire_date) = 2023` disables the index; rewrite as a range: `WHERE hire_date >= '2023-01-01' AND hire_date < '2024-01-01'`).
4. **Prefer `EXISTS` over `IN`** for large correlated subqueries (and always over `NOT IN` — see Section 22 for the NULL trap).
5. **Filter early** — push `WHERE` conditions before large joins where possible (the optimizer often does this automatically, but writing it explicitly helps readability and sometimes forces a better plan).
6. **Batch large DML** — updating 10 million rows in one `UPDATE` can blow up the transaction log; consider chunked batches.
7. **Update table statistics** regularly (`ANALYZE TABLE` / `UPDATE STATISTICS`) so the optimizer's cost estimates stay accurate.
8. **Avoid implicit type conversion** — comparing a `VARCHAR` column to an `INT` literal can silently disable an index.

## 18.3 Interview Questions

- **"Query is slow — what do you check first?"** → Run `EXPLAIN`, check for full table scans, missing indexes on filter/join columns, and whether the row-count estimates match reality.
- **"How would you paginate a huge table efficiently?"** → Avoid large `OFFSET` values (which still scan and discard N rows); use **keyset/seek pagination** — `WHERE id > last_seen_id ORDER BY id LIMIT 20` — instead.
- **"N+1 query problem?"** → Running one query per row of a result set in application code instead of a single join/batched query — a classic performance anti-pattern in ORMs.

---

# SECTION 19 — QUERY QUESTION BANK (The Classics, TCS-Style)

> Format per question: **Problem → Query → Output → Explanation → Mistakes/Follow-up.** All queries run against Section 0 tables.

## 🔹 A. Salary / Ranking Questions

**Q1. Second highest salary (overall)**
```sql
SELECT MAX(salary) AS second_highest FROM Employee WHERE salary < (SELECT MAX(salary) FROM Employee);
```
Output: `95000` (Vikram Nair). Fails silently (returns NULL) if there's only one distinct salary value — always handle that edge case in an interview answer.

**Q2. Nth highest salary (general solution)**
```sql
SELECT DISTINCT salary FROM Employee ORDER BY salary DESC LIMIT 1 OFFSET (N-1);
-- OR, portable across all DBs:
SELECT salary FROM (
  SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS drnk FROM Employee
) t WHERE drnk = N;
```
**Why `DISTINCT` in the first version?** Without it, ties count as separate rows, so "3rd highest" could return a duplicate of the 2nd highest instead of a genuinely different value. **Why `DENSE_RANK` in the second?** It handles ties correctly and is portable (no `OFFSET` needed) — the answer interviewers actually want to see for "Nth highest".

**Q3. Third highest salary**
```sql
SELECT DISTINCT salary FROM Employee ORDER BY salary DESC LIMIT 1 OFFSET 2;
```
Output: `95000`... wait — distinct salaries desc are 120000, 115000, 95000 → 3rd is **95000**.

**Q4. Highest salary department-wise**
```sql
SELECT dept_id, MAX(salary) AS max_salary FROM Employee GROUP BY dept_id;
```

**Q5. 2nd highest salary in each department (window function)**
```sql
SELECT emp_name, dept_id, salary FROM (
  SELECT emp_name, dept_id, salary,
         DENSE_RANK() OVER (PARTITION BY dept_id ORDER BY salary DESC) AS drnk
  FROM Employee
) t WHERE drnk = 2;
```
Output includes Diya Patel (62000, dept 10), Rohan Mehta (58000, dept 20 — tied with Isha at rank 1... wait Isha=58000 too so both are rank 1, meaning dept 20 has **no rank-2** distinct salary) — good discussion point on how ties can mean "no 2nd highest" exists for a group.

**Q6. Employees earning more than their manager**
```sql
SELECT e.emp_name AS employee, e.salary AS emp_salary, m.emp_name AS manager, m.salary AS mgr_salary
FROM Employee e
JOIN Employee m ON e.manager_id = m.emp_id
WHERE e.salary > m.salary;
```
With our data, no employee out-earns their manager — a good example to discuss how to **modify** sample data live in an interview to demonstrate the query still works logically.

**Q7. Top N salaries per department (Top 2)**
```sql
SELECT * FROM (
  SELECT emp_name, dept_id, salary,
         ROW_NUMBER() OVER (PARTITION BY dept_id ORDER BY salary DESC) AS rn
  FROM Employee
) t WHERE rn <= 2;
```

**Q8. Employees without a manager**
```sql
SELECT emp_name FROM Employee WHERE manager_id IS NULL;
```
Output: `Priya Iyer`.

**Q9. Swap salary of two employees (classic LeetCode-style, using a gender-swap variant)**
```sql
UPDATE Employee
SET gender = CASE WHEN gender = 'M' THEN 'F' ELSE 'M' END;
```
For actual salary swap between two specific employees:
```sql
UPDATE Employee
SET salary = CASE emp_id WHEN 1 THEN (SELECT salary FROM Employee WHERE emp_id = 2)
                         WHEN 2 THEN (SELECT salary FROM Employee WHERE emp_id = 1)
             END
WHERE emp_id IN (1, 2);
```

**Q10. Employees with duplicate salary**
```sql
SELECT salary, COUNT(*) AS cnt FROM Employee GROUP BY salary HAVING COUNT(*) > 1;
```
Output: `48000 (2 rows)`, `58000 (2 rows)`.

**Q11. Median salary**
```sql
-- Portable via window functions
SELECT AVG(salary) AS median_salary FROM (
  SELECT salary,
         ROW_NUMBER() OVER (ORDER BY salary) AS rn,
         COUNT(*) OVER () AS total_cnt
  FROM Employee
) t
WHERE rn IN (FLOOR((total_cnt+1)/2), CEIL((total_cnt+1)/2));
```
**Explanation:** For an even count (12 employees), median = average of the two middle values; for odd count, both formulas point to the same single middle row.

**Q12. Mode (most frequent salary)**
```sql
SELECT salary FROM Employee GROUP BY salary ORDER BY COUNT(*) DESC LIMIT 1;
```

**Q13. Average salary department-wise, only for departments with >1 employee**
```sql
SELECT dept_id, AVG(salary) FROM Employee GROUP BY dept_id HAVING COUNT(*) > 1;
```

**Q14. Percentage of total salary contributed by each department**
```sql
SELECT dept_id, SUM(salary) AS dept_total,
       ROUND(SUM(salary) * 100.0 / SUM(SUM(salary)) OVER (), 2) AS pct_of_total
FROM Employee GROUP BY dept_id;
```

## 🔹 B. Duplicates

**Q15. Find duplicate rows (full row duplicates)**
```sql
SELECT emp_name, dept_id, salary, COUNT(*) FROM Employee
GROUP BY emp_name, dept_id, salary HAVING COUNT(*) > 1;
```

**Q16. Remove duplicate rows, keeping one copy (using ROW_NUMBER, since Employee has a PK, we simulate on a table without one, e.g. a raw staging table)**
```sql
WITH Ranked AS (
  SELECT *, ROW_NUMBER() OVER (PARTITION BY emp_name, dept_id, salary ORDER BY emp_id) AS rn
  FROM Staging_Employee
)
DELETE FROM Staging_Employee WHERE emp_id IN (SELECT emp_id FROM Ranked WHERE rn > 1);
```
**Explanation:** Keep `rn = 1` (the first occurrence per duplicate group), delete everything else.

**Q17. Duplicate emails (classic LeetCode question, adapted)**
```sql
SELECT email, COUNT(*) FROM Employee GROUP BY email HAVING COUNT(*) > 1;
```

## 🔹 C. NULL / Missing Data

**Q18. Departments without employees**
```sql
SELECT d.dept_name FROM Department d
LEFT JOIN Employee e ON d.dept_id = e.dept_id
WHERE e.emp_id IS NULL;
```
Output: `Finance`.

**Q19. Customers with no orders**
```sql
SELECT c.customer_name FROM Customers c
LEFT JOIN Orders o ON c.customer_id = o.customer_id
WHERE o.order_id IS NULL;
```
Output: `Nova Enterprises`.

**Q20. Find missing IDs in a sequence (gaps)**
```sql
WITH Seq AS (SELECT emp_id, LEAD(emp_id) OVER (ORDER BY emp_id) AS next_id FROM Employee)
SELECT emp_id + 1 AS missing_from, next_id - 1 AS missing_to
FROM Seq WHERE next_id - emp_id > 1;
```

## 🔹 D. Aggregation, Top-N, First/Last

**Q21. Top-selling product (by total sales amount)**
```sql
SELECT p.product_name, SUM(s.amount) AS total_sales
FROM Sales s JOIN Products p ON s.product_id = p.product_id
GROUP BY p.product_name ORDER BY total_sales DESC LIMIT 1;
```
Output: `Laptop` (110000 + 55000 + 165000 = 330000).

**Q22. Monthly sales total**
```sql
SELECT DATE_FORMAT(sale_date, '%Y-%m') AS month, SUM(amount) AS monthly_total
FROM Sales GROUP BY DATE_FORMAT(sale_date, '%Y-%m');
```

**Q23. Latest order per customer**
```sql
SELECT customer_id, MAX(order_date) AS latest_order FROM Orders GROUP BY customer_id;
```

**Q24. First and last record overall**
```sql
(SELECT * FROM Orders ORDER BY order_date ASC LIMIT 1)
UNION ALL
(SELECT * FROM Orders ORDER BY order_date DESC LIMIT 1);
```

**Q25. Even/Odd numbered records**
```sql
-- Odd rows
SELECT * FROM (SELECT *, ROW_NUMBER() OVER (ORDER BY emp_id) AS rn FROM Employee) t WHERE MOD(rn, 2) = 1;
-- Even rows
SELECT * FROM (SELECT *, ROW_NUMBER() OVER (ORDER BY emp_id) AS rn FROM Employee) t WHERE MOD(rn, 2) = 0;
```

## 🔹 E. Running Totals, Streaks, and Sequences

**Q26. Running total of order amount (overall, ordered by date)**
```sql
SELECT order_id, order_date, amount,
       SUM(amount) OVER (ORDER BY order_date, order_id) AS running_total
FROM Orders;
```
**Explanation:** Each row's `running_total` = sum of `amount` for all rows up to and including the current row, in date order — the default frame for `SUM() OVER (ORDER BY ...)` is `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`.

**Q27. Rolling / moving average of sales (3-period)**
```sql
SELECT sale_date, amount,
       AVG(amount) OVER (ORDER BY sale_date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS moving_avg
FROM Sales;
```

**Q28. Moving sum (7-day window, general pattern)**
```sql
SELECT sale_date, amount,
       SUM(amount) OVER (ORDER BY sale_date RANGE BETWEEN INTERVAL 6 DAY PRECEDING AND CURRENT ROW) AS sum_7d
FROM Sales;   -- PostgreSQL/MySQL 8+ style RANGE with INTERVAL
```

**Q29. Find consecutive login / attendance streak (⭐ very popular)**
```sql
-- emp 7 has 3 consecutive Present days: find the streak length
WITH Flagged AS (
  SELECT emp_id, attend_date,
         DATEDIFF(attend_date, LAG(attend_date) OVER (PARTITION BY emp_id ORDER BY attend_date)) AS gap
  FROM Attendance WHERE status = 'Present'
),
Grouped AS (
  SELECT emp_id, attend_date,
         SUM(CASE WHEN gap = 1 THEN 0 ELSE 1 END) OVER (PARTITION BY emp_id ORDER BY attend_date) AS streak_group
  FROM Flagged
)
SELECT emp_id, streak_group, COUNT(*) AS streak_length, MIN(attend_date) AS streak_start, MAX(attend_date) AS streak_end
FROM Grouped GROUP BY emp_id, streak_group HAVING COUNT(*) >= 3;
```
**Explanation — the "island and gaps" technique:** Every time the gap from the previous Present date isn't exactly 1 day, we start a **new group** (`streak_group` increments). Rows within the same group are a consecutive run. This "difference between row number and a grouping value creates islands" trick is one of the most reused patterns in advanced SQL interviews — memorize it.

**Q30. Find the gap/break in a date sequence**
Same technique as Q20/Q29 — compute `LAG()`, flag where the difference isn't the expected step, group into islands.

**Q31. Consecutive record numbers with same value (e.g., 3+ days with Present status back to back) — see Q29.**

## 🔹 F. Dates, Age, and Time

**Q32. Difference between two dates (order fulfilment time, hospital stay length)**
```sql
SELECT patient_name, DATEDIFF(discharge_date, admit_date) AS stay_days FROM Hospital_Patients;
```
Ramesh: 9 days. Manoj: `NULL` (still admitted) — a good spot to mention `COALESCE(discharge_date, CURDATE())` to compute an **ongoing** stay length instead of NULL.

**Q33. Age calculation from date of birth**
```sql
SELECT emp_name, TIMESTAMPDIFF(YEAR, hire_date, CURDATE()) AS years_of_service FROM Employee; -- MySQL
SELECT emp_name, DATE_PART('year', AGE(CURRENT_DATE, hire_date)) AS years_of_service FROM Employee; -- PostgreSQL
```

**Q34. Employees joined in the last month**
```sql
SELECT emp_name, hire_date FROM Employee
WHERE hire_date >= DATE_SUB(CURDATE(), INTERVAL 1 MONTH);
```

**Q35. Weekend detection**
```sql
SELECT order_id, order_date,
       CASE WHEN DAYOFWEEK(order_date) IN (1,7) THEN 'Weekend' ELSE 'Weekday' END AS day_type
FROM Orders;  -- MySQL: 1 = Sunday, 7 = Saturday
```

**Q36. Working days between two dates (excluding weekends, simplified)**
```sql
SELECT (DATEDIFF(end_date, start_date) + 1)
     - (2 * (DATEDIFF(end_date, start_date) DIV 7))
     - CASE WHEN DAYOFWEEK(start_date) = 1 THEN 1 ELSE 0 END
     - CASE WHEN DAYOFWEEK(end_date) = 7 THEN 1 ELSE 0 END AS working_days
FROM Project WHERE project_id = 'PR1';
```
> 📝 **Interview tip:** For working-days calculations, many interviewers are happy if you simply describe the approach (subtract weekend days) rather than write perfect MySQL arithmetic — clarity of logic matters more than syntax perfection here.

## 🔹 G. Hierarchy, Pivot, and Advanced Aggregation

**Q37. Recursive employee tree / manager hierarchy — see full worked example in Section 11.3.**

**Q38. Pivot — rows to columns (department headcount as columns)**
```sql
SELECT
  SUM(CASE WHEN dept_id = 10 THEN 1 ELSE 0 END) AS Engineering,
  SUM(CASE WHEN dept_id = 20 THEN 1 ELSE 0 END) AS Business,
  SUM(CASE WHEN dept_id = 30 THEN 1 ELSE 0 END) AS Quality
FROM Employee;
```
**Explanation:** Standard SQL has no universal `PIVOT` keyword (SQL Server and Oracle have one; MySQL/Postgres don't) — the **portable** way is conditional aggregation with `CASE WHEN` inside `SUM()`/`COUNT()`. This is the technique TCS interviewers actually want to see.

```sql
-- SQL Server native PIVOT syntax (know it exists, but lead with the CASE WHEN version above)
SELECT * FROM (SELECT dept_id, salary FROM Employee) src
PIVOT (COUNT(salary) FOR dept_id IN ([10],[20],[30])) AS pvt;
```

**Q39. Unpivot — columns to rows**
```sql
SELECT emp_id, 'basic' AS component, basic AS amount FROM Salary
UNION ALL
SELECT emp_id, 'hra', hra FROM Salary
UNION ALL
SELECT emp_id, 'bonus', bonus FROM Salary;
```

**Q40. Transpose a summary table (dept-wise avg salary as columns) — same conditional-aggregation technique as Q38.**

**Q41. Actor with maximum movies (self-referencing count)**
```sql
SELECT actor_name, COUNT(DISTINCT movie_id) AS movie_count
FROM Actors GROUP BY actor_name ORDER BY movie_count DESC LIMIT 1;
```
Output: Actor D — 2 movies.

**Q42. Employee with maximum projects**
```sql
SELECT e.emp_name, COUNT(p.project_id) AS project_count
FROM Employee e JOIN Project p ON e.emp_id = p.emp_id
GROUP BY e.emp_name ORDER BY project_count DESC LIMIT 1;
```

**Q43. Customer Lifetime Value (total spend per customer, Delivered orders only)**
```sql
SELECT c.customer_name, SUM(o.amount) AS lifetime_value
FROM Customers c JOIN Orders o ON c.customer_id = o.customer_id
WHERE o.status = 'Delivered'
GROUP BY c.customer_name ORDER BY lifetime_value DESC;
```

**Q44. Order frequency per customer**
```sql
SELECT customer_id, COUNT(*) AS order_count FROM Orders GROUP BY customer_id;
```

**Q45. Bank account balance after all transactions (reconciliation)**
```sql
SELECT b.account_id,
       b.balance AS stored_balance,
       SUM(CASE WHEN t.txn_type = 'Deposit' THEN t.amount ELSE -t.amount END) AS net_txn_amount
FROM Bank b JOIN Transactions t ON b.account_id = t.account_id
GROUP BY b.account_id, b.balance;
```

**Q46. Latest transaction per account**
```sql
SELECT account_id, txn_date, amount FROM (
  SELECT *, ROW_NUMBER() OVER (PARTITION BY account_id ORDER BY txn_date DESC) AS rn
  FROM Transactions
) t WHERE rn = 1;
```

**Q47. Movies with above-average rating in their genre**
```sql
SELECT title, genre, rating FROM Movies m
WHERE rating > (SELECT AVG(rating) FROM Movies WHERE genre = m.genre);
```

**Q48. Books currently issued and not yet returned (Library)**
```sql
SELECT book_title, issued_to FROM Library WHERE return_date IS NULL;
```
Output: `Sapiens (Meera)`.

**Q49. Patients still admitted (Hospital)**
```sql
SELECT patient_name FROM Hospital_Patients WHERE discharge_date IS NULL;
```
Output: `Manoj`.

**Q50. Doctor treating the most patients**
```sql
SELECT d.doctor_name, COUNT(p.patient_id) AS patient_count
FROM Doctors d JOIN Hospital_Patients p ON d.doctor_id = p.doctor_id
GROUP BY d.doctor_name ORDER BY patient_count DESC LIMIT 1;
```
Output: `Dr. Anil` — 2 patients (Heart Disease is the most common condition in the sample).

---

# SECTION 20 — OUTPUT PREDICTION QUESTIONS

> Given the query, predict the output **before** reading the answer. These are designed to expose the exact traps interviewers set.

**Q1.**
```sql
SELECT COUNT(*), COUNT(marks) FROM Student;
```
**Answer:** `6, 5`. `COUNT(*)` counts all rows; `COUNT(marks)` skips Pooja's NULL.

**Q2.**
```sql
SELECT dept_id, COUNT(*) FROM Employee GROUP BY dept_id;
```
**Answer:** Includes a row `NULL, 1` for Neha Verma — NULL is treated as its own group in `GROUP BY`.

**Q3.**
```sql
SELECT * FROM Employee WHERE manager_id = NULL;
```
**Answer:** **Empty result set** (zero rows) — `= NULL` never evaluates to TRUE; must use `IS NULL`.

**Q4.**
```sql
SELECT emp_name FROM Employee WHERE dept_id NOT IN (SELECT dept_id FROM Employee WHERE dept_id IS NULL);
```
**Answer:** **Empty result set.** The subquery returns `(NULL)`. `NOT IN (NULL)` makes every comparison UNKNOWN, so the outer `WHERE` matches nothing — even though logically we "meant" to exclude nothing.

**Q5.**
```sql
SELECT AVG(marks) FROM Student;
```
**Answer:** `(92+85+92+76+88)/5 = 86.6` — NOT divided by 6. `AVG()` ignores NULLs both in the sum and in the count divisor.

**Q6.**
```sql
SELECT emp_name, salary FROM Employee ORDER BY salary DESC LIMIT 1 OFFSET 1;
```
**Answer:** `Suresh Kumar, 115000` — skips the top row (Priya, 120000), returns the next one.

**Q7.**
```sql
SELECT dept_id, salary, RANK() OVER (PARTITION BY dept_id ORDER BY salary DESC) FROM Employee WHERE dept_id = 20;
```
**Answer:** Rohan and Isha both tied at 58000 → **both get rank 1**; Ananya Rao (90000) is actually higher — wait, reorder by salary desc: Ananya(90000)=1, Rohan(58000)=2, Isha(58000)=2. (Ties get the same rank; no rank 3 is skipped after since there's no third distinct row.)

**Q8.**
```sql
SELECT emp_name FROM Employee e1
WHERE EXISTS (SELECT 1 FROM Employee e2 WHERE e2.manager_id = e1.emp_id);
```
**Answer:** Returns everyone who **is a manager of someone else** — Priya, Vikram, Ananya, Suresh, Meera (assuming Meera has no reports, she'd be excluded — check: manager_id=8 appears for emps 1,2,5,9,10,12; wait manager_id 8 = Priya. So actual managers referenced: 5 (Vikram), 6 (Ananya), 8 (Priya), 9 (Suresh). Only these 4 names are returned.

**Q9.**
```sql
SELECT UNION_RESULT.* FROM (
  SELECT emp_name, salary FROM Employee WHERE dept_id = 10
  UNION ALL
  SELECT emp_name, salary FROM Employee WHERE salary > 90000
) AS UNION_RESULT;
```
**Answer:** Priya Iyer (dept 10 **and** salary 120000 > 90000) appears **twice**, because `UNION ALL` does not deduplicate.

**Q10.**
```sql
SELECT dept_id, COUNT(*) FROM Employee GROUP BY dept_id HAVING dept_id > 10;
```
**Answer:** Runs fine — `dept_id` is a GROUP BY column, so it's valid in `HAVING` even without an aggregate. Returns `20, 30, 40` groups (10 and NULL excluded).

**Q11.**
```sql
SELECT LAST_VALUE(emp_name) OVER (PARTITION BY dept_id ORDER BY salary) FROM Employee WHERE dept_id = 10;
```
**Answer (trap!):** Without an explicit frame, this does **not** return the highest earner's name for every row — it returns **each row's own name** (because the default frame ends at `CURRENT ROW`). See Section 12.5.

**Q12.**
```sql
SELECT emp_name FROM Employee WHERE salary = (SELECT MAX(salary) FROM Employee WHERE dept_id = 20);
```
**Answer:** **Empty.** Max salary in dept 20 is 90000 (Ananya), but Ananya's own `dept_id` is 20 so `emp_name` matches only `Employee` rows with `salary = 90000` — that's Ananya Rao herself, so actually **Ananya Rao** is returned (self-correcting: the outer query has no dept filter, so any employee company-wide with salary 90000 qualifies — only Ananya has that salary).

**Q13.**
```sql
SELECT * FROM Employee WHERE dept_id = 10 AND dept_id = 20;
```
**Answer:** **Empty** — no row can simultaneously equal two different literal values with `AND`. (Common beginner confusion vs. `IN`.)

**Q14.**
```sql
SELECT dept_id, designation, SUM(salary) FROM Employee GROUP BY ROLLUP(dept_id, designation) ORDER BY dept_id;
```
**Answer:** Rows per `(dept_id, designation)` pair, **plus** one subtotal row per `dept_id` (with `designation = NULL`), **plus** one grand-total row (both NULL) — likely sorted with NULLs first or last depending on DB.

**Q15.**
```sql
SELECT emp_name FROM Employee ORDER BY salary_typo DESC;
```
**Answer:** **Error** — `salary_typo` doesn't exist as a column; fails at the binder/semantic-check stage (Section 1.3), not the parser stage, since the *syntax* itself is valid.

---

# SECTION 21 — SCENARIO-BASED QUESTIONS

> These simulate the "imagine a real system" style questions TCS interviewers ask to test whether you can translate a business need into SQL.

## 🔹 E-Commerce

**S1. "Show me customers who spent more than ₹20,000 total, only counting delivered orders."**
```sql
SELECT c.customer_name, SUM(o.amount) AS total_spent
FROM Customers c JOIN Orders o ON c.customer_id = o.customer_id
WHERE o.status = 'Delivered'
GROUP BY c.customer_name HAVING SUM(o.amount) > 20000;
```

**S2. "Which product category generates the most revenue?"**
```sql
SELECT p.category, SUM(o.amount) AS revenue
FROM Orders o JOIN Products p ON o.product_id = p.product_id
WHERE o.status = 'Delivered'
GROUP BY p.category ORDER BY revenue DESC LIMIT 1;
```

**S3. "Find customers who ordered the same product more than once."**
```sql
SELECT customer_id, product_id, COUNT(*) FROM Orders GROUP BY customer_id, product_id HAVING COUNT(*) > 1;
```

## 🔹 Banking

**S4. "Flag accounts where withdrawals exceed deposits in a given month."**
```sql
SELECT account_id,
       SUM(CASE WHEN txn_type='Deposit' THEN amount ELSE 0 END) AS total_deposit,
       SUM(CASE WHEN txn_type='Withdrawal' THEN amount ELSE 0 END) AS total_withdrawal
FROM Transactions
GROUP BY account_id
HAVING SUM(CASE WHEN txn_type='Withdrawal' THEN amount ELSE 0 END)
     > SUM(CASE WHEN txn_type='Deposit' THEN amount ELSE 0 END);
```

**S5. "Detect a customer holding more than one account (potential duplicate KYC)."**
```sql
SELECT customer_id, COUNT(*) AS account_count FROM Bank GROUP BY customer_id HAVING COUNT(*) > 1;
```
Output: `customer_id 1` (Global Traders holds A001 and A004).

## 🔹 HR / Employee Management

**S6. "HR wants a report: for every department, headcount, average salary, and the name of the highest earner."**
```sql
WITH Ranked AS (
  SELECT *, ROW_NUMBER() OVER (PARTITION BY dept_id ORDER BY salary DESC) AS rn FROM Employee
)
SELECT d.dept_name,
       COUNT(e.emp_id) AS headcount,
       AVG(e.salary) AS avg_salary,
       MAX(CASE WHEN r.rn = 1 THEN r.emp_name END) AS top_earner
FROM Department d
LEFT JOIN Employee e ON d.dept_id = e.dept_id
LEFT JOIN Ranked r ON d.dept_id = r.dept_id AND r.rn = 1
GROUP BY d.dept_name;
```

**S7. "Identify employees eligible for a 5-year service award."**
```sql
SELECT emp_name, hire_date FROM Employee WHERE hire_date <= DATE_SUB(CURDATE(), INTERVAL 5 YEAR);
```

## 🔹 College / Student Management

**S8. "List the topper of each class."**
```sql
SELECT * FROM (
  SELECT student_name, class, marks, RANK() OVER (PARTITION BY class ORDER BY marks DESC) AS rnk
  FROM Student
) t WHERE rnk = 1;
```
Output: Aditi and Sneha both tie at 92 marks — but Aditi is 10A and Sneha is 10B, so both are correctly the topper of their **own** class.

**S9. "Find students who haven't submitted marks (incomplete records) for follow-up."**
```sql
SELECT student_name FROM Student WHERE marks IS NULL;
```

## 🔹 Inventory / Logistics

**S10. "Alert when product sales in a region drop for two consecutive periods."**
Approach: use `LAG()` twice (or `LAG(amount,1)` and `LAG(amount,2)`) partitioned by product+region, ordered by sale_date, then filter where `amount < lag1 AND lag1 < lag2`. *(Discuss the LAG-chaining pattern — a strong senior-level answer even without full sample data for this exact case.)*

**S11. "Which region has never sold the Notebook (product 504)?"**
```sql
SELECT DISTINCT region FROM Sales
WHERE region NOT IN (SELECT region FROM Sales WHERE product_id = 504);
```
⚠️ Careful — this is the exact `NOT IN` + possible-NULL trap from Section 22. Since `region` here has no NULLs, it's safe, but always mention you'd double check for NULLs before shipping this to production.

## 🔹 Hospital

**S12. "Find the average length of stay per doctor, for discharged patients only."**
```sql
SELECT d.doctor_name, AVG(DATEDIFF(p.discharge_date, p.admit_date)) AS avg_stay_days
FROM Doctors d JOIN Hospital_Patients p ON d.doctor_id = p.doctor_id
WHERE p.discharge_date IS NOT NULL
GROUP BY d.doctor_name;
```

## 🔹 Social Media (product-company style)

**S13. "Find users who follow each other back (mutual follows), given a Follows(follower_id, followee_id) table."**
```sql
SELECT f1.follower_id, f1.followee_id
FROM Follows f1
JOIN Follows f2 ON f1.follower_id = f2.followee_id AND f1.followee_id = f2.follower_id
WHERE f1.follower_id < f1.followee_id;   -- avoid duplicate pairs (A,B) and (B,A)
```

## 🔹 Finance

**S14. "Compute month-over-month revenue growth %."**
```sql
WITH Monthly AS (
  SELECT DATE_FORMAT(sale_date,'%Y-%m') AS month, SUM(amount) AS revenue
  FROM Sales GROUP BY DATE_FORMAT(sale_date,'%Y-%m')
)
SELECT month, revenue,
       ROUND((revenue - LAG(revenue) OVER (ORDER BY month)) * 100.0 / LAG(revenue) OVER (ORDER BY month), 2) AS mom_growth_pct
FROM Monthly;
```

> 📝 **Interviewer wants to see, on every scenario question:** (1) you clarify assumptions out loud ("Assuming 'active' means status = Delivered..."), (2) you write clean, readable SQL — CTEs over deeply nested subqueries, (3) you mention edge cases (NULLs, ties, empty groups) unprompted.

---

# SECTION 22 — TRICKY SQL QUESTIONS (X vs Y) ⭐

## 22.1 NOT IN vs NOT EXISTS (the #1 tricky question at every service company)

```sql
-- Dangerous if dept_id can be NULL anywhere in the subquery result
SELECT emp_name FROM Employee WHERE dept_id NOT IN (SELECT dept_id FROM Employee WHERE dept_id IS NULL);
-- Returns ZERO rows — NOT IN silently breaks when the list contains a NULL

-- Safe, NULL-proof equivalent
SELECT e.emp_name FROM Employee e
WHERE NOT EXISTS (SELECT 1 FROM Employee e2 WHERE e2.dept_id IS NULL AND e2.dept_id = e.dept_id);
```
**Rule of thumb:** Prefer `NOT EXISTS` over `NOT IN` whenever the subquery's column **can** contain NULLs — which, in real production schemas, is "almost always." `NOT EXISTS` is NULL-safe because it only ever tests row existence, never does a value-by-value `<>` comparison against every list element.

## 22.2 COUNT(*) vs COUNT(column) vs COUNT(1)

Covered in 6.1 — `COUNT(*)`/`COUNT(1)` count rows; `COUNT(column)` skips NULLs in that column. No performance difference between `COUNT(*)` and `COUNT(1)` in any modern optimizer.

## 22.3 DELETE vs TRUNCATE vs DROP — see full table in Section 2.3.

## 22.4 WHERE vs HAVING — see Section 7.2.

## 22.5 UNION vs UNION ALL — see Section 10.

## 22.6 CHAR vs VARCHAR

| CHAR(n) | VARCHAR(n) |
|---|---|
| Fixed-length; pads with spaces to `n` | Variable-length; stores only what's needed (+ small overhead) |
| Slightly faster for fixed-width data (e.g., state codes, gender flags) | Better for variable-length text (names, descriptions) |
| Wastes space on short values | More storage-efficient |

## 22.7 RANK() vs DENSE_RANK() vs ROW_NUMBER() — see Section 12.2 (memorize the worked example).

## 22.8 INNER JOIN vs EXISTS

An `INNER JOIN` to a table with multiple matches **duplicates** the outer row once per match; `EXISTS` never duplicates — it's a yes/no check. Use `EXISTS` when you just need to know "does a match exist" without pulling any columns from the other table.

## 22.9 LEFT JOIN + IS NULL vs NOT EXISTS (finding "missing" rows)

Both work, but `NOT EXISTS` is generally considered clearer intent and is **NULL-safe by construction**; `LEFT JOIN ... WHERE x IS NULL` is the more commonly *seen* pattern in real codebases and equally correct as long as you filter on a column that's genuinely NULL only for non-matches (usually the joined table's primary key).

## 22.10 NULL Comparison Traps

- `NULL = NULL` → **UNKNOWN**, not TRUE.
- `NULL <> NULL` → also UNKNOWN.
- `WHERE column <> NULL` → matches **nothing**, ever.
- `COUNT(column)` skips NULLs, but `COUNT(*)` does not.
- `salary IN (NULL)` → UNKNOWN (never TRUE), but `salary NOT IN (NULL)` → also always UNKNOWN (never TRUE) — this is *why* the NOT IN trap in 22.1 happens.

## 22.11 Window Function Traps

- Cannot filter a window function's result directly in `WHERE` — must wrap in a CTE/subquery (Section 12.10).
- `LAST_VALUE()` needs an explicit frame (`ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING`) or it silently returns the current row (Section 12.5).
- `RANK()` skips numbers after ties; `DENSE_RANK()` doesn't (Section 12.2).

## 22.12 GROUP BY Traps

- Selecting a non-aggregated, non-grouped column → error in strict-mode databases (PostgreSQL, SQL Server, Oracle), but MySQL may silently allow it and pick an **arbitrary** value from the group unless `ONLY_FULL_GROUP_BY` mode is enabled — a genuinely dangerous MySQL default some interviewers specifically probe for.
- `GROUP BY` treats all NULLs as **one single group**, unlike a naive `WHERE column = NULL` which matches nothing.

## 22.13 Order of Execution Traps

- Can't use a `SELECT` alias in `WHERE` (WHERE runs before SELECT computes it) — but you *can* use it in `ORDER BY`/`GROUP BY` in most databases, since those run after or alongside SELECT (MySQL/Postgres allow alias in GROUP BY; strict Oracle does not).
- `LIMIT`/`TOP` applies **after** `ORDER BY` — a `LIMIT` before sorting would be meaningless, which is why `LIMIT` is always the last clause.

## 22.14 Cartesian Product Mistakes

Forgetting a JOIN condition (or using a comma-join `FROM A, B` without a matching `WHERE`) silently produces `rows(A) × rows(B)` — a bug that often goes unnoticed on small test tables but explodes to millions of rows in production.

## 22.15 Correlated Subquery Pitfalls

A correlated subquery inside `SELECT` (not just `WHERE`) runs once per outer row — on a large table, this is a common cause of a query that works fine on 100 rows but times out on 10 million. Rewrite as a `JOIN` or window function whenever possible.

---

# SECTION 23 — ⭐ MOST-ASKED TCS SQL INTERVIEW QUESTIONS ⭐
### (The list to memorize if you only have 1 day left)

> **Importance Rating:** 🔥🔥🔥 = asked in almost every TCS Prime/Digital/Ninja SQL round · 🔥🔥 = asked very often · 🔥 = occasionally asked, but shows depth if you bring it up unprompted.

---

### 1. What is the difference between SQL and MySQL? 🔥🔥
**Expected answer:** SQL is a **language** (the standard); MySQL is a **database product** that implements/understands SQL (with its own dialect extensions). Comparing them directly is like comparing "a language" to "a book written in that language."

### 2. Second highest salary — write the query. 🔥🔥🔥
**Difficulty:** Easy–Medium. See Section 19, Q1–Q2 for the full worked solution (`MAX(salary) WHERE salary < overall MAX`, or `DENSE_RANK`).
**Follow-up:** *"What if there are ties for the highest salary?"* → Both solutions still work correctly, because they compare against the **value**, not the row count.

### 3. Difference between WHERE and HAVING. 🔥🔥🔥
See Section 7.2. **Follow-up:** *"Can HAVING be used without GROUP BY?"* → Yes, it then treats the whole table as one group (e.g., `HAVING COUNT(*) > 5` with no GROUP BY checks the total row count).

### 4. Explain all types of JOINs with examples. 🔥🔥🔥
See Section 8 in full — this is asked in essentially **every single TCS SQL round**. Be ready to draw the diagram from memory and write each join live.

### 5. What is a Primary Key vs Foreign Key vs Unique Key? 🔥🔥🔥
**Expected answer:** Primary Key uniquely identifies a row (implies `NOT NULL + UNIQUE`, one per table); Foreign Key enforces a relationship to another table's primary/unique key (can be NULL, can repeat); Unique Key enforces uniqueness but **allows one NULL** (in most databases) and a table can have several.

### 6. Difference between DELETE, TRUNCATE, and DROP. 🔥🔥🔥
See Section 2.3 — asked almost as often as JOINs.

### 7. What are ACID properties? 🔥🔥🔥
See Section 15.1. **Follow-up:** *"Give a real example of Atomicity."* → Bank transfer: debit + credit must both happen or neither does.

### 8. Explain Normalization with an example up to 3NF. 🔥🔥
See Section 17.3 — always have the Employee/Department worked example ready to draw on a whiteboard.

### 9. What is a subquery? Correlated vs non-correlated. 🔥🔥
See Section 9.3. **Follow-up:** *"Which is generally slower?"* → Correlated (conceptually runs per outer row), though modern optimizers often rewrite it.

### 10. What is indexing? How does it improve performance? 🔥🔥
See Section 14. **Follow-up:** *"Does adding more indexes always help?"* → No — every index slows down writes (INSERT/UPDATE/DELETE) and consumes storage; index only what you actually filter/join/sort on.

### 11. Difference between clustered and non-clustered index. 🔥🔥
See Section 14.2. **Key line to say:** *"Clustered index determines physical row order — only one per table; non-clustered is a separate lookup structure — a table can have many."*

### 12. What are window functions? Explain RANK, DENSE_RANK, ROW_NUMBER. 🔥🔥🔥
See Section 12.2 — increasingly the **most-weighted single topic** in 2025-2026 interviews, including at TCS Digital.

### 13. What is a CTE? What is a recursive CTE, and where would you use one? 🔥🔥
See Section 11 — the manager-hierarchy example is the textbook answer they expect.

### 14. Explain the logical order of SQL execution. 🔥🔥
See Section 1.5 — a strong candidate uses this to *explain* several other answers (e.g., why HAVING allows aggregates and WHERE doesn't), which visibly impresses interviewers.

### 15. What is the difference between UNION and UNION ALL? 🔥🔥
See Section 10. Mention the performance angle (dedup sort/hash cost) — that's the detail that separates a strong answer from an average one.

### 16. What are Views? Can you update data through a view? 🔥
See Section 13. **Follow-up:** *"When is a view not updatable?"* → When it involves joins, aggregates, `DISTINCT`, or `GROUP BY`.

### 17. What is a Stored Procedure? How is it different from a Function? 🔥
See Section 16.1–16.2.

### 18. What is a Trigger? Give a real use case. 🔥
See Section 16.3 — auditing salary changes (our exact example) is a favorite real-world case to mention.

### 19. Explain Transaction Isolation Levels and the read phenomena they prevent. 🔥🔥
See Section 15.3 — know the 4-level table (Dirty/Non-repeatable/Phantom) cold.

### 20. What is the difference between NOT IN and NOT EXISTS? 🔥🔥🔥
See Section 22.1 — this **NULL trap** question is one of the most commonly used "gotcha" questions to separate junior from senior candidates. Get this one perfect.

### 21. How would you find duplicate records in a table, and how would you delete them keeping only one copy? 🔥🔥🔥
See Section 19, Q15–Q16 — the `ROW_NUMBER() OVER (PARTITION BY ...)` deletion pattern is essential.

### 22. What is denormalization, and when would you use it? 🔥
See Section 17.4.

### 23. How do you optimize a slow-running query? 🔥🔥
See Section 18.2–18.3 — structure your answer as a checklist ("First I'd check the execution plan for full scans, then check indexes on filter/join columns, then check for functions wrapping indexed columns...").

### 24. What is the difference between a Composite Key, Candidate Key, and Super Key? 🔥
See Section 2.6.

### 25. Write a query to find employees who joined in the same month as their manager. 🔥 (Scenario/Combination question)
```sql
SELECT e.emp_name, m.emp_name AS manager
FROM Employee e JOIN Employee m ON e.manager_id = m.emp_id
WHERE MONTH(e.hire_date) = MONTH(m.hire_date);
```
**Why this question is asked:** It forces you to combine a **self-join** with a **date function** in one query — a good test of whether concepts are actually connected in your head, not just memorized in isolation.

---

# SECTION 24 — COMMON SQL ERRORS & FIXES

| Error Type | Example | Cause | Fix |
|---|---|---|---|
| **Syntax Error** | `SELCT * FROM Employee` | Typo/malformed statement | Check keyword spelling, comma placement, matching parentheses |
| **Ambiguous Column** | `SELECT emp_id FROM Employee JOIN Department` (both have similar columns) | Column name exists in multiple joined tables | Prefix with table alias: `e.emp_id` |
| **Constraint Violation** | `INSERT ... dept_id = 99` | `99` doesn't exist in `Department` (FK violation) | Insert the parent row first, or verify the value exists |
| **NOT NULL Violation** | `INSERT INTO Employee (emp_id) VALUES (20)` | Required column `emp_name` omitted | Supply a value or make the column nullable/give it a DEFAULT |
| **Data Type Mismatch** | `WHERE hire_date = '2023'` | Comparing a DATE column to an incomplete/wrong-type string | Use a properly formatted date literal or explicit `CAST` |
| **GROUP BY Error** | `SELECT emp_name, dept_id, SUM(salary) FROM Employee GROUP BY dept_id` | `emp_name` isn't grouped or aggregated | Add `emp_name` to `GROUP BY` or remove it from `SELECT` |
| **Subquery Returns >1 Row** | `WHERE salary = (SELECT salary FROM Employee WHERE dept_id = 10)` | Scalar subquery unexpectedly returns multiple rows | Use `IN`, `ANY`, or add more filtering to make it return one row |
| **Division by Zero** | `salary / bonus` where `bonus = 0` | Arithmetic error at runtime | Wrap divisor in `NULLIF(bonus, 0)` |
| **Deadlock** | Two transactions cross-locking rows | Circular wait between transactions | Always acquire locks in a consistent order; keep transactions short |
| **Full Table Scan on Large Table** | `WHERE UPPER(emp_name) = 'AARAV SHARMA'` | Function on indexed column disables index usage | Store/compare in consistent case, or use a function-based index |
| **Implicit Conversion Kills Index** | `WHERE emp_id = '5'` (emp_id is INT) | Comparing INT column to a string literal | Match data types exactly in comparisons |

---

# SECTION 25 — SQL CHEAT SHEET (One-Page Revision)

### Commands by Category
| Category | Commands |
|---|---|
| DDL | `CREATE, ALTER, DROP, TRUNCATE, RENAME` |
| DML | `INSERT, UPDATE, DELETE, MERGE` |
| DQL | `SELECT` |
| DCL | `GRANT, REVOKE` |
| TCL | `COMMIT, ROLLBACK, SAVEPOINT` |

### Logical Execution Order
```
FROM → JOIN → WHERE → GROUP BY → HAVING → SELECT → DISTINCT → ORDER BY → LIMIT
```

### Joins Quick Reference
| Join | Returns |
|---|---|
| INNER | Only matching rows in both tables |
| LEFT | All left rows + matches (unmatched → NULL) |
| RIGHT | All right rows + matches (unmatched → NULL) |
| FULL | All rows from both (unmatched either side → NULL) |
| CROSS | Cartesian product (all × all) |
| SELF | Table joined to itself (aliases required) |

### Operators
`=, <>, >, <, IN, NOT IN, BETWEEN, LIKE, ILIKE, IS NULL, EXISTS, ANY, ALL`

### Aggregate Functions
`COUNT(), SUM(), AVG(), MIN(), MAX()`

### Window Functions
| Function | Purpose |
|---|---|
| `ROW_NUMBER()` | Unique sequential number, ties broken arbitrarily |
| `RANK()` | Same rank for ties, next rank skips |
| `DENSE_RANK()` | Same rank for ties, next rank doesn't skip |
| `NTILE(n)` | Splits rows into `n` buckets |
| `LAG()/LEAD()` | Access previous/next row's value |
| `FIRST_VALUE()/LAST_VALUE()` | First/last value in the window (mind the frame!) |
| `SUM()/AVG() OVER()` | Running totals / moving averages |

### NULL Functions
| MySQL | Oracle | SQL Server | ANSI-portable |
|---|---|---|---|
| `IFNULL(a,b)` | `NVL(a,b)` | `ISNULL(a,b)` | `COALESCE(a,b,...)` |

### Set Operations
`UNION (dedupes), UNION ALL (keeps dupes), INTERSECT, EXCEPT/MINUS`

### Normal Forms
`1NF → atomic values | 2NF → no partial dependency | 3NF → no transitive dependency | BCNF → every determinant is a candidate key`

### Transaction Isolation Levels (weakest → strongest)
`Read Uncommitted → Read Committed → Repeatable Read → Serializable`

### Index Types
`Clustered, Non-Clustered, Composite, Unique, B-Tree, Hash, Bitmap, Covering, Partial`

### DDL vs DML vs DQL vs TCL vs DCL
| Type | Full Form | Examples |
|---|---|---|
| DDL | Data Definition Language | CREATE, ALTER, DROP |
| DML | Data Manipulation Language | INSERT, UPDATE, DELETE |
| DQL | Data Query Language | SELECT |
| TCL | Transaction Control Language | COMMIT, ROLLBACK |
| DCL | Data Control Language | GRANT, REVOKE |

---

# SECTION 26 — LAST-MINUTE REVISION (Night Before the Interview)

## ✅ Top 15 Concepts You MUST Be Able to Explain Cold
1. Logical order of SQL execution (Section 1.5)
2. All JOIN types with a diagram (Section 8)
3. RANK vs DENSE_RANK vs ROW_NUMBER, with the tie example (Section 12.2)
4. WHERE vs HAVING (Section 7.2)
5. DELETE vs TRUNCATE vs DROP (Section 2.3)
6. NOT IN vs NOT EXISTS and the NULL trap (Section 22.1)
7. Correlated vs non-correlated subqueries (Section 9.3)
8. ACID properties with a bank-transfer example (Section 15.1)
9. Normalization up to 3NF with the Employee/Department example (Section 17.3)
10. Clustered vs non-clustered index (Section 14.2)
11. UNION vs UNION ALL (Section 10)
12. Recursive CTE for a manager hierarchy (Section 11.3)
13. Window function frame trap with LAST_VALUE (Section 12.5)
14. Primary Key vs Foreign Key vs Unique Key vs Composite Key (Sections 2.5–2.6)
15. Isolation levels and the 3 read phenomena (Section 15.3)

## ✅ Top 10 Queries to Be Able to Write From Memory, No Hesitation
1. Nth highest salary (`DENSE_RANK` method) — Section 19, Q2
2. Second highest salary (MAX-subquery method) — Section 19, Q1
3. Find and delete duplicate rows keeping one copy — Section 19, Q15–Q16
4. 2nd highest salary **per department** — Section 19, Q5
5. Employees earning more than their manager (self-join) — Section 19, Q6
6. Departments with no employees (LEFT JOIN + IS NULL) — Section 19, Q18
7. Running total with `SUM() OVER (ORDER BY ...)` — Section 19, Q26
8. Consecutive streak detection ("islands and gaps") — Section 19, Q29
9. Recursive employee hierarchy — Section 11.3
10. Pivot via `CASE WHEN` + `SUM()` — Section 19, Q38

## ✅ Top 8 "X vs Y" Comparisons — rapid fire
`NOT IN vs NOT EXISTS` · `WHERE vs HAVING` · `DELETE vs TRUNCATE vs DROP` · `UNION vs UNION ALL` · `RANK vs DENSE_RANK` · `Clustered vs Non-Clustered Index` · `Correlated vs Non-Correlated Subquery` · `View vs Materialized View`

## ✅ Interview-Day Mindset Tips
- Always state your **assumptions out loud** before writing a query ("I'm assuming 'active customer' means at least one order in the last 90 days").
- After writing a query, **narrate it back** line by line — interviewers weight communication almost as heavily as correctness.
- If stuck, talk through the **logical execution order** (FROM→WHERE→GROUP BY→HAVING→SELECT) — it almost always points you toward the fix.
- Mention **edge cases unprompted**: NULLs, ties, empty groups, duplicate keys — this alone puts you ahead of 80% of candidates.
- If a query "doesn't run" in your head, **say what you'd check first** (typos, table aliases, aggregate placement) rather than going silent.

---

## 🎯 Final Word

This handbook covers SQL from absolute fundamentals through recursive CTEs, window-function frame traps, and TCS's favorite NULL-handling gotchas — everything needed for TCS Prime, TCS Digital, TCS Ninja, and general product-based interviews. Revise Sections 23, 25, and 26 the night before; keep Section 0's sample data open while practicing every query in Section 19.

**All the best for your interview! 🚀**
