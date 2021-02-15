# Pewlett-Hackard-Analysis
## Overview
Pewlett Hackard is a fictional company that is facing the problem of a large percentage of their workforce retiring at the same time. In this analysis, I queried the number of retiring employees per title using Postgres and identified employees who were eligible to participate in the mentorship program.

# Results
 - There are a total of 90398 employees who were born between January 1, 1952 and December 31, 1955. They are eligible for retirement. 
    - Here is a table of all the retiring employees
<img src = "https://github.com/Kee2u/Pewlett-Hackard-Analysis/blob/main/Unique_title.PNG?raw=truee" width = "600">

 - These employees held a total of 133776 positions over the course of their career.
    - Here is a table of all the retiring employees along with their past positions
  <img src = "https://github.com/Kee2u/Pewlett-Hackard-Analysis/blob/main/retirement_titles.PNG?raw=true" width = "600">
 
 - Here is the breakdown of retirement-ready individuals by title
 <img src = "https://github.com/Kee2u/Pewlett-Hackard-Analysis/blob/main/RetiringEmployees.PNG?raw=true" width = "300">
    
 - There are a total of 1549 mentorship eligible workers. The criteria that makes them mentorship eligible is that they were born between January 1, 1965 and December 31, 1965.
 <img src = "https://github.com/Kee2u/Pewlett-Hackard-Analysis/blob/main/mentorship_eligibility.PNG?raw=true" width = "800">

# Summary
   - As workers start to retire, a total of 90398 roles will need to be filled
   - There are only 1549 mentorship eligible workers to mentor the newer employees. Assuming that every new worker needs one mentor, there are not nearly enough mentors available.
   
   Here is a summary of the number of mentorship eligible workers by department. (Comparing it to the previous breakdown of number of retiring employees by title , we can see that there are not enough mentors for each position) <br /> <br />
   <img src = "https://github.com/Kee2u/Pewlett-Hackard-Analysis/blob/main/MentorEmployees.PNG?raw=true" width = "300">
   
   However, taking a closer look at the positions, we can make a reasonable assumption that a Senior Engineer and Senior Staff member will be able to mentor newer Engineers and Staff. Here is the count of senior engineers  and senior staff who were born after December 31, 1955 (not yet eligible for retirement). <br /> <br />
<img src = "https://github.com/Kee2u/Pewlett-Hackard-Analysis/blob/main/Senior_Staff.PNG?raw=true" width = "300">

From this it is clear that there are a lot more mentors available for future staff and engineers.

Here is the code I used to calculate the number of senior engineers and staff that were not yet available for retirement.<br /> 
> SELECT DISTINCT ON (e.emp_no) e.emp_no,<br /> 
> 	   e.first_name,<br /> 
> 	   e.last_name,<br /> 
> 	   t.title<br /> 
> INTO senior_staff<br /> 
> FROM employees as e<br /> 
> inner JOIN titles as t<br /> 
> ON (e.emp_no = t.emp_no)<br /> 
> WHERE e.birth_date> '1955-12-31'<br /> 
> AND title = 'Senior Engineer' OR title = 'Senior Staff'<br /> 
> ORDER BY e.emp_no ASC, t.to_date DESC<br /> 

> SELECT COUNT(title), title<br /> 
> FROM senior_staff<br /> 
> GROUP BY title<br /> 
> ORDER BY Count(title) DESC<br /> 
