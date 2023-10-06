## 12. Practise SQL Commands for creation or view assertion.

> This section will contain two practice questions. One question is a combination of all the topics mentioned. There will be three questions according to each section. You may write any one of these in the rough record, while the other will be referred for the lab exam. **But for the fair record, you may only write what is given by the teacher.**

---

### Practise Question 1

1. Create a table and insert values into the emp55 table.
2. Write a query to display the emp55 from employee55 where salary is greater than 10000.
3. Write a query to update the emp55 table by setting the manager as Anoop where the job is hr.
4. Write a query to display the employee name & department number from the table.
5. Write a query to display the employee number, and employee name who was in a department with any employee whose name contains a 'I'.
6. Write a query to delete a row where the department number is 3.
7. Write a query to view emp55 from employee55 where the common is less than 150 with the check option.
8. Write a query to drop the table.

#### Question 1
```
mysql> CREATE TABLE emp55 (
    ->     EMP_NO VARCHAR(5),
    ->     EMP_NAME VARCHAR(20),
    ->     JOB VARCHAR(20),
    ->     MANAGER VARCHAR(20),
    ->     SALARY INT,
    ->     DEP_NO INT,
    ->     COM_MN INT,
    ->     HIRE_DATE DATE
    -> );
Query OK, 0 rows affected (0.05 sec)
```
```
mysql> INSERT INTO emp55 VALUES
    ->     ('E234', 'SUBIN', 'CLERK', 'DAYAL', 8000, 2, 75, '1998-05-01'),
    ->     ('E563', 'LINSON', 'ACCOUNTANT', 'SREEHARI', 12000, 3, 120, '1999-05-04'),
    ->     ('E101', 'SONNET', 'ANALYST', 'DHANYA', 16000, 1, 280, '1996-05-25'),
    ->     ('E407', 'ANUPAMA', 'PROGRAMMER', 'BINITH', 17000, 4, 180, '2001-07-23'),
    ->     ('E305', 'ALBIN', 'TECHNICIAN', 'SANOOT', 15000, 3, 190, '2000-08-24'),
    ->     ('E497', 'PINTO', 'SUPERVISOR', 'PRINCE', 9000, 5, 0, '2006-07-04'),
    ->     ('E457', 'SAMJITH', 'MANAGER', 'VIMAL', 18000, 1, 200, '2006-06-05');
Query OK, 7 rows affected (0.04 sec)
Records: 7  Duplicates: 0  Warnings: 0
```
```
mysql> select * from emp55;
+--------+----------+------------+----------+--------+--------+--------+------------+
| EMP_NO | EMP_NAME | JOB        | MANAGER  | SALARY | DEP_NO | COM_MN | HIRE_DATE  |
+--------+----------+------------+----------+--------+--------+--------+------------+
| E234   | SUBIN    | CLERK      | DAYAL    |   8000 |      2 |     75 | 1998-05-01 |
| E563   | LINSON   | ACCOUNTANT | SREEHARI |  12000 |      3 |    120 | 1999-05-04 |
| E101   | SONNET   | ANALYST    | DHANYA   |  16000 |      1 |    280 | 1996-05-25 |
| E407   | ANUPAMA  | PROGRAMMER | BINITH   |  17000 |      4 |    180 | 2001-07-23 |
| E305   | ALBIN    | TECHNICIAN | SANOOT   |  15000 |      3 |    190 | 2000-08-24 |
| E497   | PINTO    | SUPERVISOR | PRINCE   |   9000 |      5 |      0 | 2006-07-04 |
| E457   | SAMJITH  | MANAGER    | VIMAL    |  18000 |      1 |    200 | 2006-06-05 |
+--------+----------+------------+----------+--------+--------+--------+------------+
7 rows in set (0.00 sec)
```
#### Question 2
```
mysql> SELECT * FROM emp55 WHERE SALARY > 10000;
+--------+----------+------------+----------+--------+--------+--------+------------+
| EMP_NO | EMP_NAME | JOB        | MANAGER  | SALARY | DEP_NO | COM_MN | HIRE_DATE  |
+--------+----------+------------+----------+--------+--------+--------+------------+
| E563   | LINSON   | ACCOUNTANT | SREEHARI |  12000 |      3 |    120 | 1999-05-04 |
| E101   | SONNET   | ANALYST    | DHANYA   |  16000 |      1 |    280 | 1996-05-25 |
| E407   | ANUPAMA  | PROGRAMMER | BINITH   |  17000 |      4 |    180 | 2001-07-23 |
| E305   | ALBIN    | TECHNICIAN | SANOOT   |  15000 |      3 |    190 | 2000-08-24 |
| E457   | SAMJITH  | MANAGER    | VIMAL    |  18000 |      1 |    200 | 2006-06-05 |
+--------+----------+------------+----------+--------+--------+--------+------------+
5 rows in set (0.00 sec)
```
#### Question 3
```
mysql> UPDATE emp55 SET MANAGER = 'ANOOP' WHERE UPPER(JOB) = 'MANAGER';
Query OK, 1 row affected (0.04 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```
```
mysql> select * from emp55;
+--------+----------+------------+----------+--------+--------+--------+------------+
| EMP_NO | EMP_NAME | JOB        | MANAGER  | SALARY | DEP_NO | COM_MN | HIRE_DATE  |
+--------+----------+------------+----------+--------+--------+--------+------------+
| E234   | SUBIN    | CLERK      | DAYAL    |   8000 |      2 |     75 | 1998-05-01 |
| E563   | LINSON   | ACCOUNTANT | SREEHARI |  12000 |      3 |    120 | 1999-05-04 |
| E101   | SONNET   | ANALYST    | DHANYA   |  16000 |      1 |    280 | 1996-05-25 |
| E407   | ANUPAMA  | PROGRAMMER | BINITH   |  17000 |      4 |    180 | 2001-07-23 |
| E305   | ALBIN    | TECHNICIAN | SANOOT   |  15000 |      3 |    190 | 2000-08-24 |
| E497   | PINTO    | SUPERVISOR | PRINCE   |   9000 |      5 |      0 | 2006-07-04 |
| E457   | SAMJITH  | MANAGER    | ANOOP    |  18000 |      1 |    200 | 2006-06-05 |
+--------+----------+------------+----------+--------+--------+--------+------------+
7 rows in set (0.00 sec)
```
#### Question 4
```
mysql> SELECT EMP_NAME, DEP_NO FROM emp55;
+----------+--------+
| EMP_NAME | DEP_NO |
+----------+--------+
| SUBIN    |      2 |
| LINSON   |      3 |
| SONNET   |      1 |
| ANUPAMA  |      4 |
| ALBIN    |      3 |
| PINTO    |      5 |
| SAMJITH  |      1 |
+----------+--------+
7 rows in set (0.00 sec)
```
#### Question 5
```
mysql> SELECT EMP_NO, EMP_NAME FROM emp55
    -> WHERE DEP_NO IN (SELECT DEP_NO FROM emp55 WHERE EMP_NAME LIKE '%I%');
+--------+----------+
| EMP_NO | EMP_NAME |
+--------+----------+
| E234   | SUBIN    |
| E563   | LINSON   |
| E101   | SONNET   |
| E305   | ALBIN    |
| E497   | PINTO    |
| E457   | SAMJITH  |
+--------+----------+
6 rows in set (0.00 sec)
```
#### Question 6
```
mysql> DELETE FROM emp55 WHERE DEP_NO = 3;
Query OK, 2 rows affected (0.04 sec)
```
```
mysql> select * from emp55;
+--------+----------+------------+---------+--------+--------+--------+------------+
| EMP_NO | EMP_NAME | JOB        | MANAGER | SALARY | DEP_NO | COM_MN | HIRE_DATE  |
+--------+----------+------------+---------+--------+--------+--------+------------+
| E234   | SUBIN    | CLERK      | DAYAL   |   8000 |      2 |     75 | 1998-05-01 |
| E101   | SONNET   | ANALYST    | DHANYA  |  16000 |      1 |    280 | 1996-05-25 |
| E407   | ANUPAMA  | PROGRAMMER | BINITH  |  17000 |      4 |    180 | 2001-07-23 |
| E497   | PINTO    | SUPERVISOR | PRINCE  |   9000 |      5 |      0 | 2006-07-04 |
| E457   | SAMJITH  | MANAGER    | ANOOP   |  18000 |      1 |    200 | 2006-06-05 |
+--------+----------+------------+---------+--------+--------+--------+------------+
5 rows in set (0.00 sec)
```
#### Question 7
```
mysql> CREATE VIEW emp55_view AS
    -> SELECT * FROM emp55 WHERE COM_MN < 150
    -> WITH CHECK OPTION;
Query OK, 0 rows affected (0.04 sec)
```
```
mysql> SELECT * FROM emp55_view;
+--------+----------+------------+---------+--------+--------+--------+------------+
| EMP_NO | EMP_NAME | JOB        | MANAGER | SALARY | DEP_NO | COM_MN | HIRE_DATE  |
+--------+----------+------------+---------+--------+--------+--------+------------+
| E234   | SUBIN    | CLERK      | DAYAL   |   8000 |      2 |     75 | 1998-05-01 |
| E497   | PINTO    | SUPERVISOR | PRINCE  |   9000 |      5 |      0 | 2006-07-04 |
+--------+----------+------------+---------+--------+--------+--------+------------+
2 rows in set (0.04 sec)
```
#### Question 8
```
mysql> drop table emp55;
Query OK, 0 rows affected (0.04 sec)
```
