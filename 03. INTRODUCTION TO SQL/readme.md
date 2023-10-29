# Introduction to SQL

## Table of Contents

| Sl. No. | Topic                                      | Navigation                             |
| ------- | ------------------------------------------ | -------------------------------------- |
| 1       | INTRODUCTION TO SQL                        | [click here](#introduction-to-sql)      |
| 1.1     | History of SQL                             | [click here](#history-of-sql)           |
| 1.2     | Rules                                      | [click here](#rules)                    |
| 1.3     | SQL Process                                | [click here](#sql-process)               |
| 1.4     | SQL Commands                               | [click here](#sql-commands)              |
| 1.4.1   | Data Definition Language (DDL)             | [click here](#data-definition-language-ddl) |
| 1.4.1.1 | CREATE                                    | [click here](#create)                   |
| 1.4.1.2 | DROP                                      | [click here](#drop)                     |
| 1.4.1.3 | ALTER                                     | [click here](#alter)                    |
| 1.4.1.4 | TRUNCATE                                  | [click here](#truncate)                 |
| 1.4.2   | Data Manipulation Language (DML)          | [click here](#data-manipulation-language-dml) |
| 1.4.2.1 | INSERT                                   | [click here](#insert)                   |
| 1.4.2.2 | UPDATE                                   | [click here](#update)                   |
| 1.4.2.3 | DELETE                                   | [click here](#delete)                   |
| 1.4.3   | Data Control Language (DCL)               | [click here](#data-control-language-dcl) |
| 1.4.3.1 | Grant                                    | [click here](#grant)                   |
| 1.4.3.2 | Revoke                                   | [click here](#revoke)                  |
| 1.4.4   | Transaction Control Language (TCL)        | [click here](#transaction-control-language-tcl) |
| 1.4.4.1 | Commit                                  | [click here](#commit)                   |
| 1.4.4.2 | Rollback                                | [click here](#rollback)                 |
| 1.4.4.3 | SAVEPOINT                               | [click here](#savepoint)                |
| 1.4.5   | Data Query Language                        | [click here](#data-query-language)      |
| 2       | Introduction to MySQL                     | [click here](#introduction-to-mysql)   |
| 2.1     | History of MySQL                          | [click here](#history-of-mysql)        |
| 2.2     | MySQL Data Types                          | [click here](#mysql-data-types)        |
| 2.2.1   | Numeric Data Type                         | [click here](#numeric-data-type)       |
| 2.2.2   | Date and Time Data Type                   | [click here](#date-and-time-data-type) |
| 2.2.3   | String Data Types                        | [click here](#string-data-types)       |


---

SQL, or Structured Query Language, is a standard language for managing databases. It's used to create, modify, and delete database objects, as well as store, retrieve, and update data in various database systems like SQL Server, Oracle, and MySQL.

## 1. History of SQL

Dr. E. F. Codd's 1970 ACM paper introduced the relational model, now the foundation for RDBMS. IBM developed Structured English Query Language (SEQUEL), later known as SQL. In 1979, Oracle (formerly Relational Software, Inc.) released the first commercial SQL. Today, SQL is the standard RDBMS language.

## 2. Rules

SQL follows the following rules:

1. Not case-sensitive, keywords often in uppercase.
2. Statements can span multiple lines.
3. Enables diverse database actions.
4. Based on tuple relational calculus and relational algebra.

## 3. SQL Process

- SQL command execution involves system optimization.
- Components like optimization engine, query engine, and more are involved.
- Classic query engine handles non-SQL queries; SQL engine excludes logical files.

## 4. SQL Commands

SQL commands are instructions used to communicate with the database and perform specific tasks, functions, and data queries.

### 4.1. Data Definition Language (DDL)

DDL: Alters table structure (create, delete, modify). Auto-commits, permanently affecting the database.

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

DML modifies the database but doesn't auto-commit, allowing for rollback.

#### 4.2.a. INSERT

The `INSERT` statement is used to insert data into a table.

Syntax:

*To insert values into the specified column.*

```sql
INSERT INTO TABLE_NAME (col1, col2, col3,.... colN) VALUES (value1, value2, value3, ... . valueN);
```

Example:
```sql
INSERT INTO testtable (Author, Subject) VALUES ("Sonoo", "DBMS");
```

*To insert values into all columns that exist during table creation*

```sql
INSERT INTO TABLE_NAME VALUES (value1, valeu2, ... , valueN);
```

Example:
```sql
INSERT INTO testtable VALUES ("Sonoo", "DBMS", 54, 9876543210);
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

TCL works only with DML (INSERT, DELETE, UPDATE), and auto-commits changes, not for table creation or deletion.

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

Not applicable to DCL commands.

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

MySQL is a popular open-source relational database management system (RDBMS) based on SQL, GNU-licensed, and supported by Oracle.

## 1. History of MySQL

MySQL began in 1979 as UNIREG, an in-house database tool by Michael Widenius. It evolved, and Widenius collaborated with the author of mSQL David Hughes to create MySQL.

MySQL is becoming popular because:

1. Free and open-source.
2. Handles extensive functionality.
3. Customizable due to GPL license.
4. Speed with large datasets.
5. Supports multiple systems and languages.
6. Standard SQL language.
7. Ideal for PHP web development.
8. Handles large databases, up to millions of rows.

## 2. MySQL Data Types

MySQL supports numeric, date/time, and string data types for defining table columns.

### 2.1. Numeric Data Type

MySQL supports essential SQL numeric data types (exact and approximate), including `BIT` for bit values, and they can be signed or unsigned.

| Data Type | Description                       |
|-----------|-----------------------------------|
| TINYINT   | Small integer, 1 byte storage    |
| SMALLINT  | Small integer, 2 bytes storage   |
| MEDIUMINT | Medium-sized integer, 3 bytes storage |
| INT       | Normal-sized integer, 4 bytes storage |
| BIGINT    | Large integer, 8 bytes storage   |
| FLOAT(m,d) | Floating-point number (can't be unsigned), 4 bytes storage. Can define display length (m) and number of decimals(d) |
| DOUBLE(m,d) | Double-precision floating-point number (can't be unsigned), 8 bytes storage |
| DECIMAL(m,d) | Unpacked floating-point number (can't be unsigned). The synonym is Numeric. |
| BIT(m)    | Used for storing bit values. M determines the number of bits per value      |
| BOOL      | Used for true and false conditions (1 for true, 0 for false) |
| BOOLEAN   | Similar to BOOL                  |

### 2.2. Date and Time Data Type

MySQL supports date and time data types to represent temporal values.

> While writing fair records, you can skip the Maximum Size Column altogether.

| Data Type | Maximum Size            | Explanation                                |
|-----------|-------------------------|--------------------------------------------|
| YEAR[(2|4)] | 2 or 4 digits        | Year value as 2 or 4 digits                 |
| DATE      | '1000-01-01' to '9999-12-31' | Date values in 'yyyy-mm-dd' format   |
| TIME      | '-838:59:59' to '838:59:59' | Time values in 'HH:MM:SS' format    |
| DATETIME  | '1000-01-01 00:00:00' to '9999-12-31 23:59:59' | Datetime values in 'yyyy-mm-dd hh:mm:ss' format |
| TIMESTAMP(m) | '1970-01-01 00:00:01' to '2038-01-19 03:14:07' | Timestamp values in 'YYYY-MM-DD HH:MM:SS' format |

### 2.3. String Data Types

MySQL string data types are used to hold plain text and binary data.

> While writing fair records, you can skip the Maximum Size Column altogether.

| Data Type | Maximum Size    | Explanation                   |
|-----------|-----------------|-------------------------------|
| CHAR(size)   | Up to 255 characters | Fixed-length strings, space-padded on the right to equal-size characters |
| VARCHAR(size) | Up to 255 characters | Variable-length strings |
| TINYTEXT(size) | Up to 255 characters | Maximum size of 255 characters |
| TEXT(size)    | Up to 65,535 characters | Maximum size of 65,535 characters |
| MEDIUMTEXT(size) | Up to 16,777,215 characters | Maximum size of 16,777,215 characters |
| LONGTEXT(size) | Up to 4GB or 4,294,967,295 characters | Maximum size of 4GB or 4,294,967,295 characters |
| BINARY(size)   | Up to 255 characters | Fixed-length strings, space-padded on the right to equal-size characters |
| VARBINARY(size) | Up to 255 characters | Variable-length strings |
| ENUM | Up to 65,535 values | Enumeration type, stores one of the specified values |
| SET  | Up to 64 members | Stores zero or more string values from a predefined list |
