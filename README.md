# Pewlett-Hackard-Analysis
## Overview
Pewlett Hackard is a fictional company that is facing the problem of a large percentage of their workforce retiring at the same time. In this analysis, I queried employee data using PostgreSQL to determine the impact from workers retiring. 

## Analysis
After gathering the required csv files, I created an Entity Relationship Diagram to determine the primary keys and map out the relationship them.
I used Quick DBD to create the following schematic:

<img src = "https://github.com/Kee2u/Pewlett-Hackard-Analysis/blob/main/EmployeeDB.png?raw=true">

Next, I turned to PostgreSQL and created tables to upload the csv files using the command
> CREATE TABLE
