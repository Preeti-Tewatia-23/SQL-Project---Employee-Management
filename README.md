# SQL-Project---Employee-Management

# Create Database
CREATE DATABASE employee_project;
USE employee_project;

# Table Creation
CREATE TABLE employee (
emp_id INT PRIMARY KEY,
name VARCHAR(50),
gender VARCHAR(10),
department_id INT,
Salary INT,
hire_date DATE
);

# Departments Table
CREATE TABLE departments (
department_id INT PRIMARY KEY,
department_name VARCHAR(50)
);

# Project Table
CREATE TABLE projects(
project_id INT PRIMARY KEY,
project_name VARCHAR(50),
emp_id INT
);

# Insert Sample Data
INSERT INTO departments VALUES
(1, 'IT'), 
(2, 'HR'),
(3, 'Finance');

INSERT INTO employees VALUES
(101, 'Preeti', 'Female', 1400000, '2026-04-01'),
(102, 'Amit', 'Male', 2300000, '2022-03-15'),
(103, 'Riya', 'Female', 145000, '2021-01-02),
(104, 'Rahul', 'Male', 350000, '2020-09-01');

INSERT INTO projects VALUES
(1, 'Dashboard', 101),
(2, 'Recruitment System', 102),
3, 'Finance Report', 104);

## Project Analysis Queries ##
# View all Employees
Select * from employees;

# Employees with Department Name (JOIN)
select e.name, d.department_name
FROM employees e
JOIN departments d
ON e.department_id = d.department_id;

# Highest Salary Employee
Select * from employees
Where Salary = (Select MAX(salary) From employees);

# Department Wise Average Salary
Select department_id, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id;

# Total Employees in Each Department
Select department_id, COUNT(*) AS total_employees
FROM employees
GROUP BY department_id;

# Employees Earning Above Average Salary
Select name, salary From employees
where salary > (Select AVG(salary) From employees);

# Employees Without Projects
Select e.name From employee e
LEFT JOIN projects p
ON e.emp_id = p.emp_id
Where p.project_id IS NULL;

# Second Highest Salary
Select MAX(salary) From employees
Where salary < (Select MAX(salary) From employees);

# Salary Ranking
select name, salary, RAnk() OVER (ORDER BY salary DESC) AS Salary_rank From employees;

# Employees Joined after 2022
Select * From employees
Where hire_date > '2022-01-01';

# Department with Highest Average Salary
Select department_id, AVG(salary) avg_sal From employees
GROUP BY department_id
ORDER BY avg_sal DESC
LIMIT 1;

# Update Salary
UPDATE employees
SET salary = salary + 5000
Where department_id = 1;

# Delete Employee
DELETE FROM employees
WHERE emp_id = 104;

# Create View ( For Dashboard)
CREATE VIEW employee_summary AS Select name, salary From employees;

# Stored Procedure
CREATE PROCEDURE gethighsalary() 
Select * From employees
Where salary > 35000;



