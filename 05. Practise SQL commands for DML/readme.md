# 05. Practise SQL commands for DML.

## Notes

- All the writings in this file should be written on the right side of the fair record **unless specified not to write**.
- The PDF for the left side of the fair record can be downloaded from the link given below. Leave pages to paste them by estimating the space required.
- **OUTPUT SHOULD NOT BE WRITTEN ON THE FAIR RECORD** unless you are crazy and do have a lot of time to waste.

### PDF for the Left Side of the fair record

| [Download Now](https://github.com/blackpeps/dbmslab2023/files/13198236/EXP05.pdf) |
| --- |

> Any number of variations made to the PDF will be updated in this link.

> **I'm not responsible for you getting an older revision of the PDF through WhatsApp or any other sources.**

---

## AIM

To familiarize different SQL commands.

## QUESTIONS

1. Create a table EMPLOYEE.
2. Add the column 'experience' to the table EMPLOYEE.
3. Show the structure of the table EMPLOYEE.
4. Insert five different rows to table relevant data.
5. Display the table EMPLOYEE.
6. Update the EMPLOYEE table where set job = programmer where dept=it
7. Delete an employee from the table whose emp_no is 101
8. Display the details of emp_name, job, and salary from EMPLOYEE.
9. Insert two different rows to the table EMPLOYEE.
10. Display emp_name, job, and salary from the EMPLOYEE table.
11. Update the salary = 25000 where job = tester from the EMPLOYEE table.
12. Display the salary by order from the employee table.
13. Display the salary in descending order from the EMPLOYEE table.
14. Display the details of employees whose salary is greater than 25000.
15. Display the distinct department from the table EMPLOYEE.
16. Display the emp_no and emp_name from the EMPLOYEE table where the salary is between 3000 and 45000.
17. Display the emp_no and emp_name from the EMPLOYEE table where emp_name should start with “S”.
18. Display the emp_no and emp_name from the table where department=IT and emp_name is greater than 110.
19. Display emp_no and emp_name from the table where department=IT or emp_name is greater than 110
20. Rename the table EMPLOYEE to EMPLY.
21. Display the distinct employee name from the table EMPLOYEE.

## OUTPUT

```
mysql> create database exp005;
Query OK, 1 row affected (0.04 sec)
```
```
mysql> use exp005;
Database changed
```

### Question 1
```
mysql> CREATE TABLE EMPLOYEE (EMPNUM INT(10),EMPNAME VARCHAR(25),JOB VARCHAR(15),SALARY INT(12),DEPT VARCHAR(5));
Query OK, 0 rows affected, 2 warnings (0.01 sec)
```
```
mysql> desc employee;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| EMPNUM  | int         | YES  |     | NULL    |       |
| EMPNAME | varchar(25) | YES  |     | NULL    |       |
| JOB     | varchar(15) | YES  |     | NULL    |       |
| SALARY  | int         | YES  |     | NULL    |       |
| DEPT    | varchar(5)  | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)
```

### Question 2
```
mysql> ALTER TABLE EMPLOYEE ADD EXPERIENCE INT(10);
Query OK, 0 rows affected, 1 warning (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 1
```

### Question 3
```
mysql> desc employee;
+------------+-------------+------+-----+---------+-------+
| Field      | Type        | Null | Key | Default | Extra |
+------------+-------------+------+-----+---------+-------+
| EMPNUM     | int         | YES  |     | NULL    |       |
| EMPNAME    | varchar(25) | YES  |     | NULL    |       |
| JOB        | varchar(15) | YES  |     | NULL    |       |
| SALARY     | int         | YES  |     | NULL    |       |
| DEPT       | varchar(5)  | YES  |     | NULL    |       |
| EXPERIENCE | int         | YES  |     | NULL    |       |
+------------+-------------+------+-----+---------+-------+
6 rows in set (0.00 sec)
```

### Question 4
```
mysql> INSERT INTO EMPLOYEE VALUES
    -> (100,"SANJU","HECKER",40000,"IT",3),
    -> (101,"MANJU","PROGRAMMER",25000,"IT",2),
    -> (102,"KUNJU","MANAGER",60000,"HR",5),
    -> (103,"ANJU","INSTRUCTOR",55000,"HR",3),
    -> (104,"RENJU","SUPERVISOR",40000,"IT",3);
Query OK, 5 rows affected (0.05 sec)
Records: 5  Duplicates: 0  Warnings: 0
```

### Question 5
```
mysql> SELECT * FROM EMPLOYEE;
+--------+---------+------------+--------+------+------------+
| EMPNUM | EMPNAME | JOB        | SALARY | DEPT | EXPERIENCE |
+--------+---------+------------+--------+------+------------+
|    100 | SANJU   | HECKER     |  40000 | IT   |          3 |
|    101 | MANJU   | PROGRAMMER |  25000 | IT   |          2 |
|    102 | KUNJU   | MANAGER    |  60000 | HR   |          5 |
|    103 | ANJU    | INSTRUCTOR |  55000 | HR   |          3 |
|    104 | RENJU   | SUPERVISOR |  40000 | IT   |          3 |
+--------+---------+------------+--------+------+------------+
5 rows in set (0.00 sec)
```

### Question 6
```
mysql> UPDATE EMPLOYEE SET JOB="PROGRAMMER" WHERE DEPT="IT";
Query OK, 2 rows affected (0.04 sec)
Rows matched: 3  Changed: 2  Warnings: 0
```
```
mysql> SELECT * FROM EMPLOYEE;
+--------+---------+------------+--------+------+------------+
| EMPNUM | EMPNAME | JOB        | SALARY | DEPT | EXPERIENCE |
+--------+---------+------------+--------+------+------------+
|    100 | SANJU   | PROGRAMMER |  40000 | IT   |          3 |
|    101 | MANJU   | PROGRAMMER |  25000 | IT   |          2 |
|    102 | KUNJU   | MANAGER    |  60000 | HR   |          5 |
|    103 | ANJU    | INSTRUCTOR |  55000 | HR   |          3 |
|    104 | RENJU   | PROGRAMMER |  40000 | IT   |          3 |
+--------+---------+------------+--------+------+------------+
5 rows in set (0.00 sec)
```

### Question 7
```
mysql> DELETE FROM EMPLOYEE WHERE EMPNUM = 101;
Query OK, 1 row affected (0.04 sec)
```
```
mysql> SELECT * FROM EMPLOYEE;
+--------+---------+------------+--------+------+------------+
| EMPNUM | EMPNAME | JOB        | SALARY | DEPT | EXPERIENCE |
+--------+---------+------------+--------+------+------------+
|    100 | SANJU   | PROGRAMMER |  40000 | IT   |          3 |
|    102 | KUNJU   | MANAGER    |  60000 | HR   |          5 |
|    103 | ANJU    | INSTRUCTOR |  55000 | HR   |          3 |
|    104 | RENJU   | PROGRAMMER |  40000 | IT   |          3 |
+--------+---------+------------+--------+------+------------+
4 rows in set (0.00 sec)
```

### Question 8
```
mysql> SELECT EMPNAME,JOB,SALARY FROM EMPLOYEE;
+---------+------------+--------+
| EMPNAME | JOB        | SALARY |
+---------+------------+--------+
| SANJU   | PROGRAMMER |  40000 |
| KUNJU   | MANAGER    |  60000 |
| ANJU    | INSTRUCTOR |  55000 |
| RENJU   | PROGRAMMER |  40000 |
+---------+------------+--------+
4 rows in set (0.00 sec)
```

### Question 9
```
mysql> INSERT INTO EMPLOYEE VALUES
    -> (106,"CHINJU","SUPERVISOR",50000,"HR",4),
    -> (107,"RINJU","TESTER",100000,"DR",10);
Query OK, 2 rows affected (0.04 sec)
Records: 2  Duplicates: 0  Warnings: 0
```
```
mysql> SELECT * FROM EMPLOYEE;
+--------+---------+------------+--------+------+------------+
| EMPNUM | EMPNAME | JOB        | SALARY | DEPT | EXPERIENCE |
+--------+---------+------------+--------+------+------------+
|    100 | SANJU   | PROGRAMMER |  40000 | IT   |          3 |
|    102 | KUNJU   | MANAGER    |  60000 | HR   |          5 |
|    103 | ANJU    | INSTRUCTOR |  55000 | HR   |          3 |
|    104 | RENJU   | PROGRAMMER |  40000 | IT   |          3 |
|    106 | CHINJU  | SUPERVISOR |  50000 | HR   |          4 |
|    107 | RINJU   | TESTER     | 100000 | DR   |         10 |
+--------+---------+------------+--------+------+------------+
6 rows in set (0.00 sec)
```

### Question 10
```
mysql> SELECT EMPNAME,JOB,SALARY FROM EMPLOYEE;
+---------+------------+--------+
| EMPNAME | JOB        | SALARY |
+---------+------------+--------+
| SANJU   | PROGRAMMER |  40000 |
| KUNJU   | MANAGER    |  60000 |
| ANJU    | INSTRUCTOR |  55000 |
| RENJU   | PROGRAMMER |  40000 |
| CHINJU  | SUPERVISOR |  50000 |
| RINJU   | TESTER     | 100000 |
+---------+------------+--------+
6 rows in set (0.00 sec)
```

### Question 11
```
mysql> UPDATE EMPLOYEE SET SALARY=25000 WHERE JOB="TESTER";
Query OK, 1 row affected (0.04 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```
```
mysql> SELECT * FROM EMPLOYEE;
+--------+---------+------------+--------+------+------------+
| EMPNUM | EMPNAME | JOB        | SALARY | DEPT | EXPERIENCE |
+--------+---------+------------+--------+------+------------+
|    100 | SANJU   | PROGRAMMER |  40000 | IT   |          3 |
|    102 | KUNJU   | MANAGER    |  60000 | HR   |          5 |
|    103 | ANJU    | INSTRUCTOR |  55000 | HR   |          3 |
|    104 | RENJU   | PROGRAMMER |  40000 | IT   |          3 |
|    106 | CHINJU  | SUPERVISOR |  50000 | HR   |          4 |
|    107 | RINJU   | TESTER     |  25000 | DR   |         10 |
+--------+---------+------------+--------+------+------------+
6 rows in set (0.00 sec)
```

### Question 12
```
mysql> SELECT SALARY FROM EMPLOYEE ORDER BY SALARY;
+--------+
| SALARY |
+--------+
|  25000 |
|  40000 |
|  40000 |
|  50000 |
|  55000 |
|  60000 |
+--------+
6 rows in set (0.00 sec)
```

### Question 13
```
mysql> SELECT SALARY FROM EMPLOYEE ORDER BY SALARY DESC;
+--------+
| SALARY |
+--------+
|  60000 |
|  55000 |
|  50000 |
|  40000 |
|  40000 |
|  25000 |
+--------+
6 rows in set (0.00 sec)
```

### Question 14
```
mysql> SELECT * FROM EMPLOYEE WHERE SALARY>25000;
+--------+---------+------------+--------+------+------------+
| EMPNUM | EMPNAME | JOB        | SALARY | DEPT | EXPERIENCE |
+--------+---------+------------+--------+------+------------+
|    100 | SANJU   | PROGRAMMER |  40000 | IT   |          3 |
|    102 | KUNJU   | MANAGER    |  60000 | HR   |          5 |
|    103 | ANJU    | INSTRUCTOR |  55000 | HR   |          3 |
|    104 | RENJU   | PROGRAMMER |  40000 | IT   |          3 |
|    106 | CHINJU  | SUPERVISOR |  50000 | HR   |          4 |
+--------+---------+------------+--------+------+------------+
5 rows in set (0.00 sec)
```

### Question 15
```
mysql> SELECT DISTINCT DEPT FROM EMPLOYEE;
+------+
| DEPT |
+------+
| IT   |
| HR   |
| DR   |
+------+
3 rows in set (0.00 sec)
```

### Question 16
```
mysql> SELECT EMPNUM,EMPNAME FROM EMPLOYEE WHERE SALARY BETWEEN 30000 AND 45000;
+--------+---------+
| EMPNUM | EMPNAME |
+--------+---------+
|    100 | SANJU   |
|    104 | RENJU   |
+--------+---------+
2 rows in set (0.00 sec)
```

### Question 17
```
mysql> SELECT EMPNUM,EMPNAME FROM EMPLOYEE WHERE EMPNAME LIKE "S%";
+--------+---------+
| EMPNUM | EMPNAME |
+--------+---------+
|    100 | SANJU   |
+--------+---------+
1 row in set (0.00 sec)
```

### Question 18
```
mysql> SELECT EMPNUM,EMPNAME FROM EMPLOYEE WHERE DEPT = "IT" AND EMPNUM >103;
+--------+---------+
| EMPNUM | EMPNAME |
+--------+---------+
|    104 | RENJU   |
+--------+---------+
1 row in set (0.00 sec)
```

### Question 19
```
mysql> SELECT EMPNUM,EMPNAME FROM EMPLOYEE WHERE DEPT = "IT" OR EMPNUM >103;
+--------+---------+
| EMPNUM | EMPNAME |
+--------+---------+
|    100 | SANJU   |
|    104 | RENJU   |
|    106 | CHINJU  |
|    107 | RINJU   |
+--------+---------+
4 rows in set (0.00 sec)
```

### Question 20

*Before*
```
mysql> show tables;
+------------------+
| Tables_in_exp005 |
+------------------+
| employee         |
+------------------+
1 row in set (0.00 sec)
```

*Command Executed*
```
mysql> RENAME TABLE EMPLOYEE TO EMPLYOEE_2023;
Query OK, 0 rows affected (0.04 sec)
```

*After*
```
mysql> show tables;
+------------------+
| Tables_in_exp005 |
+------------------+
| emplyoee_2023    |
+------------------+
1 row in set (0.00 sec)
```

### Question 21
```
mysql> SELECT DISTINCT EMPNAME FROM EMPLYOEE_2023;
+---------+
| EMPNAME |
+---------+
| SANJU   |
| KUNJU   |
| ANJU    |
| RENJU   |
| CHINJU  |
| RINJU   |
+---------+
6 rows in set (0.00 sec)
```

## RESULT

Queries To implement SQL commands for DML has executed successfully and output obtained.
