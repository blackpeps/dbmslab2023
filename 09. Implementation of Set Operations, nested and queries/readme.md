# 09. IMPLEMENTATION OF SET OPERATOR, NESTED QUERIES AND JOIN QUERIES

## Aim

To implement set operators, nested queries and join queries

## Set Operators

### Theory

In RDBMS, SET operators like UNION, INTERSECT, and EXCEPT are used to combine the results of two or more SELECT statements into a single result set, with UNION combining all results, INTERSECT returning common rows, and EXCEPT returning rows not found in the second result set.

### Questions

Consider this schema.

`Employee1(id, fname, lname, dept, designation, salary)`

`Employee2(id, fname, lname, dept, designation, salary)`

1. Display all the employee details from employees 1 & 2 using union all.
2. Display all the employee details from employees 1 & 2 using the union.
3. Display all the employee details from employees 1 & 2 using union & order by fname.
4. Display all the employee details from employee 1 where fname in & fname from employee 2.
5. Display all the employee details from employee 1 where fname is not in & fname from employee 2.

## Nested Queries

### Theory

In RDBMS, nested queries involve using one SQL query inside another, where the inner query depends on the result of the outer query, allowing for complex filtering and retrieval of data based on subqueries within the main query.

### Questions

Consider the schema.

`Employee55(empno,ename,job,manager,sal,deptno,commn,hiredate)`

1. Write a SQL query to display the lastname, hiredate of any employee in the same department as "Albin", and exclude Albin.
2. Write a query to display employee number, lastname and salary of all employees who earn more than the average salary. Sort the result in ascending order.
3. Write a query to display employee number, lastname of all employees who were in a department with any employee whose last name contains a 'U'.

## Join Queries

### Theory 

Join queries in RDBMS combine data from multiple tables based on a related column, allowing you to retrieve information from different tables in a single query using JOIN clauses like INNER JOIN, LEFT JOIN, RIGHT JOIN, and FULL JOIN.

### Questions

Consider the schema.

`Members(member_id,name)`

`Committees(committee_id,name)`

1. Find members who are also committee members (using join).
2. Join the members with the committee table using left join.
3. Join the members at the committee table using the right join.
4. Join the members with the committees' table using cross-join.

## Output

### Set Operators

```
mysql> CREATE TABLE Employee1 (
    ->     id INT,
    ->     fname VARCHAR(50),
    ->     lname VARCHAR(50),
    ->     dept VARCHAR(50),
    ->     designation VARCHAR(50),
    ->     salary DECIMAL(10, 2)
    -> );
Query OK, 0 rows affected (0.06 sec)
```
```
mysql> CREATE TABLE Employee2 (
    ->     id INT,
    ->     fname VARCHAR(50),
    ->     lname VARCHAR(50),
    ->     dept VARCHAR(50),
    ->     designation VARCHAR(50),
    ->     salary DECIMAL(10, 2)
    -> );
Query OK, 0 rows affected (0.05 sec)
```
```
mysql> INSERT INTO Employee1 VALUES
    ->     (1, 'John', 'Doe', 'HR', 'Manager', 55000.00),
    ->     (2, 'Jane', 'Smith', 'IT', 'Developer', 60000.00),
    ->     (3, 'Bob', 'Johnson', 'Finance', 'Accountant', 50000.00),
    ->     (4, 'Alice', 'Brown', 'Marketing', 'Coordinator', 48000.00),
    ->     (5, 'Ella', 'White', 'HR', 'Assistant', 40000.00);
Query OK, 5 rows affected (0.04 sec)
Records: 5  Duplicates: 0  Warnings: 0
```
```
mysql> select * from Employee1;
+------+-------+---------+-----------+-------------+----------+
| id   | fname | lname   | dept      | designation | salary   |
+------+-------+---------+-----------+-------------+----------+
|    1 | John  | Doe     | HR        | Manager     | 55000.00 |
|    2 | Jane  | Smith   | IT        | Developer   | 60000.00 |
|    3 | Bob   | Johnson | Finance   | Accountant  | 50000.00 |
|    4 | Alice | Brown   | Marketing | Coordinator | 48000.00 |
|    5 | Ella  | White   | HR        | Assistant   | 40000.00 |
+------+-------+---------+-----------+-------------+----------+
5 rows in set (0.00 sec)
```
```
mysql> INSERT INTO Employee2 (id, fname, lname, dept, designation, salary)
    -> VALUES
    ->     (5, 'Ella', 'White', 'HR', 'Assistant', 40000.00),
    ->     (6, 'Mike', 'Williams', 'IT', 'Manager', 65000.00),
    ->     (7, 'Grace', 'Anderson', 'Finance', 'Analyst', 52000.00),
    ->     (8, 'David', 'Clark', 'Marketing', 'Coordinator', 48000.00);
Query OK, 4 rows affected (0.04 sec)
Records: 4  Duplicates: 0  Warnings: 0
```
```
mysql> select * from Employee2;
+------+-------+----------+-----------+-------------+----------+
| id   | fname | lname    | dept      | designation | salary   |
+------+-------+----------+-----------+-------------+----------+
|    5 | Ella  | White    | HR        | Assistant   | 40000.00 |
|    6 | Mike  | Williams | IT        | Manager     | 65000.00 |
|    7 | Grace | Anderson | Finance   | Analyst     | 52000.00 |
|    8 | David | Clark    | Marketing | Coordinator | 48000.00 |
+------+-------+----------+-----------+-------------+----------+
4 rows in set (0.00 sec)
```

##### Question 1
```
mysql> SELECT * FROM Employee1 UNION ALL
    -> SELECT * FROM Employee2;
+------+-------+----------+-----------+-------------+----------+
| id   | fname | lname    | dept      | designation | salary   |
+------+-------+----------+-----------+-------------+----------+
|    1 | John  | Doe      | HR        | Manager     | 55000.00 |
|    2 | Jane  | Smith    | IT        | Developer   | 60000.00 |
|    3 | Bob   | Johnson  | Finance   | Accountant  | 50000.00 |
|    4 | Alice | Brown    | Marketing | Coordinator | 48000.00 |
|    5 | Ella  | White    | HR        | Assistant   | 40000.00 |
|    5 | Ella  | White    | HR        | Assistant   | 40000.00 |
|    6 | Mike  | Williams | IT        | Manager     | 65000.00 |
|    7 | Grace | Anderson | Finance   | Analyst     | 52000.00 |
|    8 | David | Clark    | Marketing | Coordinator | 48000.00 |
+------+-------+----------+-----------+-------------+----------+
9 rows in set (0.00 sec)
```
##### Question 2
```
mysql> SELECT * FROM Employee1 UNION
    -> SELECT * FROM Employee2;
+------+-------+----------+-----------+-------------+----------+
| id   | fname | lname    | dept      | designation | salary   |
+------+-------+----------+-----------+-------------+----------+
|    1 | John  | Doe      | HR        | Manager     | 55000.00 |
|    2 | Jane  | Smith    | IT        | Developer   | 60000.00 |
|    3 | Bob   | Johnson  | Finance   | Accountant  | 50000.00 |
|    4 | Alice | Brown    | Marketing | Coordinator | 48000.00 |
|    5 | Ella  | White    | HR        | Assistant   | 40000.00 |
|    6 | Mike  | Williams | IT        | Manager     | 65000.00 |
|    7 | Grace | Anderson | Finance   | Analyst     | 52000.00 |
|    8 | David | Clark    | Marketing | Coordinator | 48000.00 |
+------+-------+----------+-----------+-------------+----------+
8 rows in set (0.00 sec)
```
##### Question 3
```
mysql> SELECT * FROM Employee1 UNION
    -> SELECT * FROM Employee2 ORDER BY fname;
+------+-------+----------+-----------+-------------+----------+
| id   | fname | lname    | dept      | designation | salary   |
+------+-------+----------+-----------+-------------+----------+
|    4 | Alice | Brown    | Marketing | Coordinator | 48000.00 |
|    3 | Bob   | Johnson  | Finance   | Accountant  | 50000.00 |
|    8 | David | Clark    | Marketing | Coordinator | 48000.00 |
|    5 | Ella  | White    | HR        | Assistant   | 40000.00 |
|    7 | Grace | Anderson | Finance   | Analyst     | 52000.00 |
|    2 | Jane  | Smith    | IT        | Developer   | 60000.00 |
|    1 | John  | Doe      | HR        | Manager     | 55000.00 |
|    6 | Mike  | Williams | IT        | Manager     | 65000.00 |
+------+-------+----------+-----------+-------------+----------+
8 rows in set (0.00 sec)
```
##### Question 4
```
mysql> SELECT * FROM Employee1
    -> WHERE fname IN (SELECT fname FROM Employee2);
+------+-------+-------+------+-------------+----------+
| id   | fname | lname | dept | designation | salary   |
+------+-------+-------+------+-------------+----------+
|    5 | Ella  | White | HR   | Assistant   | 40000.00 |
+------+-------+-------+------+-------------+----------+
1 row in set (0.01 sec)
```
##### Question 5
```
mysql> SELECT * FROM Employee1
    -> WHERE fname NOT IN (SELECT fname FROM Employee2);
+------+-------+---------+-----------+-------------+----------+
| id   | fname | lname   | dept      | designation | salary   |
+------+-------+---------+-----------+-------------+----------+
|    1 | John  | Doe     | HR        | Manager     | 55000.00 |
|    2 | Jane  | Smith   | IT        | Developer   | 60000.00 |
|    3 | Bob   | Johnson | Finance   | Accountant  | 50000.00 |
|    4 | Alice | Brown   | Marketing | Coordinator | 48000.00 |
+------+-------+---------+-----------+-------------+----------+
4 rows in set (0.00 sec)
```
---

### Nested Queries

```
mysql> CREATE TABLE Employee55 (
    ->     empno INT PRIMARY KEY,
    ->     ename VARCHAR(50),
    ->     job VARCHAR(50),
    ->     manager INT,
    ->     sal DECIMAL(10, 2),
    ->     deptno INT,
    ->     commn DECIMAL(10, 2),
    ->     hiredate DATE
    -> );
Query OK, 0 rows affected (0.04 sec)
```
```
mysql> INSERT INTO Employee55 VALUES
    ->     (1, 'Samuel', 'Manager', NULL, 6000.00, 1, NULL, '2023-01-15'),
    ->     (2, 'Lucas', 'Manager', NULL, 5500.00, 1, NULL, '2023-02-20'),
    ->     (3, 'Sarah', 'Clerk', 1, 3500.00, 1, NULL, '2023-03-10'),
    ->     (4, 'Michael', 'Clerk', 2, 3200.00, 2, NULL, '2023-04-05'),
    ->     (5, 'Tom', 'Manager', NULL, 7000.00, 3, NULL, '2023-05-12'),
    ->     (6, 'Albin', 'Clerk', 5, 3800.00, 3, NULL, '2023-06-18'),
    ->     (7, 'Paul', 'Analyst', 2, 4500.00, 2, NULL, '2023-07-25'),
    ->     (8, 'Mary', 'Clerk', 1, 3300.00, 1, NULL, '2023-08-30');
Query OK, 8 rows affected (0.00 sec)
Records: 8  Duplicates: 0  Warnings: 0
```
```
mysql> select * from Employee55;
+-------+---------+---------+---------+---------+--------+-------+------------+
| empno | ename   | job     | manager | sal     | deptno | commn | hiredate   |
+-------+---------+---------+---------+---------+--------+-------+------------+
|     1 | Samuel  | Manager |    NULL | 6000.00 |      1 |  NULL | 2023-01-15 |
|     2 | Lucas   | Manager |    NULL | 5500.00 |      1 |  NULL | 2023-02-20 |
|     3 | Sarah   | Clerk   |       1 | 3500.00 |      1 |  NULL | 2023-03-10 |
|     4 | Michael | Clerk   |       2 | 3200.00 |      2 |  NULL | 2023-04-05 |
|     5 | Tom     | Manager |    NULL | 7000.00 |      3 |  NULL | 2023-05-12 |
|     6 | Albin   | Clerk   |       5 | 3800.00 |      3 |  NULL | 2023-06-18 |
|     7 | Paul    | Analyst |       2 | 4500.00 |      2 |  NULL | 2023-07-25 |
|     8 | Mary    | Clerk   |       1 | 3300.00 |      1 |  NULL | 2023-08-30 |
+-------+---------+---------+---------+---------+--------+-------+------------+
8 rows in set (0.00 sec)
```
##### Question 1
```
mysql> SELECT ename, hiredate FROM Employee55
    -> WHERE deptno = (SELECT deptno FROM Employee55 WHERE ename = 'Albin') AND ename <> 'Albin';
+---------+------------+
| ename   | hiredate   |
+---------+------------+
| Tom     | 2023-05-12 |
+---------+------------+
1 row in set (0.00 sec)
```
##### Question 2
```
mysql> SELECT empno, ename, sal FROM Employee55
    -> WHERE sal > (SELECT AVG(sal) FROM Employee55) ORDER BY sal ASC;
+-------+---------+---------+
| empno | ename   | sal     |
+-------+---------+---------+
|     2 | Lucas   | 5500.00 |
|     1 | Samuel  | 6000.00 |
|     5 | Tom     | 7000.00 |
+-------+---------+---------+
3 rows in set (0.00 sec)
```
##### Question 3
```
mysql> SELECT empno, ename FROM Employee55
    -> WHERE deptno IN (
    ->     SELECT DISTINCT deptno
    ->     FROM Employee55
    ->     WHERE ename LIKE '%U%'
    -> );
+-------+---------+
| empno | ename   |
+-------+---------+
|     1 | Samuel  |
|     2 | Lucas   |
|     7 | Paul    |
+-------+---------+
3 rows in set (0.00 sec)
```
---

### Join Queries

```
mysql> CREATE TABLE Members (
    ->     member_id INT PRIMARY KEY,
    ->     name VARCHAR(255)
    -> );
Query OK, 0 rows affected (0.04 sec)
```
```
mysql> INSERT INTO Members (member_id, name)
    -> VALUES
    ->     (1, 'John'),
    ->     (2, 'Jane'),
    ->     (3, 'Alice'),
    ->     (4, 'Bob');
Query OK, 4 rows affected (0.04 sec)
Records: 4  Duplicates: 0  Warnings: 0
```
```
mysql> select * from Members;
+-----------+-------+
| member_id | name  |
+-----------+-------+
|         1 | John  |
|         2 | Jane  |
|         3 | Alice |
|         4 | Bob   |
+-----------+-------+
4 rows in set (0.00 sec)
```
```
mysql> CREATE TABLE Committees (
    ->     committee_id INT PRIMARY KEY,
    ->     name VARCHAR(255)
    -> );
Query OK, 0 rows affected (0.04 sec)
```
```
mysql> INSERT INTO Committees (committee_id, name)
    -> VALUES
    ->     (1, 'Bob'),
    ->     (2, 'Jane'),
    ->     (3, 'Mandissa'),
    ->     (4, 'Tom');
Query OK, 4 rows affected (0.04 sec)
Records: 4  Duplicates: 0  Warnings: 0
```
##### Question 1
```
mysql> SELECT M.name AS name FROM Members M
    -> JOIN Committees C ON M.name = C.name;
+------+
| name |
+------+
| Bob  |
| Jane |
+------+
2 rows in set (0.04 sec)
```
##### Question 2
```
mysql> SELECT M.name AS member_name, C.name AS committee_name
    -> FROM Members M
    -> LEFT JOIN Committees C ON M.name = C.name;
+-------------+----------------+
| member_name | committee_name |
+-------------+----------------+
| John        | NULL           |
| Jane        | Jane           |
| Alice       | NULL           |
| Bob         | Bob            |
+-------------+----------------+
4 rows in set (0.00 sec)
```
##### Question 3
```
mysql> SELECT M.name AS member_name, C.name AS committee_name
    -> FROM Members M
    -> RIGHT JOIN Committees C ON M.name = C.name;
+-------------+----------------+
| member_name | committee_name |
+-------------+----------------+
| Bob         | Bob            |
| Jane        | Jane           |
| NULL        | Mandissa       |
| NULL        | Tom            |
+-------------+----------------+
4 rows in set (0.00 sec)
```
##### Question 4
```
mysql> SELECT M.name AS member_name, C.name AS committee_name
    -> FROM Members M
    -> CROSS JOIN Committees C;
+-------------+----------------+
| member_name | committee_name |
+-------------+----------------+
| Bob         | Bob            |
| Alice       | Bob            |
| Jane        | Bob            |
| John        | Bob            |
| Bob         | Jane           |
| Alice       | Jane           |
| Jane        | Jane           |
| John        | Jane           |
| Bob         | Mandissa       |
| Alice       | Mandissa       |
| Jane        | Mandissa       |
| John        | Mandissa       |
| Bob         | Tom            |
| Alice       | Tom            |
| Jane        | Tom            |
| John        | Tom            |
+-------------+----------------+
16 rows in set (0.00 sec)
```
