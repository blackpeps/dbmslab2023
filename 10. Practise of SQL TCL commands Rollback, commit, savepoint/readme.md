# 10. Practise of SQL TCL commands Rollback, commit, savepoint.

## AIM

To implement DCL commands for granting and revoking user privileges.

## Theory

### TRANSACTIONAL CONTROL LANGUAGE (T.C.L)

A transaction is a logical unit of work. All changes made to the database can be referred to as a transaction. Transaction changes can be made permanent to the database only if they are committed a transaction begins with an executable SQL statement & ends explicitly with either a rollback or commit statement.

#### COMMIT
This command is used to end a transaction only with the help of the commit command transaction changes can be made permanent to the database.

*Syntax:*

`COMMIT;`

#### SAVE POINT
Save points are like marks to divide a very lengthy transaction into smaller ones. They are used to identify a point in a transaction to which we can later roll back. Thus, save point is used in conjunction with role back.

*Syntax:*

`SAVEPOINT SAVEPOINT_ID;`

#### ROLLBACK
A role back command is used to undo the current transactions. We can roll back the entire transaction so that all changes made by SQL statements are undo (or) roll back a transaction to a save point so that the SQL statements after the save point are rolled back.

*Syntax:*

`ROLE BACK;` (current transaction that can be back)

`ROLE BACK to save_point_ID;`

## Questions

1. Create a student table
2. Write a query to start the transaction.
3. Write a query to set autocommit to 0.
4. Write a query to implement savepoints 1.
5. Update the student table and set age 29 where the id is 9.
6. Write a query to implement rollback to S1.
7. Write a query to implement a commit.
8. Insert a value into the table.
9. Write a query rollback.

## Output

#### Question 1
```
mysql> CREATE TABLE Student (
    ->     id INT PRIMARY KEY,
    ->     name VARCHAR(50),
    ->     age INT
    -> );
Query OK, 0 rows affected (0.02 sec)
```
#### Question 2
```
mysql> START TRANSACTION;
Query OK, 0 rows affected (0.03 sec)
```
#### Question 3
```
mysql> SET autocommit = 0;
Query OK, 0 rows affected (0.00 sec)
```
#### Question 4
```
mysql> SAVEPOINT S1;
Query OK, 0 rows affected (0.00 sec)
```
#### Question 5
```
mysql> UPDATE Student SET age = 29 WHERE id = 9;
Query OK, 0 rows affected (0.04 sec)
Rows matched: 0  Changed: 0  Warnings: 0
```
#### Question 6
```
mysql> ROLLBACK TO S1;
Query OK, 0 rows affected (0.00 sec)
```
#### Question 7
```
mysql> COMMIT;
Query OK, 0 rows affected (0.00 sec)
```
#### Question 8
```
mysql> INSERT INTO Student (id, name, age)
    -> VALUES (10, 'John', 25);
Query OK, 1 row affected (0.00 sec)
```
#### Question 9
```
mysql> ROLLBACK;
Query OK, 0 rows affected (0.00 sec)
```
```
mysql> select * from student;
Empty set (0.00 sec)
```
