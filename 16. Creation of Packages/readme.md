## 16. Creation of Packages

---

# UNDER MAINTENANCE

---


## To create a package in PL/SQL

Packages are schema objects that group logically related PL/SQL types, variables, and subprograms.

A package will have two mandatory parts –

- **Package Specification**
- **Package Body or Definition**

### 1. Package Specification

The specification is the interface to the package. It just DECLARES the types, variables, constants, exceptions, cursors, and subprograms that can be referenced from outside the package. In other words, it contains all information about the content of the package, but excludes the code for the subprograms. All objects placed in the specification are called public objects. Any subprogram not in the package specification but coded in the package body is called a private object.

### 2. Package Body

The package body has the codes for various methods declared in the package specification and other private declarations, which are hidden from the code outside the package. The `CREATE PACKAGE BODY` Statement is used for creating the package body.

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

## PROGRAM

```sql
SQL> select*from customer;

NAME
--------------------------------------------------------------------------------
        ID     SALARY
---------- ----------
John Doe
         1      50000

Jane Smith
         2      60000

Mike Johnson
         3      70000

```

```sql
SQL> SET SERVEROUTPUT ON
```

```sql
SQL> CREATE OR REPLACE PACKAGE EmployeePackage AS
  2      FUNCTION getSalaryById(p_employeeId IN NUMBER) RETURN NUMBER;
  3  END EmployeePackage;
  4  /

Package created.
```
```sql
SQL> CREATE OR REPLACE PACKAGE BODY EmployeePackage AS
  2      FUNCTION getSalaryById(p_employeeId IN NUMBER) RETURN NUMBER IS
  3          v_salary NUMBER;
  4      BEGIN
  5          -- Perform the logic to retrieve the salary based on the employee id
  6          SELECT salary INTO v_salary FROM customer WHERE id = p_employeeId;
  7
  8          -- Return the salary
  9          RETURN v_salary;
 10      END getSalaryById;
 11  END EmployeePackage;
 12  /

Package body created.
```
```sql
SQL> DECLARE
  2      v_employeeId NUMBER := 1; -- Provide the employee id here
  3      v_salary NUMBER;
  4  BEGIN
  5      v_salary := EmployeePackage.getSalaryById(v_employeeId);
  6      DBMS_OUTPUT.PUT_LINE('Salary: ' || v_salary);
  7  END;
  8  /

PL/SQL procedure successfully completed.
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


## Question

2. Create a PL/SQL Package with addition and subtraction

```sql
CREATE OR REPLACE PACKAGE BODY OPERATION
is
PROCEDURE ADDITION(A IN NUMBER,B IN NUMBER)
is
begin
dbms_output.put_line('addition of two numbers: ' || ADD(A, B));
end;

FUNCTION SUB(A IN NUMBER, B IN NUMBER) RETURN NUMBER
is
ans number(3);
begin
ans := A - B;
return ans;
end;
end OPERATION;
/
```

## Output

```
SQL> start D://pacbody.sql
Package body created.
```
