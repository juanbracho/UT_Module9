# Module 9: SQL

## Overview
This module focuses on SQL (Structured Query Language) to perform data modeling, engineering, and analysis. The module is divided into three sections: **Data Modeling**, **Data Engineering**, and **Data Analysis**.

---

## 9.1: Introduction to SQL

### What We Learn
- Running PostgreSQL and pgAdmin.
- Creating databases and tables.
- Defining SQL data types, primary keys, and unique values.
- Loading CSV data into SQL tables.
- Performing CRUD operations (Create, Read, Update, Delete).
- Combining data from multiple tables with JOIN clauses.

## 9.2: Advanced SQL Queries

### What We Learn
- Writing aggregate queries using `GROUP BY`, `HAVING`, and `ORDER BY`.
- Creating and using subqueries.
- Designing and querying views.

---

## 9.3: Data Modeling and ERDs

### What You'll Learn
- Creating entity-relationship diagrams (ERDs) to design a database schema.
- Normalizing data for optimal database performance.
- Designing schemas with foreign key constraints and composite keys.

---

## Data Analysis Requirements

### Tasks and Example Queries
1. **List Employee Information:**
    ```sql
    SELECT employee_number, last_name, first_name, salary FROM employees;
    ```

2. **Employees Hired in 1986:**
    ```sql
    SELECT first_name, last_name, hire_date
    FROM employees
    WHERE EXTRACT(YEAR FROM hire_date) = 1986;
    ```

3. **Manager and Department Information:**
    ```sql
    SELECT d.department_name, e.last_name AS manager_last_name, e.first_name AS manager_first_name
    FROM departments d
    JOIN employees e ON d.manager_id = e.employee_number;
    ```

4. **Employees in Sales Department:**
    ```sql
    SELECT e.employee_number, e.last_name, e.first_name
    FROM employees e
    JOIN departments d ON e.department_id = d.department_id
    WHERE d.department_name = 'Sales';
    ```

5. **Frequency of Last Names:**
    ```sql
    SELECT last_name, COUNT(*) AS frequency
    FROM employees
    GROUP BY last_name
    ORDER BY frequency DESC;
    ```

---

## Additional Notes
- Use **pgAdmin** for database management tasks.
- Ensure ERDs are created to visualize relationships between tables.
- Remember to test queries for performance and accuracy.
- For CSV imports, verify correct column mapping.

---
