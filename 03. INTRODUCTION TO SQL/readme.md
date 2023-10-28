# Introduction to SQL

---

## Under Maintenance 

---

SQL stands for Structured Query Language. SQL is used to create, remove, and alter the database and database objects in a database management system and to store, retrieve, and update the data in a database. SQL is a standard language for creating, accessing, and manipulating database management systems. SQL works for all modern relational database management systems, like SQL Server, Oracle, MySQL, etc.

## 1. History of SQL

Dr. E. F. Codd published the paper, "A Relational Model of Data for Large Shared Data Banks", in June 1970 in the Association of Computer Machinery (ACM) journal, Communications of the ACM. Codd's model is now accepted as the definitive model for relational database management systems (RDBMS). The language, Structured English Query Language (SEQUEL), was developed by IBM Corporation, Inc., to use Codd's model. SEQUEL later became SQL (still pronounced "sequel"). In 1979, Relational Software, Inc. (now Oracle) introduced the first commercially available implementation of SQL. Today, SQL is accepted as the standard RDBMS language.

## 2. Rules

SQL follows the following rules:

- Structure query language is not case-sensitive. Generally, keywords of SQL are written in uppercase.
- Statements of SQL are dependent on text lines. We can use a single SQL statement on one or multiple text lines.
- Using the SQL statements, you can perform most of the actions in a database.
- SQL depends on tuple relational calculus and relational algebra.

## 3. SQL Process

- When an SQL command is executing for any RDBMS, the system figures out the best way to carry out the request, and the SQL engine determines how to interpret the task.
- In the process, various components are included. These components can be the optimization engine, query engine, query dispatcher, classic, etc.
- All the non-SQL queries are handled by the classic query engine, but the SQL query engine won't handle logical files.

## 4. SQL Commands

SQL commands are instructions used to communicate with the database and perform specific tasks, functions, and data queries.

### 4.1. Data Definition Language (DDL)

DDL changes the structure of the table, including creating, deleting, and altering tables. All the commands of DDL are auto-committed, meaning they permanently save all the changes in the database.

#### 4.1.a. CREATE

The `CREATE` command is used to create a new table in the database.

Syntax:
```sql
CREATE TABLE TABLE_NAME (COLUMN_NAME DATATYPE[,....]);
```

Example:
```sql
CREATE TABLE EMPLOYEE(Name VARCHAR2(20), Email VARCHAR2(100), DOB DATE);
```

#### 4.1.b. DROP

The `DROP` command is used to delete both the structure and records stored in the table.

Syntax:
```sql
DROP TABLE TABLE_NAME;
```

Example:
```sql
DROP TABLE EMPLOYEE;
```

#### 4.1.c. ALTER

The `ALTER` command is used to alter the structure of the database, either to modify the characteristics of an existing attribute or to add a new attribute.

Syntax (To add a new column in the table):
```sql
ALTER TABLE TABLE_NAME ADD COLUMN_NAME COLUMN_DEFINITION;
```

Syntax (To modify an existing column in the table):
```sql
ALTER TABLE TABLE_NAME MODIFY (COLUMN_DEFINITIONS....);
```

Examples:
```sql
ALTER TABLE STU_DETAILS ADD(ADDRESS VARCHAR2(20));
ALTER TABLE STU_DETAILS MODIFY (NAME VARCHAR2(20));
```

#### 4.1.d. TRUNCATE

The `TRUNCATE` command is used to delete all the rows from the table and free the space containing the table.

Syntax:
```sql
TRUNCATE TABLE TABLE_NAME;
```

Example:
```sql
TRUNCATE TABLE EMPLOYEE;
```

### 4.2. Data Manipulation Language (DML)

DML commands are used to modify the database and are responsible for all forms of changes in the database. The command of DML is not auto-committed, meaning it can't permanently save all the changes in the database and can be rolled back.

#### 4.2.a. INSERT

The `INSERT` statement is used to insert data into a table.

Syntax:
```sql
INSERT INTO TABLE_NAME (col1, col2, col3,.... colN) VALUES (value1, value2, value3, ... . valueN);
```

Example:
```sql
INSERT INTO testtable (Author, Subject) VALUES ("Sonoo", "DBMS");
```

#### 4.2.b. UPDATE

The `UPDATE` command is used to update or modify the value of a column in the table.

Syntax:
```sql
UPDATE TABLE_NAME SET [column_name1 = value1, ...column_nameN = valueN] [WHERE CONDITION];
```

Example:
```sql
UPDATE students SET User_Name = 'Sonoo' WHERE Student_Id = '3';
```

#### 4.2.c. DELETE

The `DELETE` command is used to remove one or more rows from a table.

Syntax:
```sql
DELETE FROM TABLE_NAME [WHERE condition];
```

Example:
```sql
DELETE FROM testtable WHERE Author="Sonoo";
```

### 4.3. Data Control Language (DCL)

DCL commands are used to grant and take back authority from any database user.

#### 4.3.a. Grant

The `GRANT` command is used to give user access privileges to a database.

Example:
```sql
GRANT SELECT, UPDATE ON MY_TABLE TO SOME_USER, ANOTHER_USER;
```

#### 4.3.b. Revoke

The `REVOKE` command is used to take back permissions from the user.

Example:
```sql
REVOKE SELECT, UPDATE ON MY_TABLE FROM USER1, USER2;
```

### 4.4. Transaction Control Language (TCL)

TCL commands can only be used with DML commands like INSERT, DELETE, and UPDATE. These operations are automatically committed to the database, which is why they cannot be used while creating or dropping tables.

#### 4.4.a. Commit

The `COMMIT` command is used to save all the transactions to the database.

Syntax:
```sql
COMMIT;
```

Example:
```sql
DELETE FROM CUSTOMERS WHERE AGE = 25;
COMMIT;
```

#### 4.4.b. Rollback

The `ROLLBACK` command is used to undo transactions that have not already been saved to the database.

Syntax:
```sql
ROLLBACK;
```

Example:
```sql
DELETE FROM CUSTOMERS WHERE AGE = 25;
ROLLBACK;
```

#### 4.4.c. SAVEPOINT

Not applicable for DCL commands.

### 4.5. Data Query Language

DQL is used to fetch data from the database and uses only one command: `SELECT`.

#### 4.5.a. SELECT

The `SELECT` command is used to select attributes based on the conditions described by the `WHERE` clause.

Syntax:
```sql
SELECT expressions FROM TABLES WHERE conditions;
```

Example:
```sql
SELECT emp_name FROM employee WHERE age > 20;
```

---

# Introduction to MySQL

MySQL is a very popular open-source relational database management system (RDBMS). MySQL is a relational database

 management system based on the Structured Query Language, which is the popular language for accessing and managing records in the database. MySQL is open-source and free software under the GNU license and is supported by Oracle Company.

## 1. History of MySQL

The project of MySQL was started in 1979 when MySQL's inventor Michael Widenius developed an in-house database tool called UNIREG for managing databases. After that, UNIREG has been rewritten in several different languages and extended to handle big databases. After some time, Michael Widenius contacted David Hughes, the author of mSQL, to see if Hughes would be interested in connecting mSQL to UNIREG's B+ ISAM handler to provide indexing to mSQL. That's the way MySQL came into existence.

MySQL is becoming popular because:

- MySQL is an open-source database, so you don't have to pay a single penny to use it.
- MySQL is a powerful program that can handle a large set of functionality of the most expensive and powerful database packages.
- MySQL is customizable because it is an open-source database, and the open-source GPL license facilitates programmers to modify the SQL software according to their own specific environment.
- MySQL is quicker than other databases and can work well even with large datasets.
- MySQL supports many operating systems and languages.
- MySQL uses a standard form of the well-known SQL data language.
- MySQL is very friendly with PHP, the most popular language for web development.
- MySQL supports large databases, up to 50 million rows or more in a table. The default file size limit for a table is 4GB, but you can increase this to a theoretical limit of 8 million terabytes (TB).

## 2. MySQL Data Types

MySQL supports various data types, including numeric, date and time, and string types. These data types are used for defining the columns in database tables.

### 2.1. Numeric Data Type

MySQL has essential SQL numeric data types, both exact (e.g., integer, decimal) and approximate (e.g., float, double). It also supports the `BIT` data type to store bit values. Numeric data types can be signed or unsigned.

| Data Type | Description                       |
|-----------|-----------------------------------|
| TINYINT   | Small integer, 1 byte storage    |
| SMALLINT  | Small integer, 2 bytes storage   |
| MEDIUMINT | Medium-sized integer, 3 bytes storage |
| INT       | Normal-sized integer, 4 bytes storage |
| BIGINT    | Large integer, 8 bytes storage   |
| FLOAT(m,d) | Floating-point number, 4 bytes storage |
| DOUBLE(m,d) | Double-precision floating-point number, 8 bytes storage |
| DECIMAL(m,d) | Unpacked floating-point number |
| BIT(m)    | Used for storing bit values      |
| BOOL      | Used for true and false conditions (1 for true, 0 for false) |
| BOOLEAN   | Similar to BOOL                  |

### 2.2. Date and Time Data Type

MySQL supports date and time data types to represent temporal values.

| Data Type | Maximum Size            | Explanation                                |
|-----------|-------------------------|--------------------------------------------|
| YEAR[(2,4)] | 2 or 4 digits        | Year value as 2 or 4 digits                 |
| DATE      | '1000-01-01' to '9999-12-31' | Date values in 'yyyy-mm-dd' format   |
| TIME      | '-838:59:59' to '838:59:59' | Time values in 'HH:MM:SS' format    |
| DATETIME  | '1000-01-01 00:00:00' to '9999-12-31 23:59:59' | Datetime values in 'yyyy-mm-dd hh:mm:ss' format |
| TIMESTAMP(m) | '1970-01-01 00:00:01' to '2038-01-19 03:14:07' | Timestamp values in 'YYYY-MM-DD HH:MM:SS' format |

### 2.3. String Data Types

MySQL string data types are used to hold plain text and binary data. These data types include `CHAR`, `VARCHAR`, `TINYTEXT`, `TEXT`, `MEDIUMTEXT`, `LONGTEXT`, `BINARY`, `VARBINARY`, `ENUM`, and `SET`.

| Data Type | Maximum Size    | Explanation                   |
|-----------|-----------------|-------------------------------|
| CHAR(size)   | Up to 255 characters | Fixed-length strings, space-padded on the right to equal size characters |
| VARCHAR(size) | Up to 255 characters | Variable-length strings |
| TINYTEXT(size) | Up to 255 characters | Maximum size of 255 characters |
| TEXT(size)    | Up to 65,535 characters | Maximum size of 65,535 characters |
| MEDIUMTEXT(size) | Up to 16,777,215 characters | Maximum size of 16,777,215 characters |
| LONGTEXT(size) | Up to 4GB or 4,294,967,295 characters | Maximum size of 4GB or 4,294,967,295 characters |
| BINARY(size)   | Up to 255 characters | Fixed-length strings, space-padded on the right to equal size characters |
| VARBINARY(size) | Up to 255 characters | Variable-length strings |
| ENUM | Up to 65,535 values | Enumeration type, stores one of the specified values |
| SET  | Up to 64 members | Stores zero or more string values from a predefined list |

This structured information can be used in a markdown file for GitHub with a table of contents for quick navigation.


# Table of Contents

- [INTRODUCTION TO SQL](#introduction-to-sql)
  1. [History of SQL](#history-of-sql)
  2. [Rules](#rules)
  3. [SQL Process](#sql-process)
  4. [SQL Commands](#sql-commands)
    1. [Data Definition Language (DDL)](#data-definition-language-ddl)
      - [CREATE](#create)
      - [DROP](#drop)
      - [ALTER](#alter)
      - [TRUNCATE](#truncate)
    2. [Data Manipulation Language (DML)](#data-manipulation-language-dml)
      - [INSERT](#insert)
      - [UPDATE](#update)
      - [DELETE](#delete)
    3. [Data Control Language (DCL)](#data-control-language-dcl)
      - [Grant](#grant)
      - [Revoke](#revoke)
    4. [Transaction Control Language (TCL)](#transaction-control-language-tcl)
      - [Commit](#commit)
      - [Rollback](#rollback)
      - [SAVEPOINT](#savepoint)
    5. [Data Query Language](#data-query-language)
      - [SELECT](#select)

- [Introduction to MySQL](#introduction-to-mysql)
  1. [History of MySQL](#history-of-mysql)
  2. [MySQL Data Types](#mysql-data-types)
    1. [Numeric Data Type](#numeric-data-type)
    2. [Date and Time Data Type](#date-and-time-data-type)
    3. [String Data Types](#string-data-types)

---
