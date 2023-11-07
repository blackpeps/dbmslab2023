# 08. Implementation of order by, group by, and having.

## AIM

To implement the order by, group by, having clause

## Theory

- **ORDER BY:** In RDBMS, the ORDER BY clause is used to sort the result set of a query based on one or more columns in ascending or descending order, allowing for the presentation of data in a specific sequence.

- **GROUP BY and HAVING:** GROUP BY is used to group rows with similar values in one or more columns, and HAVING is applied in conjunction with GROUP BY to filter the grouped data based on a specified condition, enabling aggregate functions to be used on the grouped data.

## QUESTIONS

Create a table named 'Student' and insert some values. Then answer the questions followed.

`STUDENT (ID_NUMBER, STUDENT_NAME, DEPT, ADDRESS, MARKS, TOTAL, AVERAGE)`

1. Display the student table order by CSE in ascending order.
2. Display the student table order by ID number in descending order.
3. Display the minimum, maximum, and average marks from the student table department using group by operation.
4. Display the distinct departments in minimum, and maximum marks from the student table using group by operation.
5. Display the count id number, and department from the student table by using a group by having a function which is greater than the count id number by order by function in descending order.

## OUTPUT

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
