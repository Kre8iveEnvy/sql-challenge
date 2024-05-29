# sql-challenge
For this project, you’ll design the tables to hold the data from the CSV files, import the CSV files into a SQL database, and then answer questions about the data. That is, you’ll perform data modeling, data engineering, and data analysis, respectively.
# Steps of this challenge is seperated into four folders. 
Folder titled 'data' - holds the 6 csv files.
Folder titled 'Data Modeling' - holds the png file for the ERD (entity relationship diagram) of how the 6 csv files relate to one another.
Folder titled 'Data Engineering' - is the sql file utilizing the export fuction for PostgreSQL in setting up the ERD. This is used to create the necessary tables with its PK, FK, data types and references 
Folder titled 'Data Analysis' - is the dql file that leverages the tables created in the Data Engineering step to answer the below questions: 
# -- Data Analysis 
-- 1. List the employee number, last name, first name, sex, and salary of each employee
SELECT e.emp_no, e.last_name, e.first_name, e.sex, s.salary
FROM employees e
INNER JOIN salaries s on s.emp_no = e.emp_no
ORDER BY 1;

-- 2. List the first name, last name, and hire date for the employees who were hired in 1986
SELECT e.first_name, e.last_name, e.hire_date
FROM employees e
WHERE hire_date BETWEEN '1986-01-01' AND '1986-12-31'
ORDER BY 3;

-- 3. List the manager of each department along with their department number, department name, 
-- employee number, last name, and first name
SELECT dm.dept_no, d.dept_name, dm.emp_no, e.last_name, e.first_name
FROM dept_manager dm
JOIN departments d ON d.dept_no = dm.dept_no
JOIN employees e ON e.emp_no = dm.emp_no;

-- 4. List the department number for each employee along with that employee’s employee number, 
-- last name, first name, and department name
SELECT e.emp_no, e.last_name, e.first_name, d.dept_name, d.dept_no
FROM employees e
JOIN dept_emp de ON e.emp_no = de.emp_no
LEFT JOIN departments d ON d.dept_no = de.dept_no
ORDER BY 5;

-- 5. List first name, last name, and sex of each employee whose first name is Hercules 
-- and whose last name begins with the letter B
SELECT e.first_name, e.last_name, e.sex
FROM employees e
WHERE first_name = 'Hercules'
AND last_name LIKE 'B%';

-- 6. List each employee in the Sales department, including their employee number, last name, and first name
SELECT e.emp_no, e.last_name, e.first_name, d.dept_name
FROM employees e
INNER JOIN dept_emp de ON e.emp_no = de.emp_no
INNER JOIN departments d ON de.dept_no = d.dept_no
WHERE d.dept_name = 'Sales'
ORDER BY 2;

-- 7. List each employee in the Sales and Development departments, including their employee number, 
-- last name, first name, and department name
SELECT e.emp_no, e.last_name, e.first_name, d.dept_name
FROM employees e
INNER JOIN dept_emp de ON e.emp_no = de.emp_no
INNER JOIN departments d ON de.dept_no = d.dept_no
WHERE d.dept_name = 'Sales' or d.dept_name = 'Development'
ORDER BY 4;

-- 8. List the frequency counts, in descending order, of all the employee last names 
-- (that is, how many employees share each last name)
SELECT last_name, COUNT(last_name) AS "Count of LN"
FROM employees
GROUP BY last_name
ORDER BY 2 DESC;
