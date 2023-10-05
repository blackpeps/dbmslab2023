## 09. Implementation of Set Operations, nested and queries.

> For the time being download [this PDF](pdfs/exp9.pdf) from my repository to get started, This page will be updated as the lab session ends.





mysql> create database tinu;
Query OK, 1 row affected (0.00 sec)

mysql> use tinu;
Database changed
mysql> create table employee(id int primary key,fname varchar(250),lname varchar(30),department varchar(40),salary int );
Query OK, 0 rows affected (0.28 sec)


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
| nm3   |mysql> create table employee55(empno int primary key,ename varchar(200),job varhcar(20),manager varchar(20),salary int ,deptno int, commn int,hiredate date);
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'varhcar(20),manager varchar(20),salary int ,deptno int, commn int,hiredate date)' at line 1
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

+-------+
2 rows in set (0.00 sec)

mysql> 
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
