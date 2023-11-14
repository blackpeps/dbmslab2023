# 16. Creation of Packages

## AIM

To create a package in PL/SQL

## Theory

Packages are schema objects that group logically related PL/SQL types, variables, and subprograms.

A package will have two mandatory parts –

- **Package Specification**
- **Package Body or Definition**

### 1. Package Specification

  - Interface to the package.
  - DECLARES types, variables, constants, exceptions, cursors, and subprograms.
  - Referenced from outside the package.
  - Contains information, excludes subprogram code.
  - Public objects are those in the specification.
  - Subprograms in the body without specification are private objects.

### 2. Package Body

  - Contains codes for methods in the package specification.
  - Includes private declarations hidden from outside code.
  - Created using the `CREATE PACKAGE BODY` statement.

## QUESTION

1. Create a package for the table customers

### ALGORITHM

**Package Specification**

Step 1: Start

Step 2: Create a package and create a method for finding the salary of an employee whose id is given by the user

Step 3: Stop

**Package Body**

Step 1: Start

Step 2: Declaration of package body for the created package

Step 3: Check whether the entered id is equal to the id from table customer21, then display the salary of the given employee

Step 4: Stop

**Using the package elements**

Step 1: Start

Step 2: Enter the employee id by the user

Step 3: Call the method for finding the salary using the package

Step 4: Stop

### PROGRAM

```sql
SQL> SET SERVEROUTPUT ON
```
```sql
SQL> CREATE OR REPLACE PACKAGE EmployePackage AS
  2      FUNCTION getSalaryById(p_employeeId IN NUMBER) RETURN NUMBER;
  3  END EmployePackage;
  4  /

Package created.
```
```sql
SQL> CREATE OR REPLACE PACKAGE BODY EmployePackage AS
  2      FUNCTION getSalaryById(p_employeeId IN NUMBER) RETURN NUMBER IS
  3          v_salary NUMBER;
  4      BEGIN
  5          -- Perform the logic to retrieve the salary based on the employee id
  6          SELECT salary INTO v_salary FROM customer WHERE ID = p_employeeId;
  7
  8          -- Return the salary
  9          RETURN v_salary;
 10      END getSalaryById;
 11  END EmployePackage;
 12  /

Package body created.
```
```sql
SQL> DECLARE
  2      v_employeeId NUMBER := 1; -- Provide the employee id here
  3      v_salary NUMBER;
  4  BEGIN
  5      v_salary := EmployePackage.getSalaryById(v_employeeId);
  6      DBMS_OUTPUT.PUT_LINE('Salary: ' || v_salary);
  7  END;
  8  /
Salary: 50000

PL/SQL procedure successfully completed.

```

---

## Practise Question

> No need to write in the fair record, just try it yourself.

2. Create a PL/SQL Package with addition and subtraction


```sql
 CREATE OR REPLACE PACKAGE MathOperations AS
  2      FUNCTION Addition(a IN NUMBER, b IN NUMBER) RETURN NUMBER;
  3      FUNCTION Subtraction(a IN NUMBER, b IN NUMBER) RETURN NUMBER;
  4  END MathOperations;
  5  /

Package created.
```
```sql
SQL> CREATE OR REPLACE PACKAGE BODY MathOperations AS
  2      FUNCTION Addition(a IN NUMBER, b IN NUMBER) RETURN NUMBER IS
  3          result NUMBER;
  4      BEGIN
  5          result := a + b;
  6          RETURN result;
  7      END Addition;
  8
  9      FUNCTION Subtraction(a IN NUMBER, b IN NUMBER) RETURN NUMBER IS
 10          result NUMBER;
 11      BEGIN
 12          result := a - b;
 13          RETURN result;
 14      END Subtraction;
 15  END MathOperations;
 16  /

Package body created.
```
```sql
SQL> DECLARE
  2      result_add NUMBER;
  3      result_sub NUMBER;
  4  BEGIN
  5      result_add := MathOperations.Addition(5, 3);
  6      result_sub := MathOperations.Subtraction(10, 4);
  7
  8      DBMS_OUTPUT.PUT_LINE('Addition: ' || result_add);
  9      DBMS_OUTPUT.PUT_LINE('Subtraction: ' || result_sub);
 10  END;
 11  /
Addition: 8
Subtraction: 6

PL/SQL procedure successfully completed.
```
```sql
SQL> DECLARE
  2      result_add NUMBER;
  3      result_sub NUMBER;
  4      A NUMBER(4):=&NUM1;
  5      B NUMBER(4):=&NUM2;
  6  BEGIN
  7      result_add := MathOperations.Addition(A,B);
  8      result_sub := MathOperations.Subtraction(A,B);
  9
 10      DBMS_OUTPUT.PUT_LINE('Addition: ' || result_add);
 11      DBMS_OUTPUT.PUT_LINE('Subtraction: ' || result_sub);
 12  END;
 13  /
Enter value for num1: 4
old   4:     A NUMBER(4):=&NUM1;
new   4:     A NUMBER(4):=4;
Enter value for num2: 5
old   5:     B NUMBER(4):=&NUM2;
new   5:     B NUMBER(4):=5;
Addition: 9
Subtraction: -1

PL/SQL procedure successfully completed.
```
