# Employee Database — SQL Data Modeling, Engineering & Analysis

## Overview

This project demonstrates a complete data engineering workflow using PostgreSQL: designing an entity-relationship diagram (ERD), creating a relational schema, loading data from CSV files, and running analytical SQL queries against a fictional employee database from the 1980s–1990s.

---

## Dataset

Six CSV files representing employee records:

| File | Description |
|------|-------------|
| `employees.csv` | Employee records (ID, name, sex, hire date, title) |
| `departments.csv` | Department names and IDs |
| `dept_emp.csv` | Employee-to-department assignments |
| `dept_manager.csv` | Department manager assignments |
| `salaries.csv` | Employee salary records |
| `titles.csv` | Job title definitions |

---

## Project Structure

```
SQL/
├── Employees ERD.pdf          # Entity-Relationship Diagram
├── Employees_Schemata.sql     # Table creation DDL (schema)
├── Employees_Analysis.sql     # Analytical SQL queries
├── employees.csv
├── departments.csv
├── dept_emp.csv
├── dept_manager.csv
├── salaries.csv
├── titles.csv
└── README.md
```

---

## Part 1: Data Modeling

An entity-relationship diagram (ERD) was designed to map relationships across the six tables before any code was written. See `Employees ERD.pdf` for the full diagram.

**Key relationships:**
- `Employees` → `Titles` (via `Emp_title_id`)
- `Employees` ↔ `Departments` (via `Department_Employees` junction table)
- `Employees` ↔ `Departments` (via `department_Managers` junction table)
- `Employees` → `Salaries` (one-to-one)

---

## Part 2: Data Engineering

The schema was implemented in PostgreSQL using `Employees_Schemata.sql`, which:
- Drops existing tables (if present) to allow clean re-runs
- Creates all six tables with appropriate data types and constraints
- Defines primary keys, foreign keys, and a composite primary key on `Department_Employees`

Tables were populated by importing the CSV files using the **pgAdmin Import/Export** function.

---

## Part 3: Data Analysis

Eight analytical queries were written in `Employees_Analysis.sql`:

1. **Employee roster with salary** — Lists employee number, last name, first name, sex, and salary for all employees (JOIN with Salaries)
2. **Employees hired in 1986** — First name, last name, and hire date filtered by year
3. **Employees named Hercules B.** — First name = "Hercules" and last name starting with "B"
4. **Department managers** — Manager name, department number, department name, and employee number
5. **All employees with department** — Each employee's department assignment via the `Department_Employees` table
6. **Sales department employees** — Employee number, last name, first name for all Sales staff (subquery approach)
7. **Sales and Development employees** — Same as above, expanded to include both departments with department name
8. **Last name frequency** — Count of employees sharing each last name, sorted descending

---

## Tools and Technologies

- PostgreSQL (via pgAdmin)
- SQL DDL for schema creation
- SQL DML for data analysis (JOINs, subqueries, GROUP BY, ORDER BY, EXTRACT)

---

## How to Run

1. Open pgAdmin and connect to your PostgreSQL instance.
2. Run `Employees_Schemata.sql` to create all tables.
3. Use pgAdmin's Import/Export tool to load each CSV file into its corresponding table.
4. Run `Employees_Analysis.sql` to execute the analytical queries.
