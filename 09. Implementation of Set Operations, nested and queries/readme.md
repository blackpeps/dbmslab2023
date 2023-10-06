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
