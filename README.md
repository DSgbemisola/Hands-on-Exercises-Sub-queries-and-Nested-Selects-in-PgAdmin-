# Hands-on-Exercises-Sub-queries-and-Nested-Selects-in-PgAdmin-

This is a hands-on exercise to demonstrate skills in writing Sub-queries and Nested Selects in PgAdmin 4

# Software Used in this Lab

PgAdmin 4 (PostgreSQL 15)

# Database Used in this Lab

The database used in this lab is an internal database belonging to IBM; a sample HR database. This is an HR database schema that consists of 5 tables called EMPLOYEES, JOB_HISTORY, JOBS, DEPARTMENTS and LOCATIONS. Each table has a few rows of sample data. The following diagram shows the tables for the HR database:

![image](https://github.com/user-attachments/assets/067a7925-0c1d-4a68-a62f-6f9879919301)

# Objectives

The objectives of this project were to:

1. Write SQL queries that demonstrate the necessity of using sub-queries
   
3. Compose sub-queries in the where clause
   
5. Build Column Expressions (i.e. sub-query in place of a column)
   
7. Write Table Expressions (i.e. sub-query in place of a table)

# Highlights

- How does a typical Nested SELECT statement syntax look?

SELECT column_name [, column_name ]
FROM table1 [, table2 ]
WHERE column_name OPERATOR
   (SELECT column_name [, column_name ]
   FROM table1 [, table2 ]
   WHERE condition);

# Task A: Creating tables using SQL scripts

In this task, I created my new database named "HR DB" in PgAdmin and then executed the script containing the CREATE TABLE commands for all the tables rather than create each table manually by typing the DDL commands in the SQL editor.

The HR_Database_Create_Tables_Script.sql is available here: https://drive.google.com/file/d/1DOUzVXi-jsWBHR6CLNhAFQYUXdPjKFf7/view?usp=sharing

I downloaded the script file to my computer and uploaded it on my query editor of the HR DB I have initially created.

![image](https://github.com/user-attachments/assets/ebfef8e5-dbae-400c-a72f-260e281a6c94)

# Task B: Loading data into tables

In this task, I loaded all the data into the HR DB Database from .CSV files.

I downloaded the 5 .csv files below to my local computer:

Departments.csv - file is available here: https://drive.google.com/file/d/16srI4TCFh_O8VGfrhd3q-msbFp_472zu/view?usp=sharing

Employees.csv - file is available here: https://drive.google.com/file/d/1LLGie9dXrR9WiFYE7t0vyD0eVCRajRtI/view?usp=sharing

Jobs.csv - file is available here: https://drive.google.com/file/d/1qLTJiiOUfgZ9sk8RIFV_6PlSM66pjUTR/view?usp=sharing

Locations.csv - file is available here: https://drive.google.com/file/d/1WHQja5oaxKn7EqWB0sOSD1sHGZnagSBh/view?usp=sharing

JobsHistory.csv - file is available here: https://drive.google.com/file/d/1-IZUPqwPlkU3BdMV5EW2zZl0tg7jZs7C/view?usp=sharing

To load each table, I did the following steps.

I right-clicked on each table and selected Import tab.

Chose the csv file and clicked on OK to load the csv file.

# Task C: Exploring the Tables

To explore each table in the database, I right-clicked on each table and selected view/edit data to view "All Rows" 

1. Dapartment Table

   ![image](https://github.com/user-attachments/assets/f35245c5-9a25-4c18-a06a-333e9a4fadd8)

3. Employees Table

   ![image](https://github.com/user-attachments/assets/f83d2120-5fb2-486f-857b-9c27353832b2)

5. Jobs Table

   ![image](https://github.com/user-attachments/assets/a9e3931b-0fdd-4949-834c-4297808923d3)

7. Locations Table

   ![image](https://github.com/user-attachments/assets/f75e89be-93ec-4b7d-ac16-63b5368bd9e7)

8. JobsHistory Table
   
   ![image](https://github.com/user-attachments/assets/5bcc6784-ba60-4089-b2b9-21a45554683c)

# Task D: Solving SQL problems Using Sub-queries and Nested Selects

1. Execute a failing query (i.e. one which gives an error) to retrieve all employees records whose salary is lower than the average salary.

   In solving this problem, I issued the following SQL statement, however, failed:

   SELECT * FROM employees 
   WHERE salary < AVG(salary);

   ![image](https://github.com/user-attachments/assets/d5307836-80e5-4260-a8f6-36f4bf464c8a)

2. Execute a working query using a sub-select to retrieve all employees records whose salary is lower than the average salary.

   The following SQL statement solved the problem:

   SELECT * FROM employees 
   WHERE salary < (SELECT AVG(salary)
				      FROM employees);

   ![image](https://github.com/user-attachments/assets/6082e796-119f-448f-abb8-54ecb82abcdb)

3. Execute a failing query (i.e. one which gives an error) to retrieve all employees records with EMP_ID, SALARY and maximum salary as MAX_SALARY in every row.

   In solving this problem, I issued the following SQL statement, however, failed:

   SELECT f_name, l_name, emp_id, salary, MAX(salary) as MAX_SALARY
   FROM employees 
		
   ![image](https://github.com/user-attachments/assets/5850187f-118d-411f-bf1f-9806352eba35)

4. Execute a Column Expression that retrieves all employees records with EMP_ID, SALARY and maximum salary as MAX_SALARY in every row.

   The following SQL statement solved the problem:

   SELECT f_name, l_name, emp_id, salary, (SELECT MAX(salary) FROM employees) AS MAX_SALARY
   FROM employees 

   ![image](https://github.com/user-attachments/assets/6620e192-29f3-4128-b388-6e4a2bd1b8f0)
   
5. Execute a Table Expression for the EMPLOYEES table that excludes columns with sensitive employee data (i.e. does not include columns: SSN, B_DATE, SEX, ADDRESS, SALARY).

   In solving this problem, I created a new view and issued the following SQL statement in the query editor,

   SELECT * FROM ( SELECT emp_id, f_name, l_name, dep_id FROM employees) AS New_employees_table;
		
   ![image](https://github.com/user-attachments/assets/b0ab366e-320f-433d-b0d6-62dcbda8dfda)

