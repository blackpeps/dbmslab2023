# 14. Creation of procedures, triggers, functions

## AIM

To create procedures, triggers, and functions.

## THEORY

### Procedures

- Subprogram in Modular Design:
  - Program unit/module for a specific task.
  - Combined for larger programs in 'Modular design.'
  - Invoked by another subprogram or program (calling program).

- Standalone Schema-level subprogram:
  - Created with `CREATE PROCEDURE` or `CREATE FUNCTION`.
  - Stored in the database, deletable with `DROP PROCEDURE` or `DROP FUNCTION`.

- Packaged subprogram:
  - Created within a package.
  - Stored in the database, deletable only with the package using `DROP PACKAGE`.

#### 1.1 Creating a Procedure

  - Use `CREATE OR REPLACE PROCEDURE` statement.
  - Syntax:
    ```sql
    CREATE [OR REPLACE] PROCEDURE procedure_name
    [(parameter_name [IN | OUT | IN OUT] type [, ...])]
    {IS | AS}
    BEGIN
     < procedure_body >
    END procedure_name;
    ```

#### 1.2 Deleting a Standalone Procedure

  - Use `DROP PROCEDURE` statement.
  - Syntax:
    ```sql
    DROP PROCEDURE procedure_name;
    ```

#### 1.3 Parameter modes in PL/SQL subprograms:

- **IN Parameter**:
  - Read-only; passed by reference.
  - Accepts constants, literals, initialized variables, or expressions.
  - Can have a default value; omitted if not provided.

- **OUT Parameter**:
  - Returns a value to the calling program.
  - Acts like a variable; value can be changed and referenced after assignment.
  - Actual parameter must be a variable; passed by value.

- **IN OUT Parameter**:
  - Passes an initial value and returns an updated value.
  - Can be assigned and read.
  - Actual parameter must be a variable; passed by value.

### 2. Function

#### 2.1 Creating a Function

  - Use `CREATE OR REPLACE FUNCTION` statement.
  - Syntax:
    ```sql
    CREATE [OR REPLACE] FUNCTION function_name
    [(parameter_name [IN | OUT | IN OUT] type [, ...])]
    RETURN return_datatype
    {IS | AS}
    BEGIN
     < function_body >
    END [function_name];
    ```

#### 2.2 Calling a Function

  - Defined for specific tasks.
  - Called in the program, transferring control to the function.
  - Performs its task and returns control.
  - Control returns on encountering a return statement or reaching the last "END" statement.

### 3. Trigger

  - Stored programs.
  - Automatically executed when events occur.
  - Defined on tables, views, schemas, or databases associated with the event.

#### 3.1 Creating Triggers

The syntax:

```sql
CREATE [OR REPLACE ] TRIGGER trigger_name {BEFORE | AFTER | INSTEAD OF }{INSERT [OR] | UPDATE [OR] | DELETE} [OF col_name] ON table_name [REFERENCING OLD AS.NEW AS n][FOR EACH ROW] WHEN (condition)
DECLARE
Declaration-statements
BEGIN
Executable-statements
EXCEPTION
Exception-handling-statements
END;
```

## QUESTIONS

### PROCEDURE

1. Write a PL/SQL program to generate the Fibonacci series using a procedure

#### ALGORITHM

**Step 1:** Start

**Step 2:** Read the limit

**Step 3:** Call procedure, `FIB(number)`

**Step 4:** Stop

**FIB(number)**

**Step 1:** Start

**Step 2:** Initialize A and VAL as zero

**Step 3:** Display the first two terms of the series

**Step 4:** Repeat until `VAL != N-2`

- **4:1** Calculate `C = A + B`

- **4:2** Display `C`

- **4:3** Perform swapping

- **4:4** Set `VAL` as `VAL + 1`

**Step 5:** Stop

### Functions

2. Write a PL/SQL program to display the Nth prime number using the function 

#### ALGORITHM

**Step 1:** Start

**Step 2:** Read a number, NO

**Step 3:** Call function PMN(NO)

**Step 4:** Display Nth prime number

**Step 5:** Stop

*PMN(N)*

**Step 1:** Start

**Step 2:** Initialize P and C as Zero

**Step 3:** Repeat loop until I=100

     **3:1** Check if I%J=0 then set C=C+1
     
     **3:2** If C=2 then set P as P+1
     
     **3:3** Check if P=N then return i
     
**Step 4:** Stop

### Trigger

3. Create a table customer21 and Write a PL/SQL program to display the salary difference of an employee in the customer table using a trigger.

| ID    | NAME   | AGE | CITY      | DEP | DESG      | SAL   |
|-------|--------|-----|-----------|-----|-----------|-------|
| 7001  | Sethu  | 33  | Wayanad   | 31  | Developer | 35000 |
| 9001  | Jaya   | 34  | Pandalam  | 31  | Designer  | 30000 |
| 10001 | Heeral | 37  | Kollam    | 31  | Clerk     | 25000 |
| 10011 | Rimal  | 28  | Pala      | 31  | Designer  | 27000 |
| 10021 | Janil  | 39  | Kottayam  | 31  | Tester    | 20000 |
| 10031 | Hari   | 40  | TVM       | 31  | Manager   | 67000 | 

#### ALGORITHM

**Step 1:** Start

**Step 2:** Create a trigger for the customer21 table that fires for insert, update or delete operation to display the salary difference

**Step 3:** Inserting a new employee

**Step 4:** Modify the salary

**Step 5:** Calculate the salary difference

**Step 6:** Display the difference

**Step 7:** Stop

---

## OUTPUT

### PROCEDURE

#### PROGRAM

```sql
SQL> CREATE OR REPLACE PROCEDURE FIB(N IN NUMBER)
 2 IS
 3 A NUMBER(5):=0;
 4 B NUMBER(3):=1;
 5 C NUMBER(3);
 6 T NUMBER(5);
 7 VAL NUMBER(5):=0;
 8 BEGIN
 9 DBMS_OUTPUT.PUT_LINE('FIBONACCI SERIES IS:');
 10 DBMS_OUTPUT.PUT_LINE(A);
 11 DBMS_OUTPUT.PUT_LINE(B);
 12 WHILE VAL!=N-2
 13 LOOP
 14 C:=A+B;
 15 DBMS_OUTPUT.PUT_LINE(C);
 16 T:=B;
 17 B:=C;
 18 A:=T;
 19 VAL:=VAL+1;
 20 END LOOP;
 21 END;
 22 /
```

#### OUTPUT

```
SQL> SET SERVEROUTPUT ON
SQL> DECLARE F NUMBER(5):=&LIMIT;
2 BEGIN FIB(F);
3 END;
4 /
OUTPUT
Enter value for limit: 6
old 2: F NUMBER(5):=&LIMIT;
new 2: F NUMBER(5):=6;
FIBONACCI SERIES IS:
0
1
1
2
3
5
PL/SQL procedure successfully completed.
```

### FUNCTION

#### PROGRAM

```sql
SQL> CREATE OR REPLACE FUNCTION PMN(N IN NUMBER) RETURN NUMBER
 2 IS
 3 C NUMBER(5);
 4 P NUMBER(5):=0;
 5 I NUMBER(5);
 6 J NUMBER(5);
 7 BEGIN
 8 FOR I IN 2..100
 9 LOOP
 10 C:=0;
 11 FOR J IN 1..I
 12 LOOP
 13 IF MOD(I,J)=0 THEN
 14 C:=C+1;
 15 END IF;
 16 END LOOP;
 17 IF C=2 THEN
 18 P:=P+1;
 19 END IF;
 20 IF P=N THEN
 21 RETURN(I);
 22 END IF;
 23 END LOOP;
 24 END;
 25 / 

```
#### OUTPUT

```sql
SQL> SET SERVEROUTPUT ON
SQL> DECLARE
 2 NO NUMBER(5):=&LIMIT;
 3 BEGIN
 4 DBMS_OUTPUT.PUT_LINE(NO||'TH PRIME NUMBER IS:'||PMN(NO));
 5 END;
 6 / 
```

```sql
Enter value for limit: 10
old 2: NO NUMBER(5):=&LIMIT;
new 2: NO NUMBER(5):=10;
10TH PRIME NUMBER IS:29
PL/SQL procedure successfully completed.
```

### 3. TRIGGER

#### PROGRAM

```sql
1) SQL> CREATE TABLE CUSTOMER21(ID NUMBER,NAME VARCHAR(50),AGE NUMBER,CITY VARCHAR(50),DEP NUMBER,DESG VARCHAR(50),SAL NUMBER);
Table created.
SQL> INSERT INTO CUSTOMER21 VALUES(700,'REKHA',33,'ALAPPY',3,'DEVELOPER',35000);
1 row created.
SQL> INSERT INTO CUSTOMER21 VALUES(900,'ARYA',34,'PANDALAM',3,'DESIGNER',30000);
1 row created.
SQL> INSERT INTO CUSTOMER21 VALUES(1000,'JENITA',37,'KOLLAM',1,'CLERK',25000);
1 row created.
SQL> INSERT INTO CUSTOMER21 VALUES(1001,'AKASH',28,'PALA',1,'DESIGNER',27000);
1 row created.
SQL> INSERT INTO CUSTOMER21 VALUES(1002,'SANJU',39,'KOTYAM',3,'TESTER',20000);
1 row created.
SQL> INSERT INTO CUSTOMER21 VALUES(1003,'HARI',40,'TVM',1,'MANAGER',67000);
1 row created.
2)SQL> SET SERVEROUTPUT ON
SQL> CREATE OR REPLACE TRIGGER DISPLAY_SALARY_CHANGES BEFORE DELETE OR INSERT OR UPDATE ON CUSTOMER21 FOR EACH ROW
2 WHEN (NEW.ID > 0)
3 DECLARE
4 SAL_DIFF NUMBER;
5 BEGIN
6 SAL_DIFF := :NEW.SAL - :OLD.SAL;
7 DBMS_OUTPUT.PUT_LINE('OLD SALARY: ' || :OLD.SAL);
8 DBMS_OUTPUT.PUT_LINE('NEW SALARY: ' || :NEW.SAL);
9 DBMS_OUTPUT.PUT_LINE('SALARY DIFFERENCE: ' || SAL_DIFF);
10 END;
11 /
Trigger created.
```

#### OUTPUT

```sql
SQL> INSERT INTO CUSTOMER21 VALUES('780','NEERAV',21,'TVM',2,'GM',80000);
OLD SALARY:
NEW SALARY: 80000
SALARY DIFFERENCE:
1 row created.
SQL> UPDATE CUSTOMER21 SET SAL=90000 WHERE ID='780';
OLD SALARY: 80000
NEW SALARY: 90000
SALARY DIFFERENCE: 10000
1 row updated.
```
