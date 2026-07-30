# TCS Prime DBMS Interview Handbook
### The Complete 100-Question Guide for TCS Prime, Digital & Ninja Technical Interviews

*Prepared for one-day-before revision — concise, interview-ready answers, no textbook fluff.*

---

## Table of Contents

| S.No | Topic | No. of Questions | Difficulty |
|---|---|---|---|
| 1 | Introduction to DBMS | 9 | Easy |
| 2 | Architecture & Data Models | 9 | Easy |
| 3 | ER Model | 9 | Easy |
| 4 | Keys | 8 | Easy |
| 5 | Functional Dependency | 4 | Medium |
| 6 | Normalization | 6 | Medium |
| 7 | SQL Concepts | 5 | Medium |
| 8 | SQL Queries (incl. Advanced SQL) | 9 | Medium |
| 9 | Joins | 6 | Medium |
| 10 | Transactions & ACID | 5 | Medium |
| 11 | Concurrency Control | 4 | Hard |
| 12 | Locking Protocols | 3 | Hard |
| 13 | Indexing | 4 | Hard |
| 14 | Query Processing | 2 | Hard |
| 15 | Recovery Techniques | 3 | Hard |
| 16 | Distributed Databases | 3 | Hard |
| 17 | NoSQL & MongoDB Basics | 5 | Medium |
| 18 | Scenario-Based Questions | 6 | Hard |
| **Total** | | **100** | Easy: 35 · Medium: 40 · Hard: 25 |

⭐ A separate **Top 30 Most Frequently Asked DBMS Questions in TCS** rapid-revision section is included at the end of this handbook.

**How to use this handbook:** Go topic by topic in order. Each answer is written exactly the way you should say it out loud in the interview — 4 to 5 lines, no rambling. If the interviewer asks a follow-up, it's usually one of the comparison points already built into the answer.

---

## 1. Introduction to DBMS

## Question 1
**Topic:** Introduction to DBMS
**Difficulty:** Easy

**Interview Question:** What is a database?

**Answer:**
A database is an organized collection of related data stored electronically so it can be easily accessed, managed, and updated. It's structured in tables, documents, or other formats depending on the database type. The data is stored in a way that avoids unnecessary duplication. Example: a college database storing student, course, and faculty details.

---

## Question 2
**Topic:** Introduction to DBMS
**Difficulty:** Easy

**Interview Question:** What is DBMS?

**Answer:**
DBMS (Database Management System) is software that lets us create, store, retrieve, and manage data in a database efficiently and securely. It sits between the user/application and the actual data, so users never touch raw files directly. It handles concurrent access, enforces constraints, and provides backup/recovery. Examples: MySQL, Oracle, PostgreSQL, SQL Server.

---

## Question 3
**Topic:** Introduction to DBMS
**Difficulty:** Easy

**Interview Question:** What are the characteristics of DBMS?

**Answer:**
DBMS provides data abstraction (hides storage details), data independence, controlled redundancy, and multi-user concurrent access. It enforces integrity constraints and provides security through user permissions. It also supports backup and recovery mechanisms. Together these make data management reliable instead of ad-hoc.

---

## Question 4
**Topic:** Introduction to DBMS
**Difficulty:** Easy

**Interview Question:** What are the advantages of DBMS?

**Answer:**
DBMS reduces data redundancy and inconsistency by centralizing data. It enforces data integrity through constraints and supports concurrent multi-user access safely. It provides security via authentication and role-based permissions. It also offers backup, recovery, and easy querying through SQL instead of custom file-handling code.

---

## Question 5
**Topic:** Introduction to DBMS
**Difficulty:** Easy

**Interview Question:** What are the disadvantages of DBMS?

**Answer:**
DBMS software is costly to set up and needs skilled DBAs to maintain. It has higher hardware and memory requirements than plain file systems. Complexity increases for very simple applications where a full DBMS is overkill. There's also a single point of failure risk if the database server goes down.

---

## Question 6
**Topic:** Introduction to DBMS
**Difficulty:** Easy

**Interview Question:** What are the applications of DBMS?

**Answer:**
DBMS is used in banking (transactions, accounts), airline and railway reservation systems, e-commerce (inventory, orders), healthcare (patient records), and telecom (billing, call records). Basically any system that needs structured, consistent, concurrent access to data relies on a DBMS. TCS itself builds many such enterprise systems for clients.

---

## Question 7
**Topic:** Introduction to DBMS
**Difficulty:** Easy

**Interview Question:** DBMS vs File System — what's the difference?

**Answer:**
A file system stores data in flat files with no built-in relationships, so redundancy and inconsistency are common. DBMS stores data in related tables with constraints, enforcing integrity automatically. File systems have no real concurrency control, while DBMS supports safe concurrent access via transactions and locks. DBMS also provides security, backup/recovery, and a query language (SQL); file systems require custom code for all of this.

---

## Question 8
**Topic:** Introduction to DBMS
**Difficulty:** Easy

**Interview Question:** What are the types of DBMS?

**Answer:**
Hierarchical DBMS (tree structure, e.g., IMS), Network DBMS (graph structure with multiple parent-child links), Relational DBMS (tables with rows/columns, e.g., MySQL, Oracle — most widely used), and Object-Oriented DBMS (data as objects, e.g., db4o). Modern applications mostly use RDBMS, with NoSQL databases as a newer non-relational category.

---

## Question 9
**Topic:** Introduction to DBMS
**Difficulty:** Easy

**Interview Question:** What are the main components of DBMS?

**Answer:**
Hardware (servers, storage), Software (the DBMS engine itself), Data (the actual stored data plus metadata), Procedures (rules/instructions for use), and Users (DBAs, application programmers, end users). The Query Processor and Storage Manager are the two key internal engine components that handle query execution and physical data storage respectively.

---

## 2. Architecture & Data Models

## Question 10
**Topic:** Architecture & Data Models
**Difficulty:** Easy

**Interview Question:** What is one-tier architecture?

**Answer:**
In one-tier architecture, the database is directly available to the user on the same machine — the client, server, and database all reside together. It's mainly used for local development and testing, like using SQLite or a local MS Access file. There's no network involved, so it's fast but not suitable for multi-user production systems.

---

## Question 11
**Topic:** Architecture & Data Models
**Difficulty:** Easy

**Interview Question:** What is two-tier architecture?

**Answer:**
Two-tier architecture has a client (application) directly communicating with the database server over a network, typically via ODBC/JDBC. The client handles the UI and business logic, while the server handles storage and queries. It's simple and fast for small systems but doesn't scale well since business logic is duplicated across clients.

---

## Question 12
**Topic:** Architecture & Data Models
**Difficulty:** Easy

**Interview Question:** What is three-tier architecture?

**Answer:**
Three-tier architecture adds a middle application/business logic layer between the client and the database server. The client only handles presentation, the middle tier handles business logic and processing, and the database tier handles storage. This is what most web applications use — it's more scalable, secure, and maintainable since logic is centralized in one layer instead of every client.

---

## Question 13
**Topic:** Architecture & Data Models
**Difficulty:** Easy

**Interview Question:** What is a schema in DBMS?

**Answer:**
A schema is the overall logical structure or design of the database — the tables, columns, data types, and relationships — defined at the time of database design. It's like a blueprint and doesn't change frequently. Example: a "Student" table schema defining columns like roll_no, name, and department.

---

## Question 14
**Topic:** Architecture & Data Models
**Difficulty:** Easy

**Interview Question:** What is an instance in DBMS?

**Answer:**
An instance is the actual data stored in the database at a particular moment in time. While schema is the structure, instance is the content — it keeps changing as records are inserted, updated, or deleted. Example: the actual rows of student records present right now.

---

## Question 15
**Topic:** Architecture & Data Models
**Difficulty:** Easy

**Interview Question:** Schema vs Instance — what's the difference?

**Answer:**
Schema is the fixed structural design of the database (tables, columns, constraints), defined once during design and rarely changed. Instance is the actual data present in the database at a given point in time, which changes constantly with every insert/update/delete. Schema is like a class definition; instance is like the objects created from it.

---

## Question 16
**Topic:** Architecture & Data Models
**Difficulty:** Easy

**Interview Question:** What is data independence?

**Answer:**
Data independence is the capacity to change the schema at one level of the database without affecting the schema at the next higher level. It lets us modify storage or structure without rewriting application code. This is achieved through the three-level (ANSI-SPARC) architecture: physical, logical, and view levels.

---

## Question 17
**Topic:** Architecture & Data Models
**Difficulty:** Easy

**Interview Question:** What are the types of data independence?

**Answer:**
Logical data independence means we can change the logical schema (e.g., add a new table or column) without affecting application programs that use the view/external level. Physical data independence means we can change the physical storage (like moving to a different disk or changing indexing) without changing the logical schema. Logical independence is harder to achieve than physical, since applications are more tightly coupled to the logical schema.

---

## Question 18
**Topic:** Architecture & Data Models
**Difficulty:** Easy

**Interview Question:** What is data abstraction and what are its levels?

**Answer:**
Data abstraction hides the complexity of how data is physically stored, showing users only what they need. There are three levels: Physical level (how data is actually stored on disk), Logical level (what data is stored and the relationships between them — this is where the schema lives), and View level (what each specific user or application sees, a customized subset). This layering is what enables data independence.

---

## 3. ER Model

## Question 19
**Topic:** ER Model
**Difficulty:** Easy

**Interview Question:** What is an entity and an entity set?

**Answer:**
An entity is a real-world object that can be distinctly identified, like a specific student or a specific product. An entity set is a collection of similar entities that share the same attributes, like the set of all students. In the relational model, an entity set typically becomes a table, and each entity becomes a row.

---

## Question 20
**Topic:** ER Model
**Difficulty:** Easy

**Interview Question:** Weak entity vs Strong entity — what's the difference?

**Answer:**
A strong entity has its own primary key and can exist independently, like a Student entity. A weak entity does not have a sufficient primary key of its own and depends on a strong (owner) entity for identification, using a partial key plus the owner's key. Example: "Dependent" of an employee is a weak entity — it can't exist without the Employee entity, and is identified using employee_id plus dependent_name.

---

## Question 21
**Topic:** ER Model
**Difficulty:** Easy

**Interview Question:** What are attributes and what types exist?

**Answer:**
Attributes are properties that describe an entity, like name or age for a Student. Types include: Simple (atomic, can't be divided, e.g., age), Composite (can be broken into parts, e.g., address into street/city), Derived (calculated from other attributes, e.g., age from date of birth), and Multivalued (can hold more than one value, e.g., phone numbers).

---

## Question 22
**Topic:** ER Model
**Difficulty:** Easy

**Interview Question:** What is a relationship in the ER model?

**Answer:**
A relationship represents an association between two or more entities, like a Student "enrolls in" a Course. It's shown as a diamond in an ER diagram connecting the related entity rectangles. Relationships can themselves have attributes, like an "enrollment date" on the enrolls-in relationship. In the relational schema, relationships often become foreign keys or, for many-to-many cases, a separate junction table.

---

## Question 23
**Topic:** ER Model
**Difficulty:** Easy

**Interview Question:** What is cardinality in ER model?

**Answer:**
Cardinality defines the number of instances of one entity that can be associated with instances of another entity in a relationship. The types are one-to-one (1:1), one-to-many (1:N), and many-to-many (M:N). Example: one Department has many Employees (1:N), while a Student can enroll in many Courses and a Course can have many Students (M:N).

---

## Question 24
**Topic:** ER Model
**Difficulty:** Easy

**Interview Question:** What are participation constraints?

**Answer:**
Participation constraints define whether every entity in an entity set must participate in a relationship (total participation) or only some do (partial participation). Total participation is shown with a double line in ER diagrams, meaning every instance must be involved — like every Employee must belong to some Department. Partial participation means involvement is optional, like not every Employee necessarily manages a project.

---

## Question 25
**Topic:** ER Model
**Difficulty:** Easy

**Interview Question:** What is a composite attribute, and how is it different from a multivalued attribute?

**Answer:**
A composite attribute can be divided into smaller sub-parts that each have independent meaning, like Address splitting into street, city, and pincode. A multivalued attribute can hold multiple values for a single entity, like a person having multiple phone numbers. Composite is about structure/decomposition, multivalued is about quantity/repetition — they solve different problems in ER modeling.

---

## Question 26
**Topic:** ER Model
**Difficulty:** Easy

**Interview Question:** What is a recursive relationship?

**Answer:**
A recursive relationship is one where an entity set is related to itself, rather than to a different entity set. Example: in an Employee entity, a "manages" relationship connects an employee to another employee (the manager). Both roles come from the same entity set, just playing different parts in the relationship.

---

## Question 27
**Topic:** ER Model
**Difficulty:** Easy

**Interview Question:** How is an ER diagram converted into relational tables?

**Answer:**
Each strong entity becomes a table with its attributes as columns and its key as the primary key. Each weak entity becomes a table that includes the owner entity's key as a foreign key, combined with its partial key. A 1:N relationship is represented by adding the "one" side's primary key as a foreign key on the "many" side. An M:N relationship needs its own separate junction table containing both entities' keys as a composite foreign key.

---

## 4. Keys

## Question 28
**Topic:** Keys
**Difficulty:** Easy

**Interview Question:** What is a super key?

**Answer:**
A super key is any set of one or more attributes that can uniquely identify a row in a table. It can contain extra attributes beyond what's strictly needed for uniqueness. Every candidate key is a super key, but not every super key is a candidate key, since super keys can have redundant attributes.

---

## Question 29
**Topic:** Keys
**Difficulty:** Easy

**Interview Question:** What is a candidate key?

**Answer:**
A candidate key is a minimal super key — it uniquely identifies a row, and no attribute can be removed from it without losing that uniqueness. A table can have multiple candidate keys. One of the candidate keys is chosen as the primary key, and the rest become alternate keys.

---

## Question 30
**Topic:** Keys
**Difficulty:** Easy

**Interview Question:** What is a primary key?

**Answer:**
A primary key is the candidate key selected to uniquely identify each row in a table. It cannot contain NULL values and must be unique across all rows. A table can have only one primary key, though that key can be composed of multiple columns (composite primary key).

---

## Question 31
**Topic:** Keys
**Difficulty:** Easy

**Interview Question:** What is an alternate key?

**Answer:**
An alternate key is a candidate key that was not chosen as the primary key. Example: if a Student table has both roll_no and email as candidate keys, and roll_no is chosen as primary key, then email becomes the alternate key. Alternate keys are still unique and can have a UNIQUE constraint applied.

---

## Question 32
**Topic:** Keys
**Difficulty:** Easy

**Interview Question:** What is a composite key?

**Answer:**
A composite key is a primary key made up of two or more columns that together uniquely identify a row, even though no single column can do it alone. Example: in an Enrollment table, (student_id, course_id) together form a composite key since a student can enroll in many courses and a course can have many students.

---

## Question 33
**Topic:** Keys
**Difficulty:** Easy

**Interview Question:** What is a foreign key?

**Answer:**
A foreign key is a column (or set of columns) in one table that references the primary key of another table, establishing a link between the two. It enforces referential integrity — you can't insert a foreign key value that doesn't exist in the referenced table. Example: department_id in an Employee table referencing the Department table's primary key.

---

## Question 34
**Topic:** Keys
**Difficulty:** Easy

**Interview Question:** What is a surrogate key?

**Answer:**
A surrogate key is an artificially generated key, usually an auto-incrementing integer or UUID, that has no business meaning and is used purely for uniquely identifying rows. It's used instead of natural keys when natural keys are too long, can change, or aren't guaranteed unique. Example: an auto-increment "id" column instead of using email as the primary key.

---

## Question 35
**Topic:** Keys
**Difficulty:** Easy

**Interview Question:** Primary Key vs Unique Key — what's the difference?

**Answer:**
A primary key cannot contain NULL values and a table can have only one primary key, which may be composite. A unique key can accept one NULL value (in most RDBMS) and a table can have multiple unique keys. Both enforce uniqueness across rows, but primary key is the main identifier used for foreign key references, while unique keys are used for enforcing uniqueness on other important columns like email or phone number.

---

## 5. Functional Dependency

## Question 36
**Topic:** Functional Dependency
**Difficulty:** Medium

**Interview Question:** What is a functional dependency?

**Answer:**
A functional dependency X → Y means that the value of attribute X uniquely determines the value of attribute Y — for every value of X, there's exactly one corresponding value of Y. Example: roll_no → name, since a roll number determines exactly one student name. Functional dependencies are the foundation used to decide normal forms.

---

## Question 37
**Topic:** Functional Dependency
**Difficulty:** Medium

**Interview Question:** Trivial vs Non-trivial functional dependency — what's the difference?

**Answer:**
A functional dependency X → Y is trivial if Y is a subset of X — it's automatically true and adds no new information, like {roll_no, name} → name. It's non-trivial if Y is not a subset of X, meaning it gives genuinely new information, like roll_no → name. Normalization mainly cares about non-trivial dependencies since those are what create redundancy issues.

---

## Question 38
**Topic:** Functional Dependency
**Difficulty:** Medium

**Interview Question:** What is closure of a set of attributes?

**Answer:**
The closure of an attribute set X, written X+, is the set of all attributes that can be functionally determined by X using the given functional dependencies. It's computed by repeatedly applying the FDs until no new attributes can be added. Closure is used to check if a set of attributes is a candidate key — if X+ covers all attributes of the relation, X is a super key.

---

## Question 39
**Topic:** Functional Dependency
**Difficulty:** Medium

**Interview Question:** What are Armstrong's Axioms?

**Answer:**
Armstrong's Axioms are inference rules used to derive all functional dependencies logically implied by a given set. The three basic rules are: Reflexivity (if Y is a subset of X, then X → Y), Augmentation (if X → Y, then XZ → YZ for any Z), and Transitivity (if X → Y and Y → Z, then X → Z). These are proven to be both sound and complete for deriving FDs.

---

## 6. Normalization

## Question 40
**Topic:** Normalization
**Difficulty:** Medium

**Interview Question:** Why do we need normalization?

**Answer:**
Normalization is the process of organizing tables to reduce data redundancy and avoid update, insert, and delete anomalies. Without it, the same data gets repeated across rows, so updating it in one place but missing another causes inconsistency. It works by breaking large tables into smaller related tables based on functional dependencies. The trade-off is more joins at query time, but much better data integrity.

---

## Question 41
**Topic:** Normalization
**Difficulty:** Medium

**Interview Question:** What is 1NF (First Normal Form)?

**Answer:**
A table is in 1NF if every column contains only atomic (indivisible) values and there are no repeating groups or multivalued columns. Example: a "phone_numbers" column storing "9876543210, 9123456789" in one cell violates 1NF — it needs to be split into separate rows or a separate table. 1NF is the baseline requirement before any other normal form applies.

---

## Question 42
**Topic:** Normalization
**Difficulty:** Medium

**Interview Question:** What is 2NF (Second Normal Form)?

**Answer:**
A table is in 2NF if it's already in 1NF and has no partial dependency — meaning no non-key attribute depends on only part of a composite primary key. This issue only arises when the primary key is composite. Example: in a table with key (student_id, course_id), if student_name depends only on student_id and not on the full key, that's a partial dependency violating 2NF, so student_name should move to a separate Student table.

---

## Question 43
**Topic:** Normalization
**Difficulty:** Medium

**Interview Question:** What is 3NF (Third Normal Form)?

**Answer:**
A table is in 3NF if it's in 2NF and has no transitive dependency — meaning no non-key attribute depends on another non-key attribute. Example: in a Student table, if student_id → department_id and department_id → department_name, then department_name transitively depends on student_id through department_id, violating 3NF. The fix is moving department_name into a separate Department table.

---

## Question 44
**Topic:** Normalization
**Difficulty:** Medium

**Interview Question:** What is BCNF, and how is it different from 3NF?

**Answer:**
BCNF is a stricter version of 3NF — a table is in BCNF if for every functional dependency X → Y, X must be a super key. 3NF allows one exception: it permits X → Y even if X is not a super key, as long as Y is a prime attribute (part of some candidate key). BCNF removes that exception, so it handles some anomalies 3NF misses, but it can sometimes cause loss of a functional dependency during decomposition, which 3NF avoids.

---

## Question 45
**Topic:** Normalization
**Difficulty:** Medium

**Interview Question:** What are 4NF, 5NF, and denormalization?

**Answer:**
4NF removes multivalued dependencies — where one key determines multiple independent sets of values, causing redundancy even in BCNF tables. 5NF (Project-Join Normal Form) removes join dependencies, ensuring a table can't be losslessly decomposed further. Denormalization is the deliberate reverse process — merging normalized tables back together to reduce joins and improve read performance, commonly done in reporting/analytics systems where read speed matters more than write-time redundancy.

---

## 7. SQL Concepts

## Question 46
**Topic:** SQL Concepts
**Difficulty:** Medium

**Interview Question:** What are DDL, DML, DCL, and TCL?

**Answer:**
DDL (Data Definition Language) defines database structure — CREATE, ALTER, DROP, TRUNCATE. DML (Data Manipulation Language) manipulates data — SELECT, INSERT, UPDATE, DELETE. DCL (Data Control Language) manages permissions — GRANT, REVOKE. TCL (Transaction Control Language) manages transactions — COMMIT, ROLLBACK, SAVEPOINT. DDL commands auto-commit in most databases, while DML changes need explicit commit unless auto-commit mode is on.

---

## Question 47
**Topic:** SQL Concepts
**Difficulty:** Medium

**Interview Question:** What are constraints in SQL, and what types exist?

**Answer:**
Constraints are rules enforced on table columns to maintain data accuracy and integrity. Key types: NOT NULL (column can't be empty), UNIQUE (no duplicate values), PRIMARY KEY (unique + not null, identifies rows), FOREIGN KEY (enforces a valid reference to another table), CHECK (restricts values to a condition, like age > 0), and DEFAULT (auto-fills a value when none is provided).

---

## Question 48
**Topic:** SQL Concepts
**Difficulty:** Medium

**Interview Question:** How does SQL handle NULL values?

**Answer:**
NULL represents an unknown or missing value — it's not the same as zero or an empty string. Any arithmetic or comparison with NULL returns NULL, not true or false, so we must use IS NULL or IS NOT NULL instead of = NULL. Aggregate functions like COUNT, SUM, and AVG ignore NULL values by default, except COUNT(*) which counts all rows regardless of NULLs.

---

## Question 49
**Topic:** SQL Concepts
**Difficulty:** Medium

**Interview Question:** What are DEFAULT and CHECK constraints?

**Answer:**
DEFAULT automatically assigns a specified value to a column when no value is provided during an insert, like defaulting a "status" column to 'active'. CHECK enforces that a column's value satisfies a Boolean condition before it's accepted, like CHECK (age >= 18). Both constraints are validated at the database level, so bad data is rejected even if the application layer has a bug.

---

## Question 50
**Topic:** SQL Concepts
**Difficulty:** Medium

**Interview Question:** DELETE vs TRUNCATE vs DROP — what's the difference?

**Answer:**
DELETE is a DML command that removes specific rows based on a WHERE condition, can be rolled back, and fires triggers — but it's slower since it logs each row. TRUNCATE is a DDL command that removes all rows at once, resets identity/auto-increment counters, is much faster, but generally cannot be rolled back once committed in most databases. DROP is a DDL command that removes the entire table structure along with its data permanently. In short: DELETE removes rows selectively, TRUNCATE empties the whole table fast, DROP deletes the table itself.

---

## 8. SQL Queries (Basic & Advanced)

## Question 51
**Topic:** SQL Queries
**Difficulty:** Medium

**Interview Question:** Explain SELECT and WHERE clauses.

**Answer:**
SELECT retrieves specific columns from a table, and WHERE filters which rows are returned based on a condition. Example: SELECT name, age FROM Student WHERE age > 20; returns only students older than 20. WHERE is evaluated row by row before any grouping happens, and it cannot use aggregate functions directly — that's what HAVING is for.

---

## Question 52
**Topic:** SQL Queries
**Difficulty:** Medium

**Interview Question:** Explain GROUP BY and HAVING.

**Answer:**
GROUP BY groups rows that share the same value in specified columns, typically used with aggregate functions like COUNT, SUM, or AVG. HAVING filters those grouped results based on a condition, similar to WHERE but applied after grouping and able to use aggregate functions. Example: SELECT dept, COUNT(*) FROM Employee GROUP BY dept HAVING COUNT(*) > 5; shows only departments with more than 5 employees.

---

## Question 53
**Topic:** SQL Queries
**Difficulty:** Medium

**Interview Question:** Explain ORDER BY and LIMIT.

**Answer:**
ORDER BY sorts the result set by one or more columns, ascending (ASC, default) or descending (DESC). LIMIT restricts the number of rows returned, commonly used for pagination or top-N queries. Example: SELECT * FROM Employee ORDER BY salary DESC LIMIT 5; returns the top 5 highest-paid employees. ORDER BY is always applied after WHERE/GROUP BY/HAVING, and LIMIT is applied last.

---

## Question 54
**Topic:** SQL Queries
**Difficulty:** Medium

**Interview Question:** What does DISTINCT do?

**Answer:**
DISTINCT removes duplicate rows from the result set, keeping only unique combinations of the selected columns. Example: SELECT DISTINCT department FROM Employee; returns each department name only once, even if hundreds of employees belong to it. It's applied to the full row of selected columns together, not to each column independently.

---

## Question 55
**Topic:** SQL Queries
**Difficulty:** Medium

**Interview Question:** What is a View, and how is it different from a Table?

**Answer:**
A view is a virtual table based on the result of a stored SQL query — it doesn't physically store data itself, just the query definition. A table physically stores actual data on disk. Views are used to simplify complex queries, restrict column/row access for security, and present a customized subset of data. Updating a view can update the underlying table only under certain conditions (simple, single-table views); complex views with joins or aggregates are often read-only.

---

## Question 56
**Topic:** SQL Queries
**Difficulty:** Medium

**Interview Question:** Stored Procedure vs Function — what's the difference?

**Answer:**
A stored procedure is a precompiled set of SQL statements that can perform actions like insert/update/delete and may or may not return a value; it's called using CALL/EXEC. A function must return exactly one value and can be used directly inside a SQL expression, like in a SELECT statement. Functions generally can't modify data (no DML that changes state in most databases) while procedures can perform any operation, including transaction control.

---

## Question 57
**Topic:** SQL Queries
**Difficulty:** Medium

**Interview Question:** What is a Trigger?

**Answer:**
A trigger is a block of code that automatically executes in response to a specific event on a table, like BEFORE or AFTER an INSERT, UPDATE, or DELETE. It's used to enforce business rules, maintain audit logs, or keep derived data in sync automatically. Example: a trigger that logs every salary change into an audit table whenever an UPDATE happens on the Employee table.

---

## Question 58
**Topic:** SQL Queries
**Difficulty:** Medium

**Interview Question:** Nested Subquery vs Correlated Subquery — what's the difference?

**Answer:**
A nested (simple) subquery executes once, independently of the outer query, and its result is used by the outer query — like finding employees earning more than the average salary using a subquery that runs a single time. A correlated subquery references a column from the outer query, so it runs once for every row processed by the outer query, which makes it slower on large tables. Example: finding employees who earn more than the average salary of their own department needs a correlated subquery since "their department" changes per row.

---

## Question 59
**Topic:** SQL Queries
**Difficulty:** Medium

**Interview Question:** Explain EXISTS, ANY, and ALL operators.

**Answer:**
EXISTS checks whether a subquery returns any rows at all, returning true/false — it's efficient since it stops as soon as one match is found. ANY compares a value against each value returned by a subquery and is true if the condition holds for at least one of them (e.g., salary > ANY(...)). ALL is true only if the condition holds for every value returned by the subquery (e.g., salary > ALL(...) means greater than the maximum). EXISTS is generally preferred over IN for large subquery results due to better performance.

---

## 9. Joins

## Question 60
**Topic:** Joins
**Difficulty:** Medium

**Interview Question:** What is an INNER JOIN?

**Answer:**
INNER JOIN returns only the rows where there's a match in both tables based on the join condition. Rows that don't have a matching row in the other table are excluded from the result entirely. Example: joining Employee and Department on department_id returns only employees who have a valid, existing department. It's the most commonly used join type.

---

## Question 61
**Topic:** Joins
**Difficulty:** Medium

**Interview Question:** LEFT JOIN vs RIGHT JOIN — what's the difference?

**Answer:**
LEFT JOIN returns all rows from the left table plus matching rows from the right table — unmatched right-side columns come back as NULL. RIGHT JOIN does the opposite: all rows from the right table plus matches from the left, with unmatched left-side columns as NULL. Example: LEFT JOIN Employee with Department keeps all employees even if some have no department assigned. RIGHT JOIN is rarely used in practice since you can always rewrite it as a LEFT JOIN by swapping table order.

---

## Question 62
**Topic:** Joins
**Difficulty:** Medium

**Interview Question:** What is a FULL OUTER JOIN?

**Answer:**
FULL OUTER JOIN returns all rows from both tables, matching them where possible and filling in NULLs where there's no match on either side. It's essentially the combination of LEFT JOIN and RIGHT JOIN results. Example: it would show all employees (even without a department) and all departments (even without employees) in one result set. Note that MySQL doesn't support FULL OUTER JOIN directly — it's usually simulated with a UNION of LEFT and RIGHT JOIN.

---

## Question 63
**Topic:** Joins
**Difficulty:** Medium

**Interview Question:** What is a SELF JOIN?

**Answer:**
A self join is when a table is joined with itself, treated as if it were two separate tables using aliases. It's used when rows in a table have a relationship with other rows in the same table. Example: finding each employee's manager name, where both employee and manager are stored in the same Employee table, requires joining Employee e1 with Employee e2 on e1.manager_id = e2.employee_id.

---

## Question 64
**Topic:** Joins
**Difficulty:** Medium

**Interview Question:** What is a CROSS JOIN?

**Answer:**
A CROSS JOIN returns the Cartesian product of two tables — every row of the first table combined with every row of the second table, with no join condition. If Table A has 3 rows and Table B has 4 rows, the result has 12 rows. It's rarely used intentionally except for generating combinations, like pairing every size with every color for product variants; using it accidentally (by forgetting a join condition) is a common bug.

---

## Question 65
**Topic:** Joins
**Difficulty:** Medium

**Interview Question:** What is a NATURAL JOIN?

**Answer:**
A NATURAL JOIN automatically joins two tables based on all columns that share the same name and data type, without explicitly specifying the join condition. It's risky in practice because if the tables later gain a new column with a matching name, the join behavior silently changes. Most production code prefers explicit INNER JOIN ... ON conditions instead of NATURAL JOIN for this reason.

---

## 10. Transactions & ACID

## Question 66
**Topic:** Transactions & ACID
**Difficulty:** Medium

**Interview Question:** What is a transaction in DBMS?

**Answer:**
A transaction is a single logical unit of work made up of one or more database operations, which must either fully complete or have no effect at all. Example: transferring money between two bank accounts involves a debit and a credit — both must succeed together, or neither should happen. Transactions move the database from one consistent state to another.

---

## Question 67
**Topic:** Transactions & ACID
**Difficulty:** Medium

**Interview Question:** What are the ACID properties?

**Answer:**
Atomicity ensures a transaction is all-or-nothing — either every operation completes or none do. Consistency ensures the database moves from one valid state to another, respecting all constraints. Isolation ensures concurrent transactions don't interfere with each other's intermediate results. Durability ensures that once a transaction is committed, its changes survive even a system crash. These four properties together guarantee reliable transaction processing, which is why they're critical in banking systems.

---

## Question 68
**Topic:** Transactions & ACID
**Difficulty:** Medium

**Interview Question:** What are COMMIT and ROLLBACK?

**Answer:**
COMMIT permanently saves all the changes made during the current transaction to the database, making them visible to other users. ROLLBACK undoes all the changes made in the current transaction, reverting the database back to its state before the transaction began. They're both TCL commands used to control transaction outcomes — COMMIT on success, ROLLBACK when an error occurs mid-transaction.

---

## Question 69
**Topic:** Transactions & ACID
**Difficulty:** Medium

**Interview Question:** What is a SAVEPOINT?

**Answer:**
A SAVEPOINT is a marker set within a transaction that lets you roll back part of the transaction without undoing the entire thing. You can roll back to a specific savepoint using ROLLBACK TO SAVEPOINT, keeping earlier changes intact. It's useful in long transactions where you want partial recovery from an error instead of restarting from scratch.

---

## Question 70
**Topic:** Transactions & ACID
**Difficulty:** Medium

**Interview Question:** Why is ACID important in banking systems?

**Answer:**
In banking, a fund transfer involves debiting one account and crediting another — Atomicity ensures both happen together or neither does, so money is never lost or duplicated mid-transfer. Consistency ensures account balances always respect rules like "no negative balance without overdraft." Isolation prevents two simultaneous transfers from reading stale or half-updated balances. Durability guarantees that once a transaction is confirmed to the customer, it survives even a server crash immediately after.

---

## 11. Concurrency Control

## Question 71
**Topic:** Concurrency Control
**Difficulty:** Hard

**Interview Question:** What is the Lost Update problem?

**Answer:**
Lost update happens when two transactions read the same data, and both later write their update back — the second write overwrites the first, so one transaction's update is silently lost. Example: two clerks read a stock count of 100, both subtract 10 in their own transaction, and both write back 90 instead of the correct 80. Proper locking or isolation levels prevent this by not letting the second transaction write until the first is done and re-reads happen.

---

## Question 72
**Topic:** Concurrency Control
**Difficulty:** Hard

**Interview Question:** What are Dirty Read and Phantom Read?

**Answer:**
A dirty read happens when a transaction reads data written by another transaction that hasn't been committed yet — if that other transaction rolls back, the first transaction acted on data that never really existed. A phantom read happens when a transaction re-runs a query and gets a different set of rows because another transaction inserted or deleted rows matching the condition in between. Both are concurrency anomalies that stricter isolation levels are designed to prevent.

---

## Question 73
**Topic:** Concurrency Control
**Difficulty:** Hard

**Interview Question:** What are the isolation levels in DBMS?

**Answer:**
Read Uncommitted allows dirty reads — the weakest, fastest level. Read Committed prevents dirty reads but still allows non-repeatable reads and phantoms. Repeatable Read prevents dirty and non-repeatable reads, but phantom reads can still occur in some databases. Serializable is the strictest — transactions behave as if executed one after another, preventing all anomalies but with the highest locking overhead and lowest concurrency.

---

## Question 74
**Topic:** Concurrency Control
**Difficulty:** Hard

**Interview Question:** What is serializability?

**Answer:**
Serializability is a property of a schedule of concurrent transactions that guarantees the result is equivalent to some serial (one-after-another) execution of those same transactions. Conflict serializability checks this by seeing if conflicting operations (read/write on the same data) can be reordered into a valid serial order without changing the outcome. It's the correctness benchmark used to design concurrency control protocols like 2PL.

---

## 12. Locking Protocols

## Question 75
**Topic:** Locking Protocols
**Difficulty:** Hard

**Interview Question:** Shared Lock vs Exclusive Lock — what's the difference?

**Answer:**
A shared lock (S-lock) is taken for reading data and can be held by multiple transactions simultaneously on the same item, since reads don't conflict with each other. An exclusive lock (X-lock) is taken for writing data and only one transaction can hold it on a given item at a time, blocking both reads and writes from others. This distinction is what allows multiple readers to proceed in parallel while still protecting writes.

---

## Question 76
**Topic:** Locking Protocols
**Difficulty:** Hard

**Interview Question:** What is an intention lock?

**Answer:**
An intention lock is placed on a higher level of the data hierarchy (like a table) to signal that a transaction intends to acquire a shared or exclusive lock at a lower, finer level (like a row) within it. This avoids having to scan every row to check for conflicts, making multi-granularity locking efficient. Types include Intention Shared (IS) and Intention Exclusive (IX).

---

## Question 77
**Topic:** Locking Protocols
**Difficulty:** Hard

**Interview Question:** What is Two-Phase Locking (2PL), and how does it cause deadlocks?

**Answer:**
Two-Phase Locking has a growing phase, where a transaction can only acquire locks, and a shrinking phase, where it can only release locks — once it releases one lock, it can't acquire any more. This guarantees conflict serializability. However, 2PL can lead to deadlocks when two transactions each hold a lock the other needs and both wait indefinitely — this is handled separately using deadlock detection (wait-for graphs) or prevention schemes like wait-die and wound-wait.

---

## 13. Indexing

## Question 78
**Topic:** Indexing
**Difficulty:** Hard

**Interview Question:** What is indexing and why do we need it?

**Answer:**
An index is a separate data structure that stores a sorted reference to table data, allowing the database to find rows without scanning the entire table. It dramatically speeds up SELECT queries with WHERE, JOIN, or ORDER BY on the indexed column. The trade-off is that indexes slow down INSERT/UPDATE/DELETE slightly since the index also needs updating, and they consume extra storage.

---

## Question 79
**Topic:** Indexing
**Difficulty:** Hard

**Interview Question:** Clustered Index vs Non-Clustered Index — what's the difference?

**Answer:**
A clustered index determines the actual physical order in which rows are stored on disk — so a table can have only one clustered index, usually built on the primary key. A non-clustered index is a separate structure that stores pointers back to the actual data rows, so a table can have multiple non-clustered indexes. Reading via a clustered index is generally faster since the data is right there in sorted order, while non-clustered indexes need an extra lookup step to fetch the full row.

---

## Question 80
**Topic:** Indexing
**Difficulty:** Hard

**Interview Question:** Primary Index vs Secondary Index, and Dense vs Sparse Index?

**Answer:**
A primary index is built on the primary key of a table that's already physically sorted by that key. A secondary index is built on a non-key column and is always dense, since the data isn't sorted by it. A dense index has an index entry for every single record in the table. A sparse index has an entry only for some records (usually one per data block), relying on the data being sorted to locate nearby records — this saves space but only works on sorted (typically primary-indexed) data.

---

## Question 81
**Topic:** Indexing
**Difficulty:** Hard

**Interview Question:** B-Tree vs B+ Tree — what's the difference?

**Answer:**
In a B-Tree, both internal and leaf nodes can store actual data pointers, so search paths can end at any level. In a B+ Tree, only leaf nodes store data pointers — internal nodes just store keys used for navigation, and all leaf nodes are linked together in a sorted list. This makes B+ Trees much better for range queries (like BETWEEN or ORDER BY) since you can just scan the linked leaf list, and it's why almost all real-world RDBMS indexes (MySQL InnoDB, Oracle) use B+ Trees rather than plain B-Trees. Hash indexes are also used but only for exact-match lookups, not range queries, since hashing destroys ordering.

---

## 14. Query Processing

## Question 82
**Topic:** Query Processing
**Difficulty:** Hard

**Interview Question:** What is query optimization?

**Answer:**
Query optimization is the process by which the DBMS chooses the most efficient way to execute a given SQL query out of many logically equivalent options. It considers factors like available indexes, table sizes, and join order to minimize cost (usually I/O and CPU time). The query optimizer transforms the query into an execution plan and picks the cheapest one it can estimate, using statistics collected about the data.

---

## Question 83
**Topic:** Query Processing
**Difficulty:** Hard

**Interview Question:** What is an execution plan and how is cost estimated?

**Answer:**
An execution plan is the step-by-step strategy the database engine decides to use to run a query — which indexes to use, which join algorithm, and in what order to access tables. You can view it using EXPLAIN in most databases. Cost estimation uses statistics like table row counts, index selectivity, and available memory to predict I/O and CPU cost for each candidate plan, then picks the lowest-cost one. This is why adding the right index, or updating outdated table statistics, can dramatically change a query's real-world performance.

---

## 15. Recovery Techniques

## Question 84
**Topic:** Recovery Techniques
**Difficulty:** Hard

**Interview Question:** What is log-based recovery?

**Answer:**
Log-based recovery keeps a sequential log recording every change made to the database before it's actually applied (write-ahead logging), including the old and new values. If the system crashes, the recovery manager replays this log to redo committed transactions and undo uncommitted ones, restoring a consistent state. It's the most widely used recovery technique in modern RDBMS because it doesn't require expensive full-database copies.

---

## Question 85
**Topic:** Recovery Techniques
**Difficulty:** Hard

**Interview Question:** What is shadow paging?

**Answer:**
Shadow paging maintains two page tables — a current page table for the active transaction and a shadow (original) page table left untouched. Changes are made to new copies of pages, and only when the transaction commits does the current page table replace the shadow one atomically. It avoids the need for logging and makes recovery simple, but it suffers from data fragmentation and poor support for concurrent transactions, which is why log-based recovery is far more common in practice.

---

## Question 86
**Topic:** Recovery Techniques
**Difficulty:** Hard

**Interview Question:** What are checkpoints, and what is the difference between Undo and Redo?

**Answer:**
A checkpoint is a point where the DBMS writes all its buffered/modified data to disk and records this in the log, so recovery after a crash only needs to look at logs after the last checkpoint, not from the very beginning. Redo re-applies the changes of committed transactions that might not have reached disk before a crash. Undo reverses the changes of transactions that were incomplete (uncommitted) at the time of the crash, since they shouldn't have taken effect at all.

---

## 16. Distributed Databases

## Question 87
**Topic:** Distributed Databases
**Difficulty:** Hard

**Interview Question:** What is a distributed database?

**Answer:**
A distributed database is a single logical database whose data is actually stored across multiple physical locations or servers, which may be geographically spread out, but appears as one unified database to users and applications. It improves availability and scalability, and allows data to be placed closer to where it's used. The trade-off is added complexity in keeping data consistent and coordinating transactions across nodes.

---

## Question 88
**Topic:** Distributed Databases
**Difficulty:** Hard

**Interview Question:** What is the CAP theorem?

**Answer:**
CAP theorem states that a distributed system can guarantee at most two out of three properties at the same time: Consistency (every read gets the latest write), Availability (every request gets a response, even if not the latest data), and Partition Tolerance (the system keeps working despite network partitions between nodes). Since network partitions are unavoidable in real distributed systems, the practical choice is really between consistency and availability during a partition — e.g., traditional RDBMS clusters often favor consistency, while many NoSQL systems favor availability.

---

## Question 89
**Topic:** Distributed Databases
**Difficulty:** Hard

**Interview Question:** Replication vs Partitioning — what's the difference?

**Answer:**
Replication copies the same data across multiple nodes so each node has a full copy, improving availability and read performance and providing fault tolerance if one node fails. Partitioning (sharding) splits the data itself across nodes, with each node holding only a portion of the total data, improving write scalability and allowing the dataset to grow beyond a single machine's capacity. Large-scale systems often combine both — data is partitioned across shards, and each shard is also replicated for fault tolerance.

---

## 17. NoSQL & MongoDB Basics

## Question 90
**Topic:** NoSQL & MongoDB Basics
**Difficulty:** Medium

**Interview Question:** SQL vs NoSQL — what's the difference?

**Answer:**
SQL databases are relational, store data in fixed-schema tables with rows and columns, and enforce ACID properties strongly — good for structured data with complex relationships, like banking. NoSQL databases are non-relational, use flexible schemas (documents, key-value, graph, or column-family), and generally prioritize horizontal scalability and availability over strict consistency. Choose SQL when data is structured and relationships/transactions matter; choose NoSQL when you need to handle huge, rapidly-changing, or unstructured data at scale, like social media feeds or IoT sensor data.

---

## Question 91
**Topic:** NoSQL & MongoDB Basics
**Difficulty:** Medium

**Interview Question:** What is MongoDB, and how does it store data?

**Answer:**
MongoDB is a popular NoSQL document database that stores data as flexible, JSON-like documents instead of rows in fixed tables. Each document can have a different structure, so schema changes don't require altering an entire table. It's designed for horizontal scaling (sharding) and works well for applications with rapidly evolving or hierarchical data models, like content management or product catalogs.

---

## Question 92
**Topic:** NoSQL & MongoDB Basics
**Difficulty:** Medium

**Interview Question:** What is a Document Database?

**Answer:**
A document database stores data as self-contained documents, typically in JSON or BSON format, where each document can hold nested fields and arrays without requiring a fixed schema across all records. This maps naturally to how objects look in application code, avoiding the need for as many joins. Example: a "Product" document can directly embed its reviews as a nested array instead of needing a separate joined table.

---

## Question 93
**Topic:** NoSQL & MongoDB Basics
**Difficulty:** Medium

**Interview Question:** Collections vs Tables — what's the difference?

**Answer:**
A collection in MongoDB is the equivalent of a table in a relational database, but it holds documents instead of rows. Unlike a table, a collection doesn't enforce a fixed schema — different documents in the same collection can have different fields. This gives flexibility for evolving data models but shifts the responsibility of data consistency more onto the application layer.

---

## Question 94
**Topic:** NoSQL & MongoDB Basics
**Difficulty:** Medium

**Interview Question:** What is BSON?

**Answer:**
BSON (Binary JSON) is the binary-encoded format MongoDB uses internally to store documents. It extends JSON by adding support for additional data types like dates, binary data, and ObjectId, which plain JSON doesn't support natively. It's designed to be fast to encode/decode and easy to traverse, which is why MongoDB uses it as its storage and network transfer format instead of plain text JSON.

---

## 18. Scenario-Based Questions

## Question 95
**Topic:** Scenario-Based Questions
**Difficulty:** Hard

**Interview Question:** How would you design a database for a college student management system?

**Answer:**
I'd start by identifying entities: Student, Course, Department, and Faculty, then model their relationships — a Student enrolls in many Courses (M:N, needing a junction "Enrollment" table), and a Department has many Faculty and offers many Courses (1:N). Each entity gets a primary key (student_id, course_id, etc.), and I'd normalize up to at least 3NF to avoid redundancy, like keeping department name only in the Department table, not repeated in Student. Finally, I'd add foreign keys to enforce referential integrity between related tables.

---

## Question 96
**Topic:** Scenario-Based Questions
**Difficulty:** Hard

**Interview Question:** Which key would you choose for a table and why?

**Answer:**
I'd first list all candidate keys — attributes or attribute combinations that uniquely identify a row. Then I'd pick the primary key based on stability (it shouldn't change over time), simplicity (preferably a single column), and non-nullability. For example, in a Student table, I'd prefer a surrogate auto-increment student_id over email as primary key, since email could change, while still keeping email as a unique alternate key for lookups.

---

## Question 97
**Topic:** Scenario-Based Questions
**Difficulty:** Hard

**Interview Question:** When would you choose NoSQL over SQL for a project?

**Answer:**
I'd choose NoSQL when the data doesn't fit a fixed schema, changes structure frequently, or needs to scale horizontally across many servers, like a social media feed, product catalog with varying attributes, or real-time analytics on large unstructured data. I'd stick with SQL when the application needs strong ACID transactions and well-defined relationships, like a banking or inventory system where consistency is non-negotiable. In real projects, many systems actually use both together — SQL for core transactional data, NoSQL for logs, caching, or flexible content.

---

## Question 98
**Topic:** Scenario-Based Questions
**Difficulty:** Hard

**Interview Question:** Why does normalization improve performance, and when might it hurt performance?

**Answer:**
Normalization improves performance for write-heavy systems by reducing redundant data, so an update touches only one row instead of many duplicated copies, and it keeps tables smaller and more cache-friendly. It can hurt read performance in read-heavy systems, though, since retrieving a complete picture of an entity now requires multiple joins across normalized tables. That's why reporting/analytics systems often deliberately denormalize — trading some redundancy for fewer joins and faster reads.

---

## Question 99
**Topic:** Scenario-Based Questions
**Difficulty:** Hard

**Interview Question:** Explain indexing using a real-life example.

**Answer:**
An index is like the index page at the back of a textbook — instead of flipping through every page to find "Normalization," you look it up in the index and jump straight to the right page number. Similarly, a database index lets the engine jump directly to matching rows instead of scanning the entire table. Just like a book index takes extra pages to maintain, a database index takes extra storage and slightly slows down inserts/updates, since the index has to stay in sync with the data.

---

## Question 100
**Topic:** Scenario-Based Questions
**Difficulty:** Hard

**Interview Question:** A query that used to be fast has suddenly become slow in production. How would you approach debugging it?

**Answer:**
I'd first run EXPLAIN on the query to see the current execution plan and check whether it's still using the expected indexes — table growth can make the optimizer switch strategies. I'd check if the table statistics are outdated, since stale stats can cause the optimizer to pick a bad plan. I'd also look for missing indexes on newly-added WHERE/JOIN columns, or check if a recent schema/data change broke an existing index's usefulness. Finally, I'd check for lock contention or blocking transactions if the slowdown is intermittent rather than constant.

---

---

# ⭐ Top 30 Most Frequently Asked DBMS Questions in TCS

These are the questions that come up again and again in **TCS Prime, TCS Digital, and TCS Ninja** technical rounds. This section is a rapid-fire, last-minute revision card — one-liner answers only. If you've studied the 100 questions above, this section is just a quick memory jog before you walk in.

| # | Question | One-Line Answer |
|---|---|---|
| 1 | What is DBMS? | Software to create, manage, and query structured data reliably and securely. |
| 2 | DBMS vs File System? | DBMS handles relationships, integrity, and concurrency; a file system doesn't. |
| 3 | What is a Primary Key? | Uniquely identifies each row; can't be NULL; one per table. |
| 4 | Primary Key vs Unique Key? | Primary key disallows NULL and is singular; unique key allows one NULL and can be multiple. |
| 5 | What is a Foreign Key? | A column referencing another table's primary key, enforcing referential integrity. |
| 6 | What is Normalization? | Organizing tables to remove redundancy and avoid anomalies. |
| 7 | 1NF, 2NF, 3NF in one line each? | Atomic values → no partial dependency → no transitive dependency. |
| 8 | 2NF vs 3NF? | 2NF removes partial dependency on a composite key; 3NF removes transitive dependency between non-key attributes. |
| 9 | What is BCNF? | Stricter 3NF — every determinant must be a super key. |
| 10 | What are ACID properties? | Atomicity, Consistency, Isolation, Durability — guarantees for reliable transactions. |
| 11 | What is a Transaction? | A single logical unit of work that must fully succeed or fully fail. |
| 12 | Commit vs Rollback? | Commit saves changes permanently; rollback undoes them. |
| 13 | What is a Deadlock? | Two transactions waiting on each other's locks forever, neither can proceed. |
| 14 | How is Deadlock resolved? | Detection via wait-for graph, or prevention via wait-die/wound-wait schemes. |
| 15 | Shared Lock vs Exclusive Lock? | Shared allows multiple readers; exclusive allows only one writer, blocking all others. |
| 16 | What is Two-Phase Locking? | Growing phase acquires locks, shrinking phase releases them — guarantees serializability. |
| 17 | What is Indexing? | A lookup structure that speeds up data retrieval without scanning the whole table. |
| 18 | Clustered vs Non-Clustered Index? | Clustered defines physical row order (one per table); non-clustered is a separate pointer structure (many per table). |
| 19 | B-Tree vs B+ Tree? | B+ Tree stores data only in linked leaf nodes, making range queries much faster. |
| 20 | Inner Join vs Outer Join? | Inner returns only matching rows; outer also includes unmatched rows with NULLs. |
| 21 | DELETE vs TRUNCATE vs DROP? | DELETE removes rows (rollback-able); TRUNCATE empties the table fast (resets identity); DROP removes the table entirely. |
| 22 | What is a View? | A virtual table based on a stored query, no physical data of its own. |
| 23 | Stored Procedure vs Function? | Procedure can perform any action and may not return a value; function must return exactly one value and is used in expressions. |
| 24 | What is a Trigger? | Code that auto-executes on an INSERT/UPDATE/DELETE event. |
| 25 | Nested vs Correlated Subquery? | Nested runs once independently; correlated runs once per outer row. |
| 26 | What is CAP Theorem? | Pick 2 of 3: Consistency, Availability, Partition Tolerance. |
| 27 | SQL vs NoSQL? | SQL is relational and schema-fixed with strong ACID; NoSQL is flexible-schema and built for horizontal scale. |
| 28 | What is Sharding/Partitioning? | Splitting data across multiple nodes so no single node holds everything. |
| 29 | What is a Weak Entity? | An entity with no independent primary key, identified using its owner's key. |
| 30 | Why is indexing a trade-off? | Faster reads, but slower writes and extra storage since the index must stay updated. |

---

## Final Interview Tips (TCS Prime Specific)

* **Speak in the same 4–5 line structure** used throughout this handbook — TCS interviewers value precision over long-winded theory.
* **Always be ready for a comparison follow-up.** If asked "what is normalization," expect "difference between 2NF and 3NF" right after.
* **Tie answers to real systems** where possible (banking for ACID, e-commerce for indexing) — TCS interviewers like practical grounding since TCS builds enterprise systems for such domains.
* **For SQL questions, mentally write the query** even if not asked to — it shows confidence if you can casually add "the query for this would be SELECT... GROUP BY...".
* **Don't guess on NoSQL/CAP theorem** if unsure — say what you know confidently rather than fumbling; TCS Digital/Prime interviewers value honesty over bluffing.

Good luck with your TCS Prime interview.
