## 08. Implementation of order by, group by, and having.

> This section will contain two practice questions. You may write any one of these in the rough record, while the other will be referred for the lab exam. **But for the fair record, you may only write what is given by the teacher.**

---

### Practise Question 1

Create a table named 'Student' and insert some values. Then answer the questions followed.

`STUDENT (ID_NUMBER, STUDENT_NAME, DEPT, ADDRESS, MARKS, TOTAL, AVERAGE)`

1. Display the student table order by CSE in ascending order.
2. Display the student table order by ID number in descending order.
3. Display the minimum, maximum, and average marks from the student table department using group by operation.
4. Display the distinct departments in minimum, and maximum marks from the student table using group by operation.
5. Display the count id number, and department from the student table by using a group by having a function which is greater than the count id number by order by function in descending order.

#### Performing Queries

##### Prerequisite
```
mysql> CREATE TABLE student (
    ->     ID_NUMBER INT,
    ->     STUDENT_NAME VARCHAR(50),
    ->     DEPT VARCHAR(50),
    ->     ADDRESS VARCHAR(50),
    ->     MARKS INT,
    ->     TOTAL INT,
    ->     AVERAGE INT
    -> );
Query OK, 0 rows affected (0.02 sec)
```
```
mysql> INSERT INTO student VALUES
    ->     (1, 'MANJU', 'CSE', 'ABC', 10, 50, 5),
    ->     (2, 'ANJU', 'CE', 'DEF', 20, 50, 10),
    ->     (3, 'KUNJU', 'EC', 'GHI', 30, 50, 15),
    ->     (4, 'CHINJU', 'EEE', 'JKL', 40, 50, 20),
    ->     (5, 'SANJU', 'MECH', 'MNO', 50, 50, 25),
    ->     (6, 'RENJU', 'CSE', 'PQR', 25, 50, 18),
    ->     (7, 'RINJU', 'CSE', 'STU', 35, 50, 20);
Query OK, 7 rows affected (0.01 sec)
Records: 7  Duplicates: 0  Warnings: 0
```
```
mysql> select * from student;
+-----------+--------------+------+---------+-------+-------+---------+
| ID_NUMBER | STUDENT_NAME | DEPT | ADDRESS | MARKS | TOTAL | AVERAGE |
+-----------+--------------+------+---------+-------+-------+---------+
|         1 | MANJU        | CSE  | ABC     |    10 |    50 |       5 |
|         2 | ANJU         | CE   | DEF     |    20 |    50 |      10 |
|         3 | KUNJU        | EC   | GHI     |    30 |    50 |      15 |
|         4 | CHINJU       | EEE  | JKL     |    40 |    50 |      20 |
|         5 | SANJU        | MECH | MNO     |    50 |    50 |      25 |
|         6 | RENJU        | CSE  | PQR     |    25 |    50 |      18 |
|         7 | RINJU        | CSE  | STU     |    35 |    50 |      20 |
+-----------+--------------+------+---------+-------+-------+---------+
7 rows in set (0.03 sec)
```

##### Question 1
```
mysql> SELECT * FROM student ORDER BY DEPT ASC;
+-----------+--------------+------+---------+-------+-------+---------+
| ID_NUMBER | STUDENT_NAME | DEPT | ADDRESS | MARKS | TOTAL | AVERAGE |
+-----------+--------------+------+---------+-------+-------+---------+
|         2 | ANJU         | CE   | DEF     |    20 |    50 |      10 |
|         1 | MANJU        | CSE  | ABC     |    10 |    50 |       5 |
|         6 | RENJU        | CSE  | PQR     |    25 |    50 |      18 |
|         7 | RINJU        | CSE  | STU     |    35 |    50 |      20 |
|         3 | KUNJU        | EC   | GHI     |    30 |    50 |      15 |
|         4 | CHINJU       | EEE  | JKL     |    40 |    50 |      20 |
|         5 | SANJU        | MECH | MNO     |    50 |    50 |      25 |
+-----------+--------------+------+---------+-------+-------+---------+
7 rows in set (0.00 sec)
```
##### Question 2
```
mysql> SELECT * FROM student ORDER BY ID_NUMBER DESC;
+-----------+--------------+------+---------+-------+-------+---------+
| ID_NUMBER | STUDENT_NAME | DEPT | ADDRESS | MARKS | TOTAL | AVERAGE |
+-----------+--------------+------+---------+-------+-------+---------+
|         7 | RINJU        | CSE  | STU     |    35 |    50 |      20 |
|         6 | RENJU        | CSE  | PQR     |    25 |    50 |      18 |
|         5 | SANJU        | MECH | MNO     |    50 |    50 |      25 |
|         4 | CHINJU       | EEE  | JKL     |    40 |    50 |      20 |
|         3 | KUNJU        | EC   | GHI     |    30 |    50 |      15 |
|         2 | ANJU         | CE   | DEF     |    20 |    50 |      10 |
|         1 | MANJU        | CSE  | ABC     |    10 |    50 |       5 |
+-----------+--------------+------+---------+-------+-------+---------+
7 rows in set (0.00 sec)
```
##### Question 3
```
mysql> SELECT DEPT,
    ->        MIN(MARKS) AS MIN_MARKS,
    ->        MAX(MARKS) AS MAX_MARKS,
    ->        AVG(MARKS) AS AVG_MARKS
    -> FROM student GROUP BY DEPT;
+------+-----------+-----------+-----------+
| DEPT | MIN_MARKS | MAX_MARKS | AVG_MARKS |
+------+-----------+-----------+-----------+
| CSE  |        10 |        35 |   23.3333 |
| CE   |        20 |        20 |   20.0000 |
| EC   |        30 |        30 |   30.0000 |
| EEE  |        40 |        40 |   40.0000 |
| MECH |        50 |        50 |   50.0000 |
+------+-----------+-----------+-----------+
5 rows in set (0.00 sec)
```
##### Question 4
```
mysql> SELECT DEPT,
    ->        MIN(MARKS) AS MIN_MARKS,
    ->        MAX(MARKS) AS MAX_MARKS
    -> FROM student GROUP BY DEPT;
+------+-----------+-----------+
| DEPT | MIN_MARKS | MAX_MARKS |
+------+-----------+-----------+
| CSE  |        10 |        35 |
| CE   |        20 |        20 |
| EC   |        30 |        30 |
| EEE  |        40 |        40 |
| MECH |        50 |        50 |
+------+-----------+-----------+
5 rows in set (0.00 sec)
```
##### Question 5
```
mysql> SELECT COUNT(ID_NUMBER), DEPT FROM student GROUP BY DEPT
    -> HAVING COUNT(ID_NUMBER) > 1 ORDER BY COUNT(ID_NUMBER) DESC;
+------------------+------+
| COUNT(ID_NUMBER) | DEPT |
+------------------+------+
|                3 | CSE  |
+------------------+------+
1 row in set (0.00 sec)
```
---

### Practise Question 2 (Try this for yourself)

Create two tables. MANAGER_ID is the empno of the employee whom the employee reports to. DEPTNO is a foreign key. Insert these values into the department table.

`Dept(Department_Id, Department_Name , Manager_id, Loc)`

`Emp(Emp_no , Emp_name,Job , Salary , Hiredate,Comm , Depno)`

1) Display the name and salary for all employees whose salary is not in the range of 5000 and 35000
2) Display the employee name, job ID, and start date of employees hired between February 20, 1990, and May 1, 1998. Order the query in ascending order by start date.
3) list the name and salary of employees who earn between 5,000 and 12,000, and are in department 2 or 4. Label the columns Employee and Monthly Salary, respectively.
4) Display the name and hire date of every employee who was hired in 1994.
5) Display the name, salary, and commission for all employees who earn commissions. Sort data in descending order of salary and commissions.
6) Display the name and job title of all employees who do not have a manager.
7) Display the names of all employees where the third letter of the name is an 'a'.
8) Display the names of all employees who have an a and an e in their name.
9) Display the name, job, and salary for all employees whose job is sales representative or stock clerk and whose salary is not equal to 2,0000, 4000, or 7,000.
10) Write a query that displays the employee’s names with the first letter capitalized and all other letters lowercase and the length of the name for all employees whose name starts with J, A, or M. Give each column an appropriate label. Sort the results by the employees’ names.
11) For each employee, display the employee’s name, and calculate the number of months between today and the date the employee was hired and years worked. Label the columnMONTHS_WORKED. Order your results by the number of months employed. Round the number of months and years up to the closest whole number.
12) Write a query to display the name, department number, and department name for all employees.
13) Create a query to display the name and hire date of any employee hired after employee Mathew
14) Display the names and hire dates for all employees who were hired before their managers, along with their manager’s names and hire dates. Label the columns Employee, EmpHired, Manager, and Mgr Hired, respectively.
15) Write a query to display the number of people with the same job.
16) Display the manager number and the salary of the lowest-paid employee for that manager. Exclude anyone whose manager is not known. Exclude any groups where the minimum salary is less than 6,000. Sort the output in descending order of salary.
17) Write a query to display each department’s name, location, number of employees, and the average salary for all employees in that department. Label the columns Name, Location, Number of People, and Salary, respectively. Round the average salary to two decimal places.
18) Write a query to display the name and hire date of any employee in the same department as Amit. Exclude JOHN.
19) Write a query that displays the employee numbers and names of all employees who work in a department with any employee whose name contains a u.
20) Display the employee name and department name of all employees who work in a department that has at least 3 employees. Order the list in alphabetical order first by department name, then by employee name.
21) Write a query to list the length of service of the employees (of the form n years and m months).
---
> You can refer [this PDF](pdfs/exp9.pdf) from my repository for the answer.
