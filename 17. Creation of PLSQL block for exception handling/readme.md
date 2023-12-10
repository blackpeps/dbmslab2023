# 17. CREATION OF PL/SQL BLOCK FOR EXCEPTION HANDLING

## AIM
To create a PL/SQL block for exception handling.

## THEORY
An exception is an error condition during a program execution. PL/SQL supports programmers in catching such conditions using the EXCEPTION block in the program, and appropriate action is taken against the error condition.

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
SQL> DECLARE
  2  A NUMBER(4):=&NUM1;
  3  B NUMBER(4):=&NUM2;
  4  ANS NUMBER(8):=0;
  5  ZERO_DIVIDE EXCEPTION;
  6  BEGIN
  7  IF B=0 THEN
  8  RAISE ZERO_DIVIDE;
  9  ELSE
 10  ANS:=A/B;
 11  DBMS_OUTPUT.PUT_LINE('RESULT: '||ANS);
 12  END IF;
 13  EXCEPTION
 14  WHEN ZERO_DIVIDE THEN
 15  DBMS_OUTPUT.PUT_LINE('DIVIDE BY ZERO NOT POSSIBLE');
 16  END;
 17  /
```

**OUTPUT**
```
Enter value for num1: 0
old   2: A NUMBER(4):=&NUM1;
new   2: A NUMBER(4):=0;
Enter value for num2: 5
old   3: B NUMBER(4):=&NUM2;
new   3: B NUMBER(4):=5;
RESULT: 0
PL/SQL procedure successfully completed.
```

```
Enter value for num1: 7
old   2: A NUMBER(4):=&NUM1;
new   2: A NUMBER(4):=7;
Enter value for num2: 0
old   3: B NUMBER(4):=&NUM2;
new   3: B NUMBER(4):=0;
DIVIDE BY ZERO NOT POSSIBLE
PL/SQL procedure successfully completed.
```

### 3. Write a PL/SQL block to handle the following BUILT-IN EXCEPTIONS.

**PROGRAM**

```sql
CREATE TABLE CUSTOMER17 (ID NUMBER, NAME VARCHAR(50), AGE NUMBER);
INSERT INTO CUSTOMER17 VALUES (1, 'MEENA', 22);
INSERT INTO CUSTOMER17 VALUES (2, 'REENA', 22);
INSERT INTO CUSTOMER17 VALUES (3, 'VEENA', 20);
INSERT INTO CUSTOMER17 VALUES (3, 'BEENA', 21);
```
```sql
DECLARE
	E_ID NUMBER:=&EID;
	M NUMBER(4);
	NULL_ERROR EXCEPTION;
BEGIN
	SELECT AGE INTO M FROM CUSTOMER17 WHERE ID=E_ID;
	IF M IS NULL THEN
		RAISE NULL_ERROR;
	END IF;
EXCEPTION
	WHEN NO_DATA_FOUND THEN
		DBMS_OUTPUT.PUT_LINE('NO SUCH DATA FOUND');
	WHEN TOO_MANY_ROWS THEN
		DBMS_OUTPUT.PUT_LINE('MANY ROWS PRESENT');
	WHEN NULL_ERROR THEN
		DBMS_OUTPUT.PUT_LINE('ERROR DUE TO NULL');
END;
/
```

**OUTPUT**

```sql
Enter value for eid: 3
old   2:        E_ID NUMBER:=&EID;
new   2:        E_ID NUMBER:=3;
MANY ROWS PRESENT
PL/SQL procedure successfully completed.
```
```sql
Enter value for eid: 4
old   2:        E_ID NUMBER:=&EID;
new   2:        E_ID NUMBER:=4;
NO SUCH DATA FOUND
PL/SQL procedure successfully completed.
```
