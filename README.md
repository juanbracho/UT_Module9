# Module 9: SQL

## Overview
This module focuses on SQL (Structured Query Language) to perform data modeling, engineering, and analysis. The module is divided into three sections: **Data Modeling**, **Data Engineering**, and **Data Analysis**.

---

## 9.1: Introduction to SQL

### What You'll Learn
- Running PostgreSQL and pgAdmin.
- Creating databases and tables.
- Defining SQL data types, primary keys, and unique values.
- Loading CSV data into SQL tables.
- Performing CRUD operations (Create, Read, Update, Delete).
- Combining data from multiple tables with JOIN clauses.

### Example Code Snippets
- **Creating a Table:**
    ```sql
    CREATE TABLE employees (
        employee_number SERIAL PRIMARY KEY,
        last_name VARCHAR(50),
        first_name VARCHAR(50),
        hire_date DATE,
        department_id INT,
        salary DECIMAL(10, 2)
    );
    ```

- **Inserting Data:**
    Use pgAdmin or `COPY` command to import CSV data:
    ```sql
    COPY employees FROM '/path/to/employees.csv' DELIMITER ',' CSV HEADER;
    ```

- **Basic Query:**
    ```sql
    SELECT * FROM employees;
    ```

---

## 9.2: Advanced SQL Queries

### What You'll Learn
- Writing aggregate queries using `GROUP BY`, `HAVING`, and `ORDER BY`.
- Creating and using subqueries.
- Designing and querying views.

### Example Code Snippets
- **Aggregate Query:**
    ```sql
    SELECT department_id, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
    ORDER BY avg_salary DESC;
    ```

- **Subquery Example:**
    ```sql
    SELECT last_name, first_name, salary
    FROM employees
    WHERE salary = (SELECT MAX(salary) FROM employees);
    ```

- **Creating a View:**
    ```sql
    CREATE VIEW department_summary AS
    SELECT d.department_name, COUNT(e.employee_number) AS total_employees, AVG(e.salary) AS avg_salary
    FROM departments d
    JOIN employees e ON d.department_id = e.department_id
    GROUP BY d.department_name;
    ```

---

## 9.3: Data Modeling and ERDs

### What You'll Learn
- Creating entity-relationship diagrams (ERDs) to design a database schema.
- Normalizing data for optimal database performance.
- Designing schemas with foreign key constraints and composite keys.

### Example Schema
- **Departments and Projects Example:**
    ```sql
    CREATE TABLE projects (
        project_id SERIAL PRIMARY KEY,
        project_name VARCHAR(100),
        start_date DATE,
        end_date DATE
    );

    CREATE TABLE tasks (
        task_id SERIAL PRIMARY KEY,
        task_name VARCHAR(100),
        project_id INT REFERENCES projects(project_id),
        assigned_to INT REFERENCES employees(employee_number),
        due_date DATE
    );
    ```

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
