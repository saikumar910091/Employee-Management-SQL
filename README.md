# Employee-Management-SQL
Employee Management and salary Analysis using SQL
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(50)
);

CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    name VARCHAR(50),
    department_id INT,
    salary DECIMAL(10,2),
    city VARCHAR(50),
    experience INT,
    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);

INSERT INTO departments VALUES
(1, 'IT'),
(2, 'HR'),
(3, 'Finance');

INSERT INTO employees VALUES
(101, 'Rahul', 1, 55000, 'Hyderabad', 2),
(102, 'Priya', 2, 40000, 'Chennai', 3),
(103, 'Arjun', 1, 65000, 'Bangalore', 4),
(104, 'Sneha', 3, 50000, 'Hyderabad', 2),
(105, 'Kiran', 1, 70000, 'Pune', 5);

-- 5. DISPLAY ALL EMPLOYEES
-- ============================================

SELECT *
FROM employees;


-- Display selected columns

SELECT emp_id, name, salary, city
FROM employees;


-- ============================================
-- 6. FILTER EMPLOYEES
-- ============================================

-- Employees earning more than 50000

SELECT *
FROM employees
WHERE salary > 50000;


-- Employees from Hyderabad

SELECT *
FROM employees
WHERE city = 'Hyderabad';


-- Employees with more than 3 years of experience

SELECT *
FROM employees
WHERE experience > 3;


-- Employees from IT department

SELECT *
FROM employees
WHERE department_id = 1;


-- ============================================
-- 7. SORT EMPLOYEES
-- ============================================

-- Highest salary first

SELECT *
FROM employees
ORDER BY salary DESC;


-- Lowest salary first

SELECT *
FROM employees
ORDER BY salary ASC;


-- Sort by experience from highest to lowest

SELECT *
FROM employees
ORDER BY experience DESC;


-- ============================================
-- 8. ADD A NEW EMPLOYEE
-- ============================================

INSERT INTO employees
VALUES (106, 'Anil', 2, 45000, 'Hyderabad', 1);


-- View the new employee

SELECT *
FROM employees
WHERE emp_id = 106;


-- ============================================
-- 9. UPDATE EMPLOYEE DETAILS
-- ============================================

-- Increase Rahul's salary

UPDATE employees
SET salary = 60000
WHERE emp_id = 101;


-- Change Anil's city

UPDATE employees
SET city = 'Mumbai'
WHERE emp_id = 106;


-- Check updated records

SELECT *
FROM employees
WHERE emp_id IN (101, 106);


-- ============================================
-- 10. DELETE AN EMPLOYEE
-- ============================================

-- Delete Anil's record

DELETE FROM employees
WHERE emp_id = 106;


-- Confirm deletion

SELECT *
FROM employees
WHERE emp_id = 106;


-- ============================================
-- 11. BASIC SALARY ANALYSIS
-- ============================================

-- Total salary expense

SELECT SUM(salary) AS total_salary
FROM employees;


-- Average salary

SELECT AVG(salary) AS average_salary
FROM employees;


-- Highest salary

SELECT MAX(salary) AS highest_salary
FROM employees;


-- Lowest salary

SELECT MIN(salary) AS lowest_salary
FROM employees;


-- Count total employees

SELECT COUNT(*) AS total_employees
FROM employees;


-- ============================================
-- 12. DEPARTMENT-WISE EMPLOYEE COUNT
-- ============================================

SELECT
    d.department_name,
    COUNT(e.emp_id) AS employee_count
FROM departments d
LEFT JOIN employees e
    ON d.department_id = e.department_id
GROUP BY d.department_id, d.department_name;


-- ============================================
-- 13. DEPARTMENT-WISE SALARY ANALYSIS
-- ============================================

-- Total salary by department

SELECT
    d.department_name,
    SUM(e.salary) AS total_salary
FROM departments d
JOIN employees e
    ON d.department_id = e.department_id
GROUP BY d.department_id, d.department_name;


-- Average salary by department

SELECT
    d.department_name,
    AVG(e.salary) AS average_salary
FROM departments d
JOIN employees e
    ON d.department_id = e.department_id
GROUP BY d.department_id, d.department_name;


-- Highest salary in each department

SELECT
    d.department_name,
    MAX(e.salary) AS highest_salary
FROM departments d
JOIN employees e
    ON d.department_id = e.department_id
GROUP BY d.department_id, d.department_name;


-- ============================================
-- 14. GROUP BY AND HAVING
-- ============================================

-- Departments with average salary above 50000

SELECT
    d.department_name,
    AVG(e.salary) AS average_salary
FROM departments d
JOIN employees e
    ON d.department_id = e.department_id
GROUP BY d.department_id, d.department_name
HAVING AVG(e.salary) > 50000;


-- Departments with at least 2 employees

SELECT
    d.department_name,
    COUNT(e.emp_id) AS employee_count
FROM departments d
JOIN employees e
    ON d.department_id = e.department_id
GROUP BY d.department_id, d.department_name
HAVING COUNT(e.emp_id) >= 2;

-- ============================================
-- 15. JOIN: DISPLAY EMPLOYEE AND DEPARTMENT
-- ============================================

SELECT
    e.emp_id,
    e.name,
    d.department_name,
    e.salary,
    e.city,
    e.experience
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
