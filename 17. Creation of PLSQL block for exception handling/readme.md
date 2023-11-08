# 17. CREATION OF PL/SQL BLOCK FOR EXCEPTION HANDLING

## AIM
To create a PL/SQL block for exception handling.

## Introduction
An exception is an error condition during a program execution. PL/SQL supports programmers to catch such conditions using EXCEPTION block in the program, and an appropriate action is taken against the error condition.

There are two types of exceptions:
1. System-defined exceptions
2. User-defined exceptions

## Syntax for Exception Handling
The general syntax for exception handling is as follows. The default exception will be handled using `WHEN OTHERS THEN`.

```sql
DECLARE
    <declaration section>
BEGIN
    <executable command(s)>
EXCEPTION
    <exception handling goes here >
    WHEN exception1 THEN
        exception1-handling-statements
    WHEN exception2 THEN
        exception2-handling-statements
    WHEN exception3 THEN
        exception3-handling-statements
    ...
    WHEN OTHERS THEN
        exception3-handling-statements
END;
```

## 2. Raising Exceptions
Exceptions are raised by the database server automatically whenever there is any internal database error, but exceptions can be raised explicitly by the programmer by using the command `RAISE`. Following is the simple syntax for raising an exception.

```sql
DECLARE
    exception_name EXCEPTION;
BEGIN
    IF condition THEN
        RAISE exception_name;
    END IF;
EXCEPTION
    WHEN exception_name THEN
        statement;
END;
```

## QUESTIONS

### 1. Write a PL/SQL program to implement exception handling

**ALGORITHM**
1. Start
2. Read employee id from the user
3. Check employee id
   3.1 If it is in table customer21 then display employee name and address
   3.2 If employee id is not in table customer21 then raise no found data exception
   3.3 If employee id is less than zero, raise an invalid exception
4. Stop

**PROGRAM**
```sql
SQL> SET SERVEROUTPUT ON
SQL> DECLARE
2 C_ID CUSTM25.ID%TYPE := &ID;
3 ENAME CUSTM25.NAME%TYPE;
4 ECITY CUSTM25.CITY%TYPE;
5 EX_INVALID_ID EXCEPTION;
6 BEGIN
7 IF C_ID <= 0 THEN
8 RAISE EX_INVALID_ID;
9 ELSE
10 SELECT NAME, CITY INTO ENAME, ECITY FROM CUSTM25 WHERE ID = C_ID;
11 DBMS_OUTPUT.PUT_LINE('NAME:' || ENAME);
12 DBMS_OUTPUT.PUT_LINE('ADDRESS:' || ECITY);
13 END IF;
14 EXCEPTION
15 WHEN EX_INVALID_ID THEN
16 DBMS_OUTPUT.PUT_LINE('ID MUST BE GREATER THAN ZERO!');
17 WHEN NO_DATA_FOUND THEN
18 DBMS_OUTPUT.PUT_LINE('NO SUCH CUSTOMER!');
19 WHEN OTHERS THEN
20 DBMS_OUTPUT.PUT_LINE('ERROR');
21 END;
22 /
```

**OUTPUT**
```
Enter value for id: 1002
old 2: C_ID CUSTM25.ID%TYPE := &ID;
new 2: C_ID CUSTM25.ID%TYPE := 1002;
NAME: RENJU
ADDRESS: TVM
PL/SQL procedure successfully completed.
```

```
Enter value for id: -9
old 2: C_ID CUSTM25.ID%TYPE := &ID;
new 2: C_ID CUSTM25.ID%TYPE := -9;
ID MUST BE GREATER THAN ZERO!
PL/SQL procedure successfully completed.
```

```
Enter value for id: 5000
old 2: C_ID CUSTM25.ID%TYPE := &ID;
new 2: C_ID CUSTM25.ID%TYPE := 5000;
NO SUCH CUSTOMER!
PL/SQL procedure successfully completed.
```

### 2. Write a PL/SQL program to raise an exception when dividing by zero

**ALGORITHM**
1. Start
2. Enter two numbers
3. Perform the division operation
4. Display the result
5. Raise an exception when dividing by zero
6. Stop

**PROGRAM**
```sql
SQL> SET SERVEROUTPUT ON
SQL> DECLARE
2 A INT := &NUM1;
3 B INT := &NUM2;
4 ANSWER INT;
5 BEGIN
6 ANSWER := A / B;
7 DBMS_OUTPUT.PUT_LINE('THE RESULT AFTER DIVISION IS: ' || ANSWER);
8 EXCEPTION
9 WHEN ZERO_DIVIDE THEN
10 DBMS_OUTPUT.PUT_LINE('DIVIDING BY ZERO PLEASE CHECK THE VALUES AGAIN');
11 DBMS_OUTPUT.PUT_LINE('THE VALUE OF A IS ' || A);
12 DBMS_OUTPUT.PUT_LINE('THE VALUE OF B IS ' || B);
13 END;
14 /
```

**OUTPUT**
```
Enter value for num1: 25
old 2: A INT := &NUM1;
new 2: A INT := 25;
Enter value for num2: 5
old 3: B INT := &NUM2;
new 3: B INT := 5;
THE RESULT AFTER DIVISION IS: 5
PL/SQL procedure successfully completed.
```

```
Enter value for num1: 25
old 2: A INT := &NUM1;
new 2: A INT := 25;
Enter value for num2: 0
old 3: B INT := &NUM2;
new 3: B INT := 0;
DIVIDING BY ZERO PLEASE CHECK THE VALUES AGAIN
THE VALUE OF A IS 25
THE VALUE OF B IS 0
PL/SQL procedure successfully completed.
```

### 3. Write a PL/SQL block to handle the following BUILT-IN EXCEPTIONS.

```sql
DECLARE
    M NUMBER(4);
    MYERROR EXCEPTION;
BEGIN
    SELECT COMM INTO M FROM EMP WHERE EMPNO = 7839;
    IF M IS NULL THEN
        RAISE MYERROR;
    END IF;
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('ERROR OF DATA');
    WHEN TOO_MANY_ROWS THEN
        DBMS_OUTPUT.PUT_LINE('ERROR OF TOO MANY ROWS');
    WHEN MYERROR THEN
        DBMS_OUTPUT.PUT_LINE('ERROR FOUND NULL');
END;
/
```
