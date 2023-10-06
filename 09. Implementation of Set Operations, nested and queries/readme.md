## 08. Implementation of order by, group by, and having.

> This section will contain two practice questions. You may write any one of these in the rough record, while the other will be referred for the lab exam. **But for the fair record, you may only write what is given by the teacher.**

---

### Set Operators

Consider this schema.

`Employee1(id, fname, lname, dept, designation, salary)`

`Employee2(id, fname, lname, dept, designation, salary)`

1. Display all the employee details from employee 1 & 2 using union all.
2. Display all the employee details from employee 1 & 2 using union.
3. Display all the employee details from employee 1 & 2 using union & order by fname.
4. Display all the employee details from employee 1 where fname in & fname from employee 2.
5. Display all the employee details from employee 1 where fname not in & fname from employee 2.

#### Performing Queries

##### Prerequisite

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

Consider the schema.

`Employee55(empno,ename,job,manager,sal,deptno,commn,hiredate)`

1. Write a SQL query to display the lastname, hiredate of any employee in the same department as "Albin", and exclude Albin.
2. Write a query to display employee number, lastname and salary of all employees who earn more than the average salary. Sort the result in ascending order.
3. Write a query to display employee number, lastname of all employees who were in a department with any employee whose last name contains a 'U'.

#### Performing Queries

##### Prerequisite
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

Consider the schema.

`Members(member_id,name)`

`Committees(committee_id,name)`

1. Find members who are also committee members (using join).
2. Join the members with the committee table using left join.
3. Join the members at the committee table using the right join.
4. Join the members with the committees' table using cross-join.

   mysql> CREATE TABLE Members (
    ->     member_id INT PRIMARY KEY,
    ->     name VARCHAR(255)
    -> );
Query OK, 0 rows affected (0.04 sec)

#### Performing Queries

##### Prerequisites
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
---

### Practise Questions

Consider the schema for MovieDatabase:

`ACTOR (Act_id, Act_Name, Act_Gender)`

`DIRECTOR (Dir_id, Dir_Name, Dir_Phone)`

`MOVIES (Mov_id, Mov_Title, Mov_Year, Mov_Lang, Dir_id)`

`MOVIE_CAST (Act_id, Mov_id, Role) RATING (Mov_id, Rev_Stars)`

1. List the titles of all movies directed by ‘Hitchcock’.
2. Find the movie names where one or more actors acted in two or more movies.
3. List all actors who acted in a movie before 2000 and also in a movie after 2015 (use JOIN operation).
4. Find the title of the movie and the number of stars for each movie that has at least one rating and find the highest number of stars that movie received. Sort the result by movie title.
5. Update the rating of all movies directed by ‘Steven Spielberg to 5.

#### Performing Queries

##### Prerequisite
```
mysql> CREATE TABLE ACTOR (
    ->     ACT_ID INT(3) PRIMARY KEY,
    ->     ACT_NAME VARCHAR(20),
    ->     ACT_GENDER CHAR(1)
    -> );
Query OK, 0 rows affected, 1 warning (0.05 sec)
```
```
mysql> CREATE TABLE DIRECTOR (
    ->     DIR_ID INT(3) PRIMARY KEY,
    ->     DIR_NAME VARCHAR(20),
    ->     DIR_PHONE INT(10)
    -> );
Query OK, 0 rows affected, 2 warnings (0.03 sec)
```
```
mysql> CREATE TABLE MOVIES (
    ->     MOV_ID INT(4) PRIMARY KEY,
    ->     MOV_TITLE VARCHAR(25),
    ->     MOV_YEAR INT(4),
    ->     MOV_LANG VARCHAR(12),
    ->     DIR_ID INT(3),
    ->     FOREIGN KEY (DIR_ID) REFERENCES DIRECTOR(DIR_ID)
    -> );
Query OK, 0 rows affected, 3 warnings (0.07 sec)
```
```
mysql> CREATE TABLE MOVIE_CAST (
    ->     ACT_ID INT(3),
    ->     MOV_ID INT(4),
    ->     ROLE VARCHAR(10),
    ->     PRIMARY KEY (ACT_ID, MOV_ID),
    ->     FOREIGN KEY (ACT_ID) REFERENCES ACTOR(ACT_ID),
    ->     FOREIGN KEY (MOV_ID) REFERENCES MOVIES(MOV_ID)
    -> );
Query OK, 0 rows affected, 2 warnings (0.05 sec)
```
```
mysql> CREATE TABLE RATING (
    ->     MOV_ID INT(4) PRIMARY KEY,
    ->     REV_STARS VARCHAR(25),
    ->     FOREIGN KEY (MOV_ID) REFERENCES MOVIES(MOV_ID)
    -> );
Query OK, 0 rows affected, 1 warning (0.06 sec)
```
```
mysql> INSERT INTO ACTOR (ACT_ID, ACT_NAME, ACT_GENDER) VALUES
    -> (301, 'ANUSHKA', 'F'),
    -> (302, 'PRABHAS', 'M'),
    -> (303, 'PUNITH', 'M'),
    -> (304, 'JERMY', 'M');
Query OK, 4 rows affected (0.00 sec)
Records: 4  Duplicates: 0  Warnings: 0
```
```
mysql> INSERT INTO DIRECTOR (DIR_ID, DIR_NAME, DIR_PHONE) VALUES
    -> (60, 'RAJAMOULI', 51611001),
    -> (61, 'HITCHCOCK', 66138911),
    -> (62, 'FARAN', 86776531),
    -> (63, 'STEVEN SPIELBERG', 89776530);
Query OK, 4 rows affected (0.04 sec)
Records: 4  Duplicates: 0  Warnings: 0
```
```
mysql> INSERT INTO MOVIES (MOV_ID, MOV_TITLE, MOV_YEAR, MOV_LANG, DIR_ID) VALUES
    -> (1001, 'BAHUBALI-2', 2017, 'TELAGU', 60),
    -> (1002, 'BAHUBALI-1', 2015, 'TELAGU', 60),
    -> (1003, 'AKASH', 2008, 'KANNADA', 61),
    -> (1004, 'WAR HORSE', 2011, 'ENGLISH', 63);
Query OK, 4 rows affected (0.01 sec)
Records: 4  Duplicates: 0  Warnings: 0
```
```
mysql> INSERT INTO MOVIE_CAST (ACT_ID, MOV_ID, ROLE) VALUES
    -> (301, 1002, 'HEROINE'),
    -> (301, 1001, 'HEROINE'),
    -> (303, 1003, 'HERO'),
    -> (303, 1002, 'GUEST'),
    -> (304, 1004, 'HERO');
Query OK, 5 rows affected (0.04 sec)
Records: 5  Duplicates: 0  Warnings: 0
```
```
mysql> INSERT INTO RATING (MOV_ID, REV_STARS) VALUES
    -> (1001, '4'),
    -> (1002, '2'),
    -> (1003, '5'),
    -> (1004, '4');
Query OK, 4 rows affected (0.04 sec)
Records: 4  Duplicates: 0  Warnings: 0
```
```
mysql> select * from ACTOR;
+--------+----------+------------+
| ACT_ID | ACT_NAME | ACT_GENDER |
+--------+----------+------------+
|    301 | ANUSHKA  | F          |
|    302 | PRABHAS  | M          |
|    303 | PUNITH   | M          |
|    304 | JERMY    | M          |
+--------+----------+------------+
4 rows in set (0.00 sec)
```
```
mysql> SELECT * FROM DIRECTOR;
+--------+------------------+-----------+
| DIR_ID | DIR_NAME         | DIR_PHONE |
+--------+------------------+-----------+
|     60 | RAJAMOULI        |  51611001 |
|     61 | HITCHCOCK        |  66138911 |
|     62 | FARAN            |  86776531 |
|     63 | STEVEN SPIELBERG |  89776530 |
+--------+------------------+-----------+
4 rows in set (0.00 sec)
```
```
mysql> SELECT * FROM MOVIES;
+--------+------------+----------+----------+--------+
| MOV_ID | MOV_TITLE  | MOV_YEAR | MOV_LANG | DIR_ID |
+--------+------------+----------+----------+--------+
|   1001 | BAHUBALI-2 |     2017 | TELAGU   |     60 |
|   1002 | BAHUBALI-1 |     2015 | TELAGU   |     60 |
|   1003 | AKASH      |     2008 | KANNADA  |     61 |
|   1004 | WAR HORSE  |     2011 | ENGLISH  |     63 |
+--------+------------+----------+----------+--------+
4 rows in set (0.00 sec)
```
```
mysql> SELECT * FROM MOVIE_CAST;
+--------+--------+---------+
| ACT_ID | MOV_ID | ROLE    |
+--------+--------+---------+
|    301 |   1001 | HEROINE |
|    301 |   1002 | HEROINE |
|    303 |   1002 | GUEST   |
|    303 |   1003 | HERO    |
|    304 |   1004 | HERO    |
+--------+--------+---------+
5 rows in set (0.00 sec)
```
```
mysql> SELECT * FROM RATING;
+--------+-----------+
| MOV_ID | REV_STARS |
+--------+-----------+
|   1001 | 4         |
|   1002 | 2         |
|   1003 | 5         |
|   1004 | 4         |
+--------+-----------+
4 rows in set (0.00 sec)
```

##### Question 1

```
mysql> SELECT MOV_TITLE
    -> FROM MOVIES
    -> WHERE DIR_ID = (SELECT DIR_ID FROM DIRECTOR WHERE DIR_NAME = 'Hitchcock');
+-----------+
| MOV_TITLE |
+-----------+
| AKASH     |
+-----------+
1 row in set (0.04 sec)
```
##### Question 2
```
mysql> SELECT M.MOV_TITLE FROM MOVIES M
    -> WHERE M.MOV_ID IN (
    ->     SELECT MOV_ID FROM MOVIE_CAST
    ->     WHERE ACT_ID IN (
    ->         SELECT ACT_ID FROM MOVIE_CAST
    ->         GROUP BY ACT_ID HAVING COUNT(DISTINCT MOV_ID) >= 2
    ->     )
    -> );
+------------+
| MOV_TITLE  |
+------------+
| BAHUBALI-2 |
| BAHUBALI-1 |
| AKASH      |
+------------+
3 rows in set (0.04 sec)
```
##### Question 3
```
mysql> SELECT A.ACT_NAME, M.MOV_TITLE, M.MOV_YEAR FROM ACTOR A
    -> JOIN MOVIE_CAST C ON A.ACT_ID = C.ACT_ID
    -> JOIN MOVIES M ON C.MOV_ID = M.MOV_ID
    -> WHERE M.MOV_YEAR NOT BETWEEN 2000 AND 2015;
+----------+------------+----------+
| ACT_NAME | MOV_TITLE  | MOV_YEAR |
+----------+------------+----------+
| ANUSHKA  | BAHUBALI-2 |     2017 |
+----------+------------+----------+
1 row in set (0.00 sec)
```
##### Question 4
```
mysql> SELECT M.MOV_TITLE, R.REV_STARS
    -> FROM MOVIES M
    -> JOIN RATING R ON M.MOV_ID = R.MOV_ID
    -> WHERE M.MOV_ID IN (SELECT MOV_ID FROM RATING)
    -> ORDER BY M.MOV_TITLE, R.REV_STARS DESC;
+------------+-----------+
| MOV_TITLE  | REV_STARS |
+------------+-----------+
| AKASH      | 5         |
| BAHUBALI-1 | 2         |
| BAHUBALI-2 | 4         |
| WAR HORSE  | 4         |
+------------+-----------+
4 rows in set (0.00 sec)
```
##### Question 5
```
mysql> UPDATE RATING SET REV_STARS = '5'
    -> WHERE MOV_ID IN (SELECT MOV_ID FROM MOVIES WHERE DIR_ID = (SELECT DIR_ID FROM DIRECTOR WHERE DIR_NAME = 'Steven Spielberg'));
Query OK, 1 row affected (0.04 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```
```
mysql> Select * From RATING;
+--------+-----------+
| MOV_ID | REV_STARS |
+--------+-----------+
|   1001 | 4         |
|   1002 | 2         |
|   1003 | 5         |
|   1004 | 5         |
+--------+-----------+
4 rows in set (0.00 sec)
```
