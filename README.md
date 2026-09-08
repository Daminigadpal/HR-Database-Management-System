# HR Database Management System

## 📌 Project Overview

The **HR Database Management System** is a relational database project developed using **SQL and Microsoft SQL Server**.

The project is designed to store, manage, retrieve, and analyze human resource information such as employees, departments, jobs, dependents, locations, countries, and regions.

The project demonstrates practical implementation of SQL concepts including database design, constraints, filtering, sorting, aggregate functions, joins, subqueries, grouping, and advanced SQL operations.

---

## 🎯 Objectives

The main objectives of this project are:

* Manage employee information efficiently.
* Maintain department and job information.
* Store employee-dependent information.
* Establish relationships between different HR entities.
* Maintain data integrity using primary and foreign keys.
* Retrieve information using SQL queries.
* Analyze HR data using aggregation and grouping.
* Perform analysis using different types of joins.
* Use subqueries for advanced data analysis.
* Demonstrate practical SQL and MS SQL Server skills.

---

## 🗄️ Database Structure

The database consists of **7 relational tables**:

| Table         | Description                                  |
| ------------- | -------------------------------------------- |
| `employees`   | Stores employee information                  |
| `dependents`  | Stores information about employee dependents |
| `departments` | Stores department information                |
| `jobs`        | Stores job information                       |
| `locations`   | Stores location information                  |
| `countries`   | Stores country information                   |
| `regions`     | Stores regional information                  |

### Main Relationships

```text
Regions
   │
   ▼
Countries
   │
   ▼
Locations
   │
   ▼
Departments
   │
   ├──────────────► Employees ◄──────────────┐
   │                       │                 │
   │                       ▼                 │
   │                  Dependents             │
   │                                         │
   └──────────────► Jobs                     │
                                             │
                                      Manager Relationship
                                      (Self-Reference)
```

---

## 🛠️ Technologies Used

* **Database:** Microsoft SQL Server
* **Query Language:** SQL
* **Database Management:** MS SQL Server / SSMS
* **Documentation:** PowerPoint / PDF
* **Version Control:** Git & GitHub

---

## 📚 SQL Concepts Covered

This project covers the following SQL concepts:

### Basic SQL

* `SELECT`
* `WHERE`
* `DISTINCT`
* `TOP`
* `ORDER BY`

### Operators

* Comparison operators
* Logical operators
* Special operators

### Database Constraints

* Primary Key
* Foreign Key
* Self-referencing Foreign Key

### Data Definition & Manipulation

* `ALTER TABLE`
* `UPDATE`

### Aggregate Functions

* `COUNT()`
* `SUM()`
* `AVG()`
* `MIN()`
* `MAX()`

### Grouping

* `GROUP BY`
* `HAVING`

### Joins

* `INNER JOIN`
* `LEFT JOIN`
* `SELF JOIN`
* `FULL JOIN`
* `CROSS JOIN`

### Advanced SQL

* Subqueries
* `UNION`
* `INTERSECT`
* `EXISTS`
* `CASE`

---

## 📊 Project Analysis

The database can be used to perform different types of HR analysis.

### Employee Analysis

Retrieve and filter employee records based on different conditions.

### Department Analysis

Analyze employees according to their departments and perform department-level aggregation.

### Job Analysis

Connect employee information with job information to understand employee roles.

### Management Analysis

Use self-joins to analyze manager and employee relationships.

### Dependent Analysis

Connect employees with their dependents using foreign-key relationships.

### Geographical Analysis

Connect locations, countries, and regions to analyze organizational geographical information.

---

## 🔑 Database Integrity

Primary keys and foreign keys are used to maintain relationships between tables.

For example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(20),
    last_name VARCHAR(25),
    hire_date DATE NOT NULL,
    job_id INT,
    department_id INT
);
```

A dependent record is connected to an employee using a foreign key:

```sql
FOREIGN KEY (employee_id)
REFERENCES employees(employee_id)
```

This prevents dependent records from referencing employees that do not exist in the employee table.

---

## 🔍 Example SQL Queries

### Display all employees

```sql
SELECT *
FROM employees;
```

### Find employees from a particular department

```sql
SELECT employee_id, first_name, last_name, department_id
FROM employees
WHERE department_id = 10;
```

### Sort employees by salary

```sql
SELECT employee_id, first_name, last_name, salary
FROM employees
ORDER BY salary DESC;
```

### Calculate average salary

```sql
SELECT AVG(salary) AS average_salary
FROM employees;
```

### Department-wise average salary

```sql
SELECT
    department_id,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department_id;
```

### Employees with their department names

```sql
SELECT
    e.employee_id,
    e.first_name,
    e.last_name,
    d.department_name
FROM employees e
INNER JOIN departments d
    ON e.department_id = d.department_id;
```

### Employees and their managers

```sql
SELECT
    e.first_name AS employee,
    m.first_name AS manager
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.employee_id;
```

---

## 📈 Key Insights

The project demonstrates that SQL can be used to:

* Retrieve employee information efficiently.
* Analyze workforce distribution across departments.
* Analyze employees according to job roles.
* Identify manager-employee relationships.
* Connect employees with their dependents.
* Analyze organizational geographical information.
* Perform department-level calculations.
* Generate useful HR reports from relational data.

---

## 💡 Actionable Recommendations

Based on the database analysis, HR teams can:

* Monitor employee distribution across departments.
* Analyze workforce information by job role.
* Identify reporting and management relationships.
* Maintain accurate employee-dependent relationships.
* Use department-level analysis for workforce planning.
* Regularly validate foreign-key relationships.
* Use SQL-based reports to support HR decision-making.
* Maintain consistent and accurate employee records.

---

## 📂 Suggested Project Structure

```text
HR-Database-Management-System/
│
├── README.md
│
├── SQL/
│   ├── database_creation.sql
│   ├── table_creation.sql
│   ├── data_insertion.sql
│   └── queries.sql
│
├── Documentation/
│   └── HR_Database_Management_System.pdf
│
└── Presentation/
    └── HR_Database_Management_System_Damini_Gadpal.pptx
```

---

## 🚀 How to Run the Project

### Step 1 — Install SQL Server

Install **Microsoft SQL Server** and **SQL Server Management Studio (SSMS)**.

### Step 2 — Create the Database

Create a new database:

```sql
CREATE DATABASE HR_Database;
GO

USE HR_Database;
GO
```

### Step 3 — Create Tables

Execute the table creation SQL script.

The tables should be created in an appropriate order so that referenced tables exist before foreign keys are created.

### Step 4 — Insert Data

Execute the data insertion script to populate the tables.

### Step 5 — Run Queries

Execute the SQL queries to perform:

* Employee analysis
* Department analysis
* Job analysis
* Dependent analysis
* Management analysis
* Geographical analysis

---

## ⚠️ Data Integrity Note

While loading the sample data, make sure that every `dependents.employee_id` exists in the `employees` table.

For example, if a dependent references:

```text
employee_id = 206
```

then employee `206` must exist in the `employees` table before that dependent record can be inserted.

You can identify invalid references with:

```sql
SELECT d.employee_id
FROM dependents d
LEFT JOIN employees e
    ON d.employee_id = e.employee_id
WHERE e.employee_id IS NULL;
```

---

## 📋 Project Deliverables

The project includes:

* Database design
* Table creation
* Data insertion
* SQL queries
* Data analysis
* Database relationships
* Project documentation
* Presentation

---

## 🎓 Learning Outcomes

Through this project, the following skills are demonstrated:

* Relational database design
* SQL query writing
* Microsoft SQL Server
* Database constraints
* Data integrity
* Data filtering and sorting
* Aggregate functions
* Grouping
* Joins
* Subqueries
* Advanced SQL operations
* HR data analysis

---

## 👩‍💻 Author

**Damini Gadpal**

**Technology:** SQL / MS SQL Server

**Project:** HR Database Management System

**Course:** CoachX

---


## 📄 Project Documentation

The complete project presentation/report is available below:

👉 **[View HR Database Management System PDF](./HR-Database-Management-System.pdf)**

The PDF contains:

* Introduction
* Problem Statement
* Database Structure
* Key Table Relationships
* SQL Techniques & Methodologies
* Project Approach
* Key Findings
* Major Insights
* Actionable Recommendations
* Conclusion

The project is built using **SQL and MS SQL Server** for managing and analyzing HR-related information.

## 🗂️ Project Files

```text
HR-Database-Management-System/
│
├── README.md
├── HR-Database-Management-System.pdf
│
├── SQL/
│   ├── database_creation.sql
│   ├── table_creation.sql
│   ├── data_insertion.sql
│   └── queries.sql
│
└── Presentation/
    └── HR_Database_Management_System_Damini_Gadpal.pptx
```

## 🛠️ Technologies

* SQL
* Microsoft SQL Server
* SQL Server Management Studio (SSMS)

## 🎯 Objective

The objective of this project is to use SQL and MS SQL Server to store, retrieve, analyze, and manage HR data efficiently.

## 📊 Database

The database contains 7 relational tables:

* Employees
* Dependents
* Departments
* Jobs
* Locations
* Countries
* Regions

## 📚 SQL Concepts

This project demonstrates:

* SELECT
* WHERE
* ORDER BY
* DISTINCT
* TOP
* Primary Keys
* Foreign Keys
* ALTER TABLE
* Aggregate Functions
* GROUP BY
* HAVING
* JOINs
* Subqueries
* CASE
* UNION
* INTERSECT
* EXISTS
* UPDATE

## 📈 Key Findings

The project demonstrates how SQL can be used to:

* Retrieve employee information based on different conditions.
* Analyze employees by department and job.
* Perform department-level analysis using aggregate functions.
* Connect employees and dependents using JOINs.
* Analyze manager–employee relationships using self-joins.
* Combine geographical information from multiple tables.
* Perform advanced employee analysis using subqueries.

## 💡 Recommendations

* Monitor employee distribution across departments.
* Analyze workforce by job role.
* Identify reporting and management relationships.
* Maintain accurate dependent records.
* Use department-level analysis for workforce planning.
* Validate foreign-key relationships regularly.
* Use SQL reports for HR decision-making.
* Maintain accurate employee data.

## 👩‍💻 Author

**Damini Gadpal**

**Technology:** SQL 

