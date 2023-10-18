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
SQL> CREATE PACKAGE CUSTOMER_SAL AS PROCEDURE FIND_SALARY(C_ID CUSTOMER21.ID%TYPE);
2 END CUSTOMER_SAL;
3 /
Package created.
SQL> CREATE OR REPLACE PACKAGE BODY CUSTOMER_SAL AS PROCEDURE FIND_SALARY(C_ID CUSTOMER21.ID%TYPE) IS C_SAL CUSTOMER21.SAL%TYPE;
2 BEGIN
3 SELECT SAL INTO C_SAL FROM CUSTOMER21 WHERE ID=C_ID;
4 DBMS_OUTPUT.PUT_LINE('SALARY:'||C_SAL);
5 END FIND_SALARY;
6 END CUSTOMER_SAL;
7 /
Package body created.
SQL> DECLARE
2 CODE CUSTOMER21.ID%TYPE:=&CC_ID;
3 BEGIN
4 CUSTOMER_SAL.FIND_SALARY(CODE);
5 END;
6 /
```

## OUTPUT

```
Enter value for cc_id: 1000
old 2: CODE CUSTOMER21.ID%TYPE:=&CC_ID;
new 2: CODE CUSTOMER21.ID%TYPE:=1000;
SALARY: 25000
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
