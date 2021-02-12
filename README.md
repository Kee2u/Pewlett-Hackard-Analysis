# Pewlett-Hackard-Analysis
## Overview
Pewlett Hackard is a fictional company that is facing the problem of a large percentage of their workforce retiring at the same time. In this analysis, I queried employee data using PostgreSQL to determine the impact from workers retiring. 

## Analysis
After gathering the required csv files, I created an Entity Relationship Diagram to determine the primary keys and map out the relationship them.
I used Quick DBD to create the following schematic:

<img src = "https://github.com/Kee2u/Pewlett-Hackard-Analysis/blob/main/EmployeeDB.png?raw=true">

Next, I turned to PostgreSQL and created tables to upload the csv files using the CREATE command. here is an example of the code:

### Determining Retirement Eligibility
 1. The first query I wrote returned a list of all employees who were born between 1952 and 1955 and who were hired between 1985 and 1988. The conditions meant that they were ready for retirement. Then I saved it to a new table called retirement_info. I also used the COUNT() aggregate function to return the number of employees. <br/> <br/>
 Here is the code I used to save the table: <br/>
 
    > SELECT first_name, last_name <br/>
    > INTO retirement_info <br/>
    > FROM employees <br/>
    > WHERE (birth_date BETWEEN '1952-01-01' AND '1955-12-31') <br/>
    > AND (hire_date BETWEEN '1958-01-01' AND '1988-12-31'); <br/>  
    Here is the result: <br/>  
    <img src = "https://github.com/Kee2u/Pewlett-Hackard-Analysis/blob/main/retirement_eligibility.jpg?raw=true" width = "500">
 
 2. To determine if these employees were still in the company, I performed a left join between the retirement info table that I created and the dept_emp table. <br/><br/>
 Here is the code I used: <br/>
 
    > SELECT ri.emp_no, <br/>
    >  ri.first_name, <br/>
    >  ri.last_name, <br/>
	   >  de.to_date <br/>
    >  INTO current_emp <br/> 
    >  FROM retirement_info as ri <br/>
    >  LEFT JOIN dept_emp as de <br/>
    >  ON ri.emp_no = de.emp_no <br/>
    >  WHERE de.to_date = ('9999-01-01');<br/>
    Here is the result: <br/>
    <img src = "https://github.com/Kee2u/Pewlett-Hackard-Analysis/blob/main/Retirement_info_2.jpg?raw=true">
  
### Determining Number of People Leaving Per Department  
 1. I used the GROUP BY command to find the count of retiring employees by department. <br/><br/>
 Here is the code I used: <br/>
 
    > SELECT COUNT(ce.emp_no), de.dept_no <br/>
    > FROM current_emp as ce <br/>
    > LEFT JOIN dept_emp as de <br/>
    > ON ce.emp_no = de.emp_no <br/>
    > GROUP BY de.dept_no <br/>
    > ORDER BY de.dept_no;<br/>
    Here is the result: <br/>  
    <img src = "https://github.com/Kee2u/Pewlett-Hackard-Analysis/blob/main/count_by_department.jpg?raw=true" width = "500"> <br/>
 
 2. Employee Information: I created a list of retiring employees containing their unique employee number, their last name, first name, gender and salary. I used on a join on three tables to achieve this. <br/><br/>
 Here is the code: <br/>
 
   > SELECT e.emp_no,<br/>
   >	e.first_name,<br/>
   >	e.last_name,<br/>
   >	e.gender,<br/>
   >	s.salary,<br/>
   >	de.to_date<br/>
   >INTO emp_info<br/>
   >FROM employees as e<br/>
   >INNER JOIN salaries as s<br/>
   >ON(e.emp_no = s.emp_no)<br/>
   >INNER JOIN dept_emp as de<br/>
   >ON (e.emp_no = de.emp_no)<br/>
   > WHERE (birth_date BETWEEN '1952-01-01' AND '1955-12-31') <br/>
   > AND (hire_date BETWEEN '1958-01-01' AND '1988-12-31') <br/>
   > AND (de.to_date = '9999-01-01'); <br/>
 
 2. Management Information: I created a list of managers retiring from each department. The information I needed was in three tables: Departments, Managers and Employees. <br/><br/>
 Here is the code: <br/>
 > SELECT dm.dept_no,<br/>
 > 	  d.dept_name,<br/>
 >	  dm.emp_no,<br/>
 > 	  ce.last_name,<br/>
 >	  ce.first_name,<br/>
 >	  dm.from_date,<br/>
 >	  dm.to_date<br/>
 > INTO manager_info<br/>
 > FROM dept_manager AS dm<br/>
 >	INNER JOIN departments AS d<br/>
 > 		ON (dm.dept_no = d.dept_no)<br/>
 >	INNER JOIN current_emp AS ce<br/>
 >		ON (dm.emp_no = ce.emp_no);<br/>
 Here is the result: <br/>  
 <img src = "https://github.com/Kee2u/Pewlett-Hackard-Analysis/blob/main/retirement_info.jpg?raw=true"> <br/>
 
