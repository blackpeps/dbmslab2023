# 04. Creation, modification, configuration and deletion command.

## Notes

- All the writings in this file should be written on the right side of the fair record **unless specified not to write**.
- The PDF for the left side of the fair record will be updated soon. Till then, leave pages to paste, by estimating the space required using the output provided.
- **OUTPUT SHOULD NOT BE WRITTEN ON THE FAIR RECORD**, unless you are crazy and does have lot of time to waste.

---

## AIM

To create, modify, configure and delete the database using DDL commands

## Thoery

### Create Database

```sql
create database database_name;
```

### Create Table

```sql
create table table_name (
    column_name datatype(size) constraints,
    ...
);
```

### Modification

```sql
alter table table_name modify column_name datatype(size);
```

```sql
alter table table_name change old_column_name new_column_name datatype(size);
```

### Clear all values

```sql
Truncate table table_name;
```

or

```sql
delete from table_name;
```

### Delete both Schema and data

```sql
drop table table_name;
```

## QUESTIONS

1. Create a table STUDENT.
2. Add the column email ID to the table.
3. Show the structure of the table STUDENT.
4. Modify the table by changing the student name field size to 40.
5. Modify the table by adding field credit to the table.
6. Drop the table STUDENT.

## OUTPUT

```sql
mysql> create database exp004;
Query OK, 1 row affected (0.04 sec)

mysql> use exp004;
Database changed
```
### Question 1

```sql
mysql> CREATE TABLE student (ID INT(10),STUDNAME VARCHAR(20), DEPT VARCHAR(20));
Query OK, 0 rows affected, 1 warning (0.04 sec)
```

```
mysql> desc student;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| ID       | int         | YES  |     | NULL    |       |
| STUDNAME | varchar(20) | YES  |     | NULL    |       |
| DEPT     | varchar(20) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

### Question 2

```sql
mysql> ALTER TABLE student ADD EMAIL_ID VARCHAR(20);
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

```
mysql> desc student;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| ID       | int         | YES  |     | NULL    |       |
| STUDNAME | varchar(20) | YES  |     | NULL    |       |
| DEPT     | varchar(20) | YES  |     | NULL    |       |
| EMAIL_ID | varchar(20) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)
```

### Question 3

```sql
mysql> desc student;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| ID       | int         | YES  |     | NULL    |       |
| STUDNAME | varchar(20) | YES  |     | NULL    |       |
| DEPT     | varchar(20) | YES  |     | NULL    |       |
| EMAIL_ID | varchar(20) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)
```

### Question 4

```sql
mysql> ALTER TABLE student MODIFY STUDNAME VARCHAR(40);
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

```
mysql> desc student;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| ID       | int         | YES  |     | NULL    |       |
| STUDNAME | varchar(40) | YES  |     | NULL    |       |
| DEPT     | varchar(20) | YES  |     | NULL    |       |
| EMAIL_ID | varchar(20) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)
```

### Question 5

```sql
mysql> ALTER TABLE student ADD CREDIT INT(10);
Query OK, 0 rows affected, 1 warning (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 1
```

```
mysql> desc student;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| ID       | int         | YES  |     | NULL    |       |
| STUDNAME | varchar(40) | YES  |     | NULL    |       |
| DEPT     | varchar(20) | YES  |     | NULL    |       |
| EMAIL_ID | varchar(20) | YES  |     | NULL    |       |
| CREDIT   | int         | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)
```

### Question 6

*Before*
```sql
mysql> show tables;
+------------------+
| Tables_in_exp004 |
+------------------+
| student          |
+------------------+
1 row in set (0.00 sec)
```

*Command executed*
```sql
mysql> drop table student;
Query OK, 0 rows affected (0.04 sec)
```

*After*
```sql
mysql> desc student;
ERROR 1146 (42S02): Table 'exp004.student' doesn't exist
```

```sql
mysql> show tables;
Empty set (0.00 sec)
```

## RESULT
Query to create, modify, configure and delete database using DDL commands has executed successfully and the output obtained
