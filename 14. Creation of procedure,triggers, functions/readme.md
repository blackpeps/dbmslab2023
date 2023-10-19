## 14. Creation of procedures, triggers, functions

# INCOMPLETE MAY MAKE MODIFICATIONS IN FUTURE, PLEASE BE AWARE BEFORE EXECUTING COMMANDS. YOU MAY GO THROUGH THE THEORY SECTION.

# Procedures

A subprogram is a program unit/module that performs a particular task. These subprograms are combined to form larger programs. This is basically called the 'Modular design'. A subprogram can be invoked by another subprogram or program, which is called the calling program.

At the schema level, a subprogram is a standalone subprogram. It is created with the `CREATE PROCEDURE` or the `CREATE FUNCTION` statement. It is stored in the database and can be deleted with the `DROP PROCEDURE` or `DROP FUNCTION` statement. A subprogram created inside a package is a packaged subprogram. It is stored in the database and can be deleted only when the package is deleted with the `DROP PACKAGE` statement.

**PL/SQL subprograms** are named PL/SQL blocks that can be invoked with parameters.

PL/SQL provides two kinds of subprograms:

- **Functions** – These subprograms return a single value; mainly used to compute and return a value.
- **Procedures** – These subprograms do not return a value directly; mainly used to perform an action.

## 1.1 Creating a Procedure

A procedure is created with the `CREATE OR REPLACE PROCEDURE` statement. The simplified syntax for the `CREATE OR REPLACE PROCEDURE` statement is as follows:

```sql
CREATE [OR REPLACE] PROCEDURE procedure_name[(parameter_name [IN | OUT | IN OUT] type [, ...])]
{IS | AS}
BEGIN
 < procedure_body >
END procedure_name;
```

Where:
- `procedure_name` specifies the name of the procedure.
- `[OR REPLACE]` option allows the modification of an existing procedure.
- The optional parameter list contains name, mode, and types of the parameters. `IN` represents the value that will be passed from outside, and `OUT` represents the parameter that will be used to return a value outside of the procedure.
- `procedure_body` contains the executable part.
- The `AS` keyword is used instead of the `IS` keyword for creating a standalone procedure.

## 1.2 Deleting a Standalone Procedure

A standalone procedure is deleted with the `DROP PROCEDURE` statement. Syntax for deleting a procedure is:

```sql
DROP PROCEDURE procedure-name;
```

## 1.3 Parameter Modes in PL/SQL Subprograms

### IN

An IN parameter lets you pass a value to the subprogram. It is a read-only parameter. Inside the subprogram, an IN parameter acts like a constant. It cannot be assigned a value. You can pass a constant, literal, initialized variable, or expression as an IN parameter. You can also initialize it to a default value; however, in that case, it is omitted from the subprogram call. It is the default mode of parameter passing. Parameters are passed by reference.

### OUT

An OUT parameter returns a value to the calling program. Inside the subprogram, an OUT parameter acts like a variable. You can change its value and reference the value after assigning it. The actual parameter must be a variable, and it is passed by value.

### IN OUT

An IN OUT parameter passes an initial value to a subprogram and returns an updated value to the caller. It can be assigned a value, and the value can be read. The actual parameter corresponding to an IN OUT formal parameter must be a variable, not a constant or an expression. Formal parameter must be assigned a value. Actual parameter is passed by value.

# 2. Function

## 2.1 Creating a Function

A standalone function is created using the `CREATE FUNCTION` statement. The simplified syntax for the `CREATE OR REPLACE FUNCTION` statement is as follows:

```sql
CREATE [OR REPLACE] FUNCTION function_name [(parameter_name [IN | OUT | IN OUT] type [, ...])]
RETURN return_datatype
{IS | AS}
BEGIN
 < function_body >
END [function_name];
```

Where:
- `function_name` specifies the name of the function.
- `[OR REPLACE]` option allows the modification of an existing function.
- The optional parameter list contains name, mode, and types of the parameters. `IN` represents the value that will be passed from outside, and `OUT` represents the parameter that will be used to return a value outside of the procedure.
- The function must contain a return statement.
- The `RETURN` clause specifies the data type you are going to return from the function.
- `function_body` contains the executable part.
- The `AS` keyword is used instead of the `IS` keyword for creating a standalone function.

## 2.2 Calling a Function

While creating a function, you give a definition of what the function has to do. To use a function, you will have to call that function to perform the defined task. When a program calls a function, the program control is transferred to the called function. A called function performs the defined task and when its return statement is executed or when the last `END` statement is reached, it returns the program control back to the main program.

# 3. Trigger

Triggers are stored programs, which are automatically executed or fired when some events occur. Triggers can be defined on the table, view, schema, or database with which the event is associated.

## 3.1 Benefits of Triggers

Triggers can be written for the following purposes:

- Generating some derived column values automatically
- Enforcing referential integrity
- Event logging and storing information on table access
- Auditing
- Synchronous replication of tables
- Imposing security authorizations
- Preventing invalid transactions

## 3.2 Creating Triggers

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

Where:
- `CREATE [OR REPLACE] TRIGGER trigger_name` − Creates or replaces an existing trigger with the trigger_name.
- `{BEFORE | AFTER | INSTEAD OF}` − This specifies when the trigger will be executed. The `INSTEAD OF` clause is used for creating a trigger on a view.
- `{INSERT [OR] | UPDATE [OR] | DELETE}` − This specifies the DML operation.
- `[OF col_name]` − This specifies the column name that will be updated.
- `[ON table_name]` − This specifies the name of the table associated with the trigger.
- `[REFERENCING OLD AS o NEW AS n]` − This allows you to refer new and old values for various DML statements, such as INSERT, UPDATE, and DELETE.
- `[FOR EACH ROW]` − This specifies a row-level trigger, i.e., the trigger will be executed for each row being affected. Otherwise, the trigger will execute just once when the SQL statement is executed, which is called a table-level trigger.
- `WHEN (condition)` − This provides a condition for rows for which the trigger would fire. This clause is valid only for row-level triggers.

---

## 1. PROCEDURE

### QUESTION

1. Write a PL/SQL program to generate Fibonacci series using a procedure

### ALGORITHM

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

# PROGRAM

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

# OUTPUT

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

## 2. FUNCTION

### QUESTION

1. Write a PL/SQL program to display Nth prime number using function 

### ALGORITHM

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

# PROGRAM

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
# OUTPUT

```
SQL> SET SERVEROUTPUT ON
SQL> DECLARE
 2 NO NUMBER(5):=&LIMIT;
 3 BEGIN
 4 DBMS_OUTPUT.PUT_LINE(NO||'TH PRIME NUMBER IS:'||PMN(NO));
 5 END;
 6 / 
```

## 3. TRIGGER

### QUESTION

1. Create a table customer21 with the following fields.

| ID    | NAME   | AGE | CITY      | DEP | DESG      | SAL   |
|-------|--------|-----|-----------|-----|-----------|-------|
| 7001  | Sethu  | 33  | Wayanad   | 31  | Developer | 35000 |
| 9001  | Jaya   | 34  | Pandalam  | 31  | Designer  | 30000 |
| 10001 | Heeral | 37  | Kollam    | 31  | Clerk     | 25000 |
| 10011 | Rimal  | 28  | Pala      | 31  | Designer  | 27000 |
| 10021 | Janil  | 39  | Kottayam  | 31  | Tester    | 20000 |
| 10031 | Hari   | 40  | TVM       | 31  | Manager   | 67000 |

## Practise Question

2. Write a PL/SQL program to display the salary difference of an employee in the customer table using a trigger

### ALGORITHM

**Step 1:** Start

**Step 2:** Create a trigger for the customer21 table that fires for insert or update or delete operation to display the salary difference

**Step 3:** Inserting a new employee

**Step 4:** Modify the salary

**Step 5:** Calculate the salary difference

**Step 6:** Display the difference

**Step 7:** Stop

# PROGRAM

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

# OUTPUT

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
