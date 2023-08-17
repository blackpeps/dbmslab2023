# DBMS Lab 2023

### [Lab Experiments](#goback)

| Experiment                                                                                                      | Date          |
| --------------------------------------------------------------------------------------------------------------- | ------------- |
| 1. [ Introduction to ER diagram and SQL](#prgm01)                                                               | Not yet done. |
| 2. [ Creation, modification, configuration and deletion command. ](#prgm02)                                     | 17-08-2023    |
| 3. [ Exprot ER diagram from database and verify relationships. ](#prgm03)                                       | Not yet done. |
| 4. [ Database Initialisation, Data Insert, Import to database. ](#prgm04)                                       | Not yet done. |
| 5. [ Practise SQL commands for DML. ](#prgm05)                                                                  | 17-08-2023    |
| 6. [ Implementation of built in functions. ](#prgm06)                                                           | Not yet done. |
| 7. [ Implementation of aggregate functions. ](#prgm07)                                                          | Not yet done. |
| 8. [ Implementation of orderby, group by, and having. ](#prgm08)                                                | Not yet done. |
| 9. [ Implementation of Set Operations, nested and queries. ](#prgm09)                                           | Not yet done. |
| 10. [ Practise of SQL TCL commands Rollback, commit, savepoint. ](#prgm10)                                      | Not yet done. |
| 11. [ Implementation of DCL commands for granting and revoking user privileges. ](#prgm11)                      | Not yet done. |
| 12. [ Practise of SQL Commands for creation or view assertion. ](#prgm12)                                       | Not yet done. |
| 13. [ Implementation of various control structures like, if then, then else, if then else, if while. ](#prgm13) | Not yet done. |
| 14. [ Creation of procedure,triggers, functions. ](#prgm14)                                                     | Not yet done. |
| 15. [ Creation of cursor. ](#prgm15)                                                                            | Not yet done. |
| 16. [ Creation of Packages. ](#prgm16)                                                                          | Not yet done. |
| 17. [ Creation of PL/SQL block for exception handling. ](#prgm17)                                               | Not yet done. |
| 18. [ Student database Management System. ](#prgm18)                                                            | Not yet done. |

## Some Basics before you start SQL

```
mysql -u root -p
```

This commad helps you start using MySQL.

<a name="prgm01"></a>

## 01. Introduction to ER diagram and SQL

a. [ Introduction to ER Model University Management System. ](#prgm01a)

b. [ Introduction to ER Diagram. ](#prgm01b)

c. [ Introduction to SQL. ](#prgm01c)

<a name="prgm02"></a>

## 02. Creation, modification, configuration and deletion command.

### Create Database

```
create database database_name;
```

#### Example

```
create database sreeram;
```

### Create Table

```
create table table_name (
    column_name datatype(size) constraints,
    ...
);
```

#### Example

```
create table student (
    rollno int primarykey,
    name varchar(255),
    age int
);
```

### Modification

```
alter table table_name modify column_name datatype(size);
```

_Note:_ **_For Systems running different versions of mySQL, please use the following syntax to get throught the error:_**

```
alter table table_name change old_column_name new_column_name datatype(size);
```

### Clear all values

```
Truncate table table_name;
```

or

```
delete from table_name;
```

### Delete both Schema and dates

```
drop table table_name;
```

<a name="prgm05"></a>

## 05. Practise SQL commands for DML.

show databases;
create database sreeram;
create table student (rollno int primarykey, name varchar(255), age int);
insert into student values (1, 'Kevin', 20);
insert into student values (2, 'Nikhil', 20), (3, 'Tinu', 20), (3, 'Sreeram', 20), (4, 'Merlin', 20);
alter table student add ph_no int;
alter table student change ph_no phno int;
select \* from student;
alter table student add dob date;
select rollno, name from student where rollno>2;
update student set dob=2002-12-13 where rollno=4;
update student set phno=5678;
desc student;
alter table student add time time;
alter table student add date_and_time timestamp;
update student set date_and_time='2023-10-11 04:55:23' where rollno=5;
update student set time='05:30:13' where rollno=4;
delete from student where rollno=4;
delete from student;
