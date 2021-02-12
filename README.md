# Pewlett-Hackard-Analysis
## Overview
Pewlett Hackard is a fictional company that is facing the problem of a large percentage of their workforce retiring at the same time. In this analysis, I queried employee data using PostgreSQL to determine the impact from workers retiring. 

## Analysis
After gathering the required csv files, I created an Entity Relationship Diagram to determine the primary keys and map out the relationship them.
I used Quick DBD to create the following schematic:

<img src = "https://github.com/Kee2u/Pewlett-Hackard-Analysis/blob/main/EmployeeDB.png?raw=true">

Next, I turned to PostgreSQL and created tables to upload the csv files using the CREATE command. here is an example of the code:

### Determining Retirement Eligibility
 1. The first query I wrote returned a list of all employees who were born between 1952 and 1955 and who were hired between 1985 and 1988. These conditions meant that they were ready for retirement. <br/>
 
    > SELECT first_name, last_name <br/>
    > FROM employees <br/>
    > WHERE (birth_date BETWEEN '1952-01-01' AND '1955-12-31') <br/>
    > AND (hire_date BETWEEN '1958-01-01' AND '1988-12-31'); <br/>
