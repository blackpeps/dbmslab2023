## 09. Implementation of Set Operations, nested and queries.

> For the time being download [this PDF](pdfs/exp9.pdf) from my repository to get started, This page will be updated as the lab session ends.


### **SET OPERATIONS**

```
mysql> create database tinu;
Query OK, 1 row affected (0.00 sec)
```
```
mysql> use tinu;
Database changed
```
```
mysql> create table employee(id int primary key,fname varchar(250),lname varchar(30),department varchar(40),salary int );
Query OK, 0 rows affected (0.28 sec)
```
```
mysql> desc employee;
+------------+--------------+------+-----+---------+-------+
| Field      | Type         | Null | Key | Default | Extra |
+------------+--------------+------+-----+---------+-------+
| id         | int(11)      | NO   | PRI | NULL    |       |
| fname      | varchar(250) | YES  |     | NULL    |       |
| lname      | varchar(30)  | YES  |     | NULL    |       |
| department | varchar(40)  | YES  |     | NULL    |       |
| salary     | int(11)      | YES  |     | NULL    |       |
+------------+--------------+------+-----+---------+-------+
5 rows in set (0.01 sec)
```
```
mysql> insert into employee values
    -> (1,'nm1','lm1','dept1',20000);
Query OK, 1 row affected (0.05 sec)
```
```
mysql> insert into employee values (2,'nm2','lm2','dept2',30000);
Query OK, 1 row affected (0.05 sec)
```
```
mysql> insert into employee values (3,'nm3','lm3','dept3',40000);
Query OK, 1 row affected (0.06 sec)
```
```
mysql> select * from employee;
+----+-------+-------+------------+--------+
| id | fname | lname | department | salary |
+----+-------+-------+------------+--------+
|  1 | nm1   | lm1   | dept1      |  20000 |
|  2 | nm2   | lm2   | dept2      |  30000 |
|  3 | nm3   | lm3   | dept3      |  40000 |
+----+-------+-------+------------+--------+
3 rows in set (0.00 sec)
```
```
mysql> create table employee2(id int primary key,first varchar(250),last varchar(30),depart varchar(40),salaryn int );
Query OK, 0 rows affected (0.36 sec)
```
```
mysql> insert into employee2 values (1,'nm1','lm1','dept1',20000);
Query OK, 1 row affected (0.05 sec)
```
```
mysql> insert into employee2 values (4,'nm4','lm4','dept4',50000);
Query OK, 1 row affected (0.04 sec)
```
```
mysql> insert into employee2 values (5,'nm5','lm5','dept5',60000);
Query OK, 1 row affected (0.04 sec)

```
```

mysql> select * from employee2;
+----+-------+------+--------+---------+
| id | first | last | depart | salaryn |
+----+-------+------+--------+---------+
|  1 | nm1   | lm1  | dept1  |   20000 |
|  4 | nm4   | lm4  | dept4  |   50000 |
|  5 | nm5   | lm5  | dept5  |   60000 |
+----+-------+------+--------+---------+
3 rows in set (0.00 sec)
```
```

mysql> select * from employee union all select * from employee2;
+----+-------+-------+------------+--------+
| id | fname | lname | department | salary |
+----+-------+-------+------------+--------+
|  1 | nm1   | lm1   | dept1      |  20000 |
|  2 | nm2   | lm2   | dept2      |  30000 |
|  3 | nm3   | lm3   | dept3      |  40000 |
|  1 | nm1   | lm1   | dept1      |  20000 |
|  4 | nm4   | lm4   | dept4      |  50000 |
|  5 | nm5   | lm5   | dept5      |  60000 |
+----+-------+-------+------------+--------+
6 rows in set (0.00 sec)
```
```

mysql> select * from employee union  select * from employee2;
+----+-------+-------+------------+--------+
| id | fname | lname | department | salary |
+----+-------+-------+------------+--------+
|  1 | nm1   | lm1   | dept1      |  20000 |
|  2 | nm2   | lm2   | dept2      |  30000 |
|  3 | nm3   | lm3   | dept3      |  40000 |
|  4 | nm4   | lm4   | dept4      |  50000 |
|  5 | nm5   | lm5   | dept5      |  60000 |
+----+-------+-------+------------+--------+
5 rows in set (0.00 sec)
```
```

mysql> alter table employee2 change first fname varchar(200);
Query OK, 3 rows affected (0.68 sec)
Records: 3  Duplicates: 0  Warnings: 0
```
```

mysql> alter table employee2 change last  lname varchar(200);
Query OK, 0 rows affected (0.07 sec)
Records: 0  Duplicates: 0  Warnings: 0
```
```

mysql> CREATE TABLE student (   id INT PRIMARY KEY AUTO_INCREMENT,   name VARCHAR(50) NOT NULL,   dob DATE NOT NULL,   age INT NOT NULL );
Query OK, 0 rows affected (0.63 sec)
```
```

mysql> INSERT INTO student (name, dob, age)
    -> VALUES
    ->   ('John Doe', '1998-05-15', 23),
    ->   ('Jane Smith', '2000-09-23', 21),
    ->   ('Michael Johnson', '1999-02-10', 22),
    ->   ('Emily Williams', '2001-07-07', 20),
    ->   ('David Brown', '1997-11-30', 24),
    ->   ('Sarah Davis', '1996-03-25', 25);
Query OK, 6 rows affected (0.16 sec)
Records: 6  Duplicates: 0  Warnings: 0
```
```

mysql> START TRANSACTION;
Query OK, 0 rows affected (0.00 sec)
```
```

mysql> SET autocommit =0;
Query OK, 0 rows affected (0.00 sec)
```
```

mysql> SAVEPOINT savepoint1;
Query OK, 0 rows affected (0.00 sec)
```
```

mysql> update student set age = 15 where id =2;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```
```

mysql> select * from student;
+----+-----------------+------------+-----+
| id | name            | dob        | age |
+----+-----------------+------------+-----+
|  1 | John Doe        | 1998-05-15 |  23 |
|  2 | Jane Smith      | 2000-09-23 |  15 |
|  3 | Michael Johnson | 1999-02-10 |  22 |
|  4 | Emily Williams  | 2001-07-07 |  20 |
|  5 | David Brown     | 1997-11-30 |  24 |
|  6 | Sarah Davis     | 1996-03-25 |  25 |
+----+-----------------+------------+-----+
6 rows in set (0.00 sec)
```
```

mysql> ROLLBACK to savepoint1;
Query OK, 0 rows affected (0.05 sec)
```
```

mysql> select * from student;
+----+-----------------+------------+-----+
| id | name            | dob        | age |
+----+-----------------+------------+-----+
|  1 | John Doe        | 1998-05-15 |  23 |
|  2 | Jane Smith      | 2000-09-23 |  21 |
|  3 | Michael Johnson | 1999-02-10 |  22 |
|  4 | Emily Williams  | 2001-07-07 |  20 |
|  5 | David Brown     | 1997-11-30 |  24 |
|  6 | Sarah Davis     | 1996-03-25 |  25 |
+----+-----------------+------------+-----+
6 rows in set (0.00 sec)
```
```

mysql> commit;
Query OK, 0 rows affected (0.00 sec)
```
```

mysql> desc student;
+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| id    | int         | NO   | PRI | NULL    | auto_increment |
| name  | varchar(50) | NO   |     | NULL    |                |
| dob   | date        | NO   |     | NULL    |                |
| age   | int         | NO   |     | NULL    |                |
+-------+-------------+------+-----+---------+----------------+
4 rows in set (0.00 sec)
```
```

mysql> insert into student(name,dob,age) values('james bond','2003-08-22',20);
Query OK, 1 row affected (0.00 sec)
```
```

mysql> select * from student;
+----+-----------------+------------+-----+
| id | name            | dob        | age |
+----+-----------------+------------+-----+
|  1 | John Doe        | 1998-05-15 |  23 |
|  2 | Jane Smith      | 2000-09-23 |  21 |
|  3 | Michael Johnson | 1999-02-10 |  22 |
|  4 | Emily Williams  | 2001-07-07 |  20 |
|  5 | David Brown     | 1997-11-30 |  24 |
|  6 | Sarah Davis     | 1996-03-25 |  25 |
|  7 | james bond      | 2003-08-22 |  20 |
+----+-----------------+------------+-----+
7 rows in set (0.00 sec)
```
```

mysql> savepoint savepoint2;
Query OK, 0 rows affected (0.00 sec)
```
```

mysql> rollback to savepoint2;
Query OK, 0 rows affected (0.00 sec)
```
```

mysql> select * from student;
+----+-----------------+------------+-----+
| id | name            | dob        | age |
+----+-----------------+------------+-----+
|  1 | John Doe        | 1998-05-15 |  23 |
|  2 | Jane Smith      | 2000-09-23 |  21 |
|  3 | Michael Johnson | 1999-02-10 |  22 |
|  4 | Emily Williams  | 2001-07-07 |  20 |
|  5 | David Brown     | 1997-11-30 |  24 |
|  6 | Sarah Davis     | 1996-03-25 |  25 |
|  7 | james bond      | 2003-08-22 |  20 |
+----+-----------------+------------+-----+
7 rows in set (0.00 sec)
```
```

mysql> commit;
Query OK, 0 rows affected (0.09 sec)
```









```
mysql> create table member(member_id int primary key,name varchar(25));
Query OK, 0 rows affected (0.56 sec)
```
```

mysql> insert into member values(01,'John'),
    -> (02,'Eline'),
    -> (03,'Micheal'),
    -> (04,'David');
Query OK, 4 rows affected (0.01 sec)
Records: 4  Duplicates: 0  Warnings: 0
```
```

mysql> CREATE TABLE cmember (
    ->     cid INT,
    ->     name VARCHAR(50)
    -> );
Query OK, 0 rows affected (0.72 sec)
```
```
mysql> insert into cmember values(01,'John'),
    -> (02,'Eline'),
    -> (03,'Fahad');
Query OK, 3 rows affected (0.00 sec)
Records: 3  Duplicates: 0  Warnings: 0
```
```

mysql> select member.name from member inner join cmember on member.name=cmember.name;
+-------+
| name  |
+-------+
| John  |
| Eline |
+-------+
2 rows in set (0.00 sec)
```
```

mysql> select * from member left join cmember on member.name=cmember.name;
+-----------+---------+------+-------+
| member_id | name    | cid  | name  |
+-----------+---------+------+-------+
|         1 | John    |    1 | John  |
|         2 | Eline   |    2 | Eline |
|         3 | Micheal | NULL | NULL  |
|         4 | David   | NULL | NULL  |
+-----------+---------+------+-------+
4 rows in set (0.00 sec)
```
```

mysql> select * from member right join cmember on member.name=cmember.name;
+-----------+-------+------+-------+
| member_id | name  | cid  | name  |
+-----------+-------+------+-------+
|         1 | John  |    1 | John  |
|         2 | Eline |    2 | Eline |
|      NULL | NULL  |    3 | Fahad |
+-----------+-------+------+-------+
3 rows in set (0.00 sec)
```
```

mysql> select * from member cross join cmember on member.name=cmember.name;
+-----------+-------+------+-------+
| member_id | name  | cid  | name  |
+-----------+-------+------+-------+
|         1 | John  |    1 | John  |
|         2 | Eline |    2 | Eline |
+-----------+-------+------+-------+
2 rows in set (0.00 sec)
```
```

oyee2 change depart  department varchar(200);
Query OK, 0 rows affected (0.08 sec)
Records: 0  Duplicates: 0  Warnings: 0
```
```

mysql> alter table employee2 change salaryn  salary int;
Query OK, 0 rows affected (0.09 sec)
Records: 0  Duplicates: 0  Warnings: 0
```
```

mysql> select * from employee2;
+----+-------+-------+------------+--------+
| id | fname | lname | department | salary |
+----+-------+-------+------------+--------+
|  1 | nm1   | lm1   | dept1      |  20000 |
|  4 | nm4   | lm4   | dept4      |  50000 |
|  5 | nm5   | lm5   | dept5      |  60000 |
+----+-------+-------+------------+--------+
3 rows in set (0.00 sec)
```
```

mysql> select * from employee union  select * from employee2 order by fname;
+----+-------+-------+------------+--------+
| id | fname | lname | department | salary |
+----+-------+-------+------------+--------+
|  1 | nm1   | lm1   | dept1      |  20000 |
|  2 | nm2   | lm2   | dept2      |  30000 |
|  3 | nm3   | lm3   | dept3      |  40000 |
|  4 | nm4   | lm4   | dept4      |  50000 |
|  5 | nm5   | lm5   | dept5      |  60000 |
+----+-------+-------+------------+--------+
5 rows in set (0.00 sec)
```
```

mysql> select fname from employee  where fname in(select fname from employee2);
+-------+
| fname |
+-------+
| nm1   |
+-------+
1 row in set (0.02 sec)
```
```

mysql> desc employee55;
+----------+--------------+------+-----+---------+-------+
| Field    | Type         | Null | Key | Default | Extra |
+----------+--------------+------+-----+---------+-------+
| empno    | int(11)      | NO   | PRI | NULL    |       |
| ename    | varchar(200) | YES  |     | NULL    |       |
| job      | varchar(20)  | YES  |     | NULL    |       |
| manager  | varchar(20)  | YES  |     | NULL    |       |
| salary   | int(11)      | YES  |     | NULL    |       |
| deptno   | int(11)      | YES  |     | NULL    |       |
| commn    | int(11)      | YES  |     | NULL    |       |
| hiredate | date         | YES  |     | NULL    |       |
+----------+--------------+------+-----+---------+-------+
8 rows in set (0.00 sec)
```
```

mysql> insert into employee55 values(01,'name1','job1','manager1',20000,1,50,'2002-01-11');
Query OK, 1 row affected (0.04 sec)
```
```

mysql> insert into employee55 values(02,'name2','job2','manager2',30000,2,60,'2000-03-12');
Query OK, 1 row affected (0.03 sec)
```
```

mysql> insert into employee55 values(03,'name3','job3','manager3',30500,1,65,'2005-04-14');
Query OK, 1 row affected (0.06 sec)
```
```

mysql> insert into employee55 values(04,'name4','job4','manager4',32500,2,75,'2001-12-23');
Query OK, 1 row affected (0.04 sec)
```
```

mysql> select * from employee55;
+-------+-------+------+----------+--------+--------+-------+------------+
| empno | ename | job  | manager  | salary | deptno | commn | hiredate   |
+-------+-------+------+----------+--------+--------+-------+------------+
|     1 | name1 | job1 | manager1 |  20000 |      1 |    50 | 2002-01-11 |
|     2 | name2 | job2 | manager2 |  30000 |      2 |    60 | 2000-03-12 |
|     3 | name3 | job3 | manager3 |  30500 |      1 |    65 | 2005-04-14 |
|     4 | name4 | job4 | manager4 |  32500 |      2 |    75 | 2001-12-23 |
+-------+-------+------+----------+--------+--------+-------+------------+

+-------+
2 rows in set (0.00 sec)
```
```

mysql> 
mysql> select ename,hiredate from employee55 where deptno=(select deptno from employee55 where ename="name1")and ename!="name1";
+-------+------------+
| ename | hiredate   |
+-------+------------+
| name3 | 2005-04-14 |
+-------+------------+
1 row in set (0.00 sec)
```
```


mysql> select empno,ename,salary from employee55 where salary>(select avg(salary) from employee55)order by empno;
+-------+-------+--------+
| empno | ename | salary |
+-------+-------+--------+
|     2 | name2 |  30000 |
|     3 | name3 |  30500 |
|     4 | name4 |  32500 |
+-------+-------+--------+
3 rows in set (0.02 sec)
```
```

mysql> select empno,ename from employee55 where deptno in(select deptno from employee55 where ename like '%2');
+-------+-------+



JOIN Operation


create table member(member_id int primary key,name varchar(25));
create table member(member_id int primary key,name varchar(25));
^C
mysql> create table member(member_id int primary key,name varchar(25));
Query OK, 0 rows affected (0.56 sec)

mysql> insert into member values(01,'John'),
    -> (02,'Eline'),
    -> (03,'Micheal'),
    -> (04,'David');
Query OK, 4 rows affected (0.01 sec)
Records: 4  Duplicates: 0  Warnings: 0

mysql> CREATE TABLE cmember (
    ->     cid INT,
    ->     name VARCHAR(50)
    -> );
Query OK, 0 rows affected (0.72 sec)

mysql> insert int cmember values(01,'John'),
    -> (02,'Eline'),
    -> (03,'Fahad');
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'int cmember values(01,'John'),
(02,'Eline'),
(03,'Fahad')' at line 1
mysql>  insert int cmember values(01,'John'),
    ->     -> (02,'Eline'),
    ->     -> (03,'Fahad');
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'int cmember values(01,'John'),
    -> (02,'Eline'),
    -> (03,'Fahad')' at line 1
mysql> insert into cmember values(01,'John'),     -> (02,'Eline'),     -> (03,'Fahad');
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '-> (02,'Eline'),     -> (03,'Fahad')' at line 1
mysql> insert into cmember values(01,'John'),
    -> (02,'Eline'),
    -> (03,'Fahad');
Query OK, 3 rows affected (0.00 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> select name from member inner join cmember on name=name;
ERROR 1052 (23000): Column 'name' in field list is ambiguous
mysql> select member.name from member inner join cmember on member.name=cmember.name;
+-------+
| name  |
+-------+
| John  |
| Eline |
+-------+
2 rows in set (0.00 sec)

mysql> select * from member left join cmember on member.name=cmember.name;
+-----------+---------+------+-------+
| member_id | name    | cid  | name  |
+-----------+---------+------+-------+
|         1 | John    |    1 | John  |
|         2 | Eline   |    2 | Eline |
|         3 | Micheal | NULL | NULL  |
|         4 | David   | NULL | NULL  |
+-----------+---------+------+-------+
4 rows in set (0.00 sec)

mysql> select * from member right join cmember on member.name=cmember.name;
+-----------+-------+------+-------+
| member_id | name  | cid  | name  |
+-----------+-------+------+-------+
|         1 | John  |    1 | John  |
|         2 | Eline |    2 | Eline |
|      NULL | NULL  |    3 | Fahad |
+-----------+-------+------+-------+
3 rows in set (0.00 sec)

mysql> select * from memb cross join cmember on member.name=cmember.name;
ERROR 1146 (42S02): Table 'nikhil.memb' doesn't exist
mysql> select * from member cross join cmember on member.name=cmember.name;
+-----------+-------+------+-------+
| member_id | name  | cid  | name  |
+-----------+-------+------+-------+
|         1 | John  |    1 | John  |
|         2 | Eline |    2 | Eline |
+-----------+-------+------+-------+
2 rows in set (0.00 sec)
| empno | ename |
+-------+-------+
|     2 | name2 |
|     4 | name4 |
+-------+-------+
2 rows in set (0.00 sec)
mysql> use tinu;
Database changed
mysql> create table employee(id int primary key,fname varchar(250),lname varchar(30),department varchar(40),salary int );
Query OK, 0 rows affected (0.28 sec)

mysql> desc employee
    -> desc employee;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'desc employee' at line 2
mysql> desc employee;
+------------+--------------+------+-----+---------+-------+
| Field      | Type         | Null | Key | Default | Extra |
+------------+--------------+------+-----+---------+-------+
| id         | int(11)      | NO   | PRI | NULL    |       |
| fname      | varchar(250) | YES  |     | NULL    |       |
| lname      | varchar(30)  | YES  |     | NULL    |       |
| department | varchar(40)  | YES  |     | NULL    |       |
| salary     | int(11)      | YES  |     | NULL    |       |
+------------+--------------+------+-----+---------+-------+
5 rows in set (0.01 sec)

mysql> insert into employee values
    -> (1,'nm1','lm1','dept1',20000),
    -> (2,'nm2','lm2','dept2',30000),
    -> (3,'nm3','lm3','dept3',40000));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ')' at line 4
mysql> insert into employee values
    -> (1,'nm1','lm1','dept1',20000);
Query OK, 1 row affected (0.05 sec)

mysql> insert into employee values (2,'nm2','lm2','dept2',30000);
Query OK, 1 row affected (0.05 sec)

mysql> insert into employee values (3,'nm3','lm3','dept3',40000);
Query OK, 1 row affected (0.06 sec)

mysql> select * from employee;
+----+-------+-------+------------+--------+
| id | fname | lname | department | salary |
+----+-------+-------+------------+--------+
|  1 | nm1   | lm1   | dept1      |  20000 |
|  2 | nm2   | lm2   | dept2      |  30000 |
|  3 | nm3   | lm3   | dept3      |  40000 |
+----+-------+-------+------------+--------+
3 rows in set (0.00 sec)

mysql> create table employee2(id int primary key,first varchar(250),last varchar(30),depart varchar(40),salaryn int );
Query OK, 0 rows affected (0.36 sec)

mysql> insert into employee2 values (1,'nm1','lm1','dept1',20000);
Query OK, 1 row affected (0.05 sec)

mysql> insert into employee2 values (4,'nm4','lm4','dept4',50000);
Query OK, 1 row affected (0.04 sec)

mysql> insert into employee2 values (5,'nm5','lm5','dept5',60000);
Query OK, 1 row affected (0.04 sec)

mysql> select * from employee2;
+----+-------+------+--------+---------+
| id | first | last | depart | salaryn |
+----+-------+------+--------+---------+
|  1 | nm1   | lm1  | dept1  |   20000 |
|  4 | nm4   | lm4  | dept4  |   50000 |
|  5 | nm5   | lm5  | dept5  |   60000 |
+----+-------+------+--------+---------+
3 rows in set (0.00 sec)

mysql> select * from employee union all select * from employee2;
+----+-------+-------+------------+--------+
| id | fname | lname | department | salary |
+----+-------+-------+------------+--------+
|  1 | nm1   | lm1   | dept1      |  20000 |
|  2 | nm2   | lm2   | dept2      |  30000 |
|  3 | nm3   | lm3   | dept3      |  40000 |
|  1 | nm1   | lm1   | dept1      |  20000 |
|  4 | nm4   | lm4   | dept4      |  50000 |
|  5 | nm5   | lm5   | dept5      |  60000 |
+----+-------+-------+------------+--------+
6 rows in set (0.00 sec)

mysql> select * from employee union  select * from employee2;
+----+-------+-------+------------+--------+
| id | fname | lname | department | salary |
+----+-------+-------+------------+--------+
|  1 | nm1   | lm1   | dept1      |  20000 |
|  2 | nm2   | lm2   | dept2      |  30000 |
|  3 | nm3   | lm3   | dept3      |  40000 |
|  4 | nm4   | lm4   | dept4      |  50000 |
|  5 | nm5   | lm5   | dept5      |  60000 |
+----+-------+-------+------------+--------+
5 rows in set (0.00 sec)



mysql> alter table employee2 change first fname varchar(200);
Query OK, 3 rows affected (0.68 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> alter table employee2 change last  lname varchar(200);
Query OK, 0 rows affected (0.07 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> alter table employee2 change depart  department varchar(200);
Query OK, 0 rows affected (0.08 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> alter table employee2 change salaryn  salary int;
Query OK, 0 rows affected (0.09 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> select * from employee2;
+----+-------+-------+------------+--------+
| id | fname | lname | department | salary |
+----+-------+-------+------------+--------+
|  1 | nm1   | lm1   | dept1      |  20000 |
|  4 | nm4   | lm4   | dept4      |  50000 |
|  5 | nm5   | lm5   | dept5      |  60000 |
+----+-------+-------+------------+--------+
3 rows in set (0.00 sec)

mysql> select * from employee union  select * from employee2 order by fname;
+----+-------+-------+------------+--------+
| id | fname | lname | department | salary |
+----+-------+-------+------------+--------+
|  1 | nm1   | lm1   | dept1      |  20000 |
|  2 | nm2   | lm2   | dept2      |  30000 |
|  3 | nm3   | lm3   | dept3      |  40000 |
|  4 | nm4   | lm4   | dept4      |  50000 |
|  5 | nm5   | lm5   | dept5      |  60000 |
+----+-------+-------+------------+--------+
5 rows in set (0.00 sec)

mysql> select fname from employee  where fname in(select fname from employee2);
+-------+
| fname |
+-------+
| nm1   |
+-------+
1 row in set (0.02 sec)

mysql> select fname from employee  where fname not in(select fname from employee2);
+-------+
| fname |
+-------+
| nm2   |
| nm3   |
+-------+
2 rows in set (0.00 sec)

mysql> create table employee55(empno int primary key,ename varchar(200),job varchar(20),manager varchar(20),salary int ,deptno int, commn int,hiredate date);
Query OK, 0 rows affected (0.26 sec)

mysql> desc employee55;
+----------+--------------+------+-----+---------+-------+
| Field    | Type         | Null | Key | Default | Extra |
+----------+--------------+------+-----+---------+-------+
| empno    | int(11)      | NO   | PRI | NULL    |       |
| ename    | varchar(200) | YES  |     | NULL    |       |
| job      | varchar(20)  | YES  |     | NULL    |       |
| manager  | varchar(20)  | YES  |     | NULL    |       |
| salary   | int(11)      | YES  |     | NULL    |       |
| deptno   | int(11)      | YES  |     | NULL    |       |
| commn    | int(11)      | YES  |     | NULL    |       |
| hiredate | date         | YES  |     | NULL    |       |
+----------+--------------+------+-----+---------+-------+
8 rows in set (0.00 sec)

mysql> insert into employee55 values(01,'name1','job1','manager1',20000,1,50,'2002-01-11');
Query OK, 1 row affected (0.04 sec)

mysql> insert into employee55 values(02,'name2','job2','manager2',30000,2,60,'2000-03-12');
Query OK, 1 row affected (0.03 sec)

mysql> insert into employee55 values(03,'name3','job3','manager3',30500,1,65,'2005-04-14');
Query OK, 1 row affected (0.06 sec)

mysql> insert into employee55 values(04,'name4','job4','manager4',32500,2,75,'2001-12-23');
Query OK, 1 row affected (0.04 sec)

mysql> select * from employee55;
+-------+-------+------+----------+--------+--------+-------+------------+
| empno | ename | job  | manager  | salary | deptno | commn | hiredate   |
+-------+-------+------+----------+--------+--------+-------+------------+
|     1 | name1 | job1 | manager1 |  20000 |      1 |    50 | 2002-01-11 |
|     2 | name2 | job2 | manager2 |  30000 |      2 |    60 | 2000-03-12 |
|     3 | name3 | job3 | manager3 |  30500 |      1 |    65 | 2005-04-14 |
|     4 | name4 | job4 | manager4 |  32500 |      2 |    75 | 2001-12-23 |
+-------+-------+------+----------+--------+--------+-------+------------+
4 rows in set (0.00 sec)
mysql> select ename,hiredate from employee55 where deptno=(select deptno from employee55 where ename="name1")and ename!="name1";
+-------+------------+
| ename | hiredate   |
+-------+------------+
| name3 | 2005-04-14 |
+-------+------------+
1 row in set (0.00 sec)


mysql> select empno,ename,salary from employee55 where salary>(select avg(salary) from employee55)order by empno;
+-------+-------+--------+
| empno | ename | salary |
+-------+-------+--------+
|     2 | name2 |  30000 |
|     3 | name3 |  30500 |
|     4 | name4 |  32500 |
+-------+-------+--------+
3 rows in set (0.02 sec)

mysql> select empno,ename from employee55 where deptno in(select deptno from employee55 where ename like '%2');
+-------+-------+
| empno | ename |
+-------+-------+
|     2 | name2 |
|     4 | name4 |
+-------+-------+
2 rows in set (0.00 sec)

