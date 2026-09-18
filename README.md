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
