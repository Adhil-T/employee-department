# Employee & Department SQL Lab

## Objective
Learn basic SQL operations including:
* Database and table creation
* Inserting records
* Retrieving data using queries
* Using JOIN, GROUP BY, aggregate functions, and subqueries

---

## SQL Script

-- Step 1: Create and Select Database

```sql
CREATE DATABASE employee_department;
USE employee_department;
```

-- Step 2: Create Tables

```sql
CREATE TABLE department(
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(20)
);

CREATE TABLE employee(
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(20),
    salary INT,
    dept_id INT,
    FOREIGN KEY(dept_id) REFERENCES department(dept_id)
);
```

-- Step 3: Insert Data

```sql
INSERT INTO department VALUES
(1001, "Computer Science"),
(1002, "Maths"),
(1003, "Physics"),
(1004, "Chemistry"),
(1005, "Zoology");

SELECT * FROM department;

INSERT INTO employee VALUES
(101, "Alan", 65000, 1002),
(102, "Smith", 45000, 1005),
(103, "Jason", 55000, 1004),
(104, "Elena", 60000, 1001),
(105, "Joseph", 70000, 1002),
(106, "Andrew", 61000, 1002),
(107, "Salman", 58000, 1003),
(108, "Eva", 68000, 1005);

SELECT * FROM employee;
```

-- Queries & Questions

-- Q1: Employees with Salary >= 60000

```sql
SELECT emp_name, salary FROM employee WHERE salary >= 60000;
```

-- Q2: Employee Names with Department Names

```sql
SELECT e.emp_name, d.dept_name FROM employee e JOIN department d ON e.dept_id = d.dept_id;
```

-- Q3: Employee(s) with Highest Salary

```sql
SELECT * FROM employee WHERE salary = (SELECT MAX(salary) FROM employee);
```

-- Q4: Number of Employees in Each Department

```sql
SELECT d.dept_name, COUNT(e.dept_id) FROM department d JOIN employee e ON d.dept_id = e.dept_id GROUP BY d.dept_name;
```

-- Q5: Employees with Salary Above Average

```sql
SELECT * FROM employee WHERE salary >= (SELECT AVG(salary) FROM employee);
```

-- Q6: Departments with More Than 2 Employees

```sql
SELECT d.dept_name FROM department d JOIN employee e ON d.dept_id = e.dept_id GROUP BY d.dept_name HAVING COUNT(e.dept_id) > 2;
```
