DROP TABLE department;
DROP TABLE dept_emp;
DROP TABLE dept_manager;
DROP TABLE employees;
DROP TABLE salary;
DROP TABLE titles;

CREATE TABLE department(
dept_no varchar NOT NULL,
dept_name varchar,
PRIMARY KEY (dept_no)
);
 
CREATE TABLE dept_emp(
emp_no int,
dept_no varchar,
from_date date,
to_date date,
FOREIGN KEY (dept_no) REFERENCES department(dept_no),
FOREIGN KEY (emp_no) REFERENCES employees(emp_no)
);

CREATE TABLE dept_manager(
dept_no varchar,
emp_no int,
from_date date,
to_date date,
FOREIGN KEY (dept_no) REFERENCES department(dept_no),
FOREIGN KEY (emp_no) REFERENCES employees(emp_no)
);

CREATE TABLE employees(
emp_no int NOT NULL PRIMARY KEY,
birth_date date,
first_name varchar (25),
last_name varchar (25),
gender char(1),
hire_date date
);

CREATE TABLE salary(
emp_no int,
salary DEC(13,2),
from_date date,
to_date date,
FOREIGN KEY (emp_no) REFERENCES employees(emp_no)
);

CREATE TABLE titles(
emp_no int,
title VARCHAR,
from_date date,
to_date date,
FOREIGN KEY (emp_no) REFERENCES employees(emp_no)
);


COPY department FROM 'C:\Users\subil\Desktop\Homework\7\departments.csv' 
WITH 
(	FORMAT CSV,
	DELIMITER ',',
    HEADER TRUE);
COPY department FROM 'C:\hm\depatments.csv' DELIMITER ',' CSV HEADER;
COPY dept_emp FROM 'C:\hm\dept_emp.csv' DELIMITER ',' CSV HEADER;
COPY dept_manager FROM 'C:\hm\dept_manager.csv' DELIMITER ',' CSV HEADER;
COPY employees FROM 'C:\hm\employees.csv' DELIMITER ',' CSV HEADER;
COPY salary FROM 'C:\hm\salary.csv' DELIMITER ',' CSV HEADER;
COPY titles FROM 'C:\hm\titles.csv' DELIMITER ',' CSV HEADER;

SELECT * FROM  employees;

--List the following details of each employee: employee number, last name, first name, gender, and salary
SELECT e.emp_no, e.last_name, e.first_name, e.gender, s.salary
FROM employees e JOIN salary s ON e.emp_no = s.emp_no

--List employees who were hired in 1986.
SELECT first_name, last_name, hire_date
FROM employees
WHERE EXTRACT (YEAR FROM hire_date) = 1986;

--List the manager of each department with the following information: 
--department number, department name, the manager's employee number, 
--last name, first name, and start and end employment dates.

SELECT d.dept_no, d.dept_name, f.emp_no, e.last_name, e.first_name, f.from_date, f.to_date 
FROM employees e
JOIN dept_manager f ON e.emp_no = f.emp_no
JOIN department d ON f.dept_no = d.dept_no;


--List the department of each employee with the following information:
--employee number, last name, first name, and department name.

SELECT e.emp_no, e.last_name, e.first_name, d.dept_name
FROM employees e
JOIN dept_emp f ON e.emp_no = f.emp_no
JOIN department d ON f.dept_no = d.dept_no;

--List all employees whose first name is "Hercules" and 
--last names begin with "B."

SELECT first_name, last_name
FROM employees
WHERE first_name = 'Hercules' AND last_name LIKE 'B%';

--List all employees in the Sales department, including their employee number,
--last name, first name, and department name.

SELECT e.emp_no, e.last_name, e.first_name, d.dept_name
FROM employees e
JOIN dept_emp f ON e.emp_no = f.emp_no
JOIN department d ON f.dept_no = d.dept_no
WHERE d.dept_name = 'Sales';

--List all employees in the Sales and Development departments, 
--including their employee number, last name, first name, and department name.

SELECT e.emp_no, e.last_name, e.first_name, d.dept_name
FROM employees e
JOIN dept_emp f ON e.emp_no = f.emp_no
JOIN department d ON f.dept_no = d.dept_no
WHERE d.dept_name IN ('Sales', 'Development');


--In descending order, list the frequency count of employee last names
-- i.e., how many employees share each last name.

SELECT last_name, COUNT(last_name) amount
FROM employees
GROUP BY last_name
ORDER BY amount DESC;

