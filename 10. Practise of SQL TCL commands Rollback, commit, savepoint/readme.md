## 08. 10. Practise of SQL TCL commands Rollback, commit, savepoint.

> For the time being download [this PDF](pdfs/exp10.pdf) from my repository to get started, This page will be updated as the lab session ends.


mysql> CREATE TABLE student (
    ->   id INT PRIMARY KEY AUTO_INCREMENT,
    ->   name VARCHAR(50) NOT NULL,
    ->   dob DATE NOT NULL,
    ->   age INT NOT NULL,
    ->   grade VARCHAR(10) NOT NULL
    -> clear
    -> ;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'clear' at line 7
mysql> CREATE TABLE student (
    ->   id INT PRIMARY KEY AUTO_INCREMENT,
    ->   name VARCHAR(50) NOT NULL,
    ->   dob DATE NOT NULL,
    ->   age INT NOT NULL,
    -> );
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ')' at line 6
mysql> CREATE TABLE student (   id INT PRIMARY KEY AUTO_INCREMENT,   name VARCHAR(50) NOT NULL,   dob DATE NOT NULL,   age INT NOT NULL );
Query OK, 0 rows affected (0.63 sec)

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

mysql> START TRANSACTION;
Query OK, 0 rows affected (0.00 sec)

mysql> SET autocommit =0;
Query OK, 0 rows affected (0.00 sec)

mysql> SAVEPOINT savepoint1;
Query OK, 0 rows affected (0.00 sec)

mysql> update student set age = 15 where id =2;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

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

mysql> ROLLBACK to savepoint1;
Query OK, 0 rows affected (0.05 sec)

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

mysql> commit;
Query OK, 0 rows affected (0.00 sec)

mysql> insert into student values('james bond','2003-08-22',20);
ERROR 1136 (21S01): Column count doesn't match value count at row 1
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

mysql> insert into student(name,dob,age) values('james bond','2003-08-22',20);
Query OK, 1 row affected (0.00 sec)

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

mysql> savepoint savepoint2;
Query OK, 0 rows affected (0.00 sec)

mysql> rollback to savepoint2;
Query OK, 0 rows affected (0.00 sec)

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

mysql> rollback to savepoint1;
ERROR 1305 (42000): SAVEPOINT savepoint1 does not exist
mysql> commit;
Query OK, 0 rows affected (0.09 sec)

mysql> rollback to savepoint2;
ERROR 1305 (42000): SAVEPOINT savepoint2 does not exist













