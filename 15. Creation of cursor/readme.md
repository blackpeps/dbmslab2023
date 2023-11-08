# 15. CREATION OF CURSORS

## AIM
To create a cursor in PL/SQL.

## Introduction
A cursor is a pointer to this context area. PL/SQL controls the context area through a cursor. A cursor holds the rows (one or more) returned by a SQL statement. The set of rows the cursor holds is referred to as the active set.

### Types of Cursors
There are two types of cursors:
1. **Implicit Cursors**
   - Implicit cursors are automatically created by Oracle whenever an SQL statement is executed when there is no explicit cursor for the statement.
   - Programmers cannot control the implicit cursors and the information in them.
   
   Whenever a DML statement (INSERT, UPDATE, and DELETE) is issued, an implicit cursor is associated with this statement. For INSERT operations, the cursor holds the data that needs to be inserted. For UPDATE and DELETE operations, the cursor identifies the rows that would be affected.

   | S.NO | ATTRIBUTES & DESCRIPTION      |
   | ---- | ----------------------------- |
   | 1    | %FOUND                        |
   |      | Returns TRUE if an INSERT, UPDATE, or DELETE statement affected one or more rows or a SELECT INTO statement returned one or more rows. Otherwise, it returns FALSE. |
   | 2    | %NOTFOUND                     |
   |      | The logical opposite of %FOUND. It returns TRUE if an INSERT, UPDATE, or DELETE statement affected no rows, or a SELECT INTO statement returned no rows. Otherwise, it returns FALSE. |
   | 3    | %ISOPEN                       |
   |      | Always returns FALSE for implicit cursors, because Oracle closes the SQL cursor automatically after executing its associated SQL statement. |
   | 4    | %ROWCOUNT                     |
   |      | Returns the number of rows affected by an INSERT, UPDATE, or DELETE statement, or returned by a SELECT INTO statement |

2. **Explicit Cursors**
   - Explicit cursors are programmer-defined cursors for gaining more control over the context area.
   - An explicit cursor should be defined in the declaration section of the PL/SQL Block.
   - It is created on a SELECT Statement that returns more than one row.

   The syntax for creating an explicit cursor is:
   ```sql
   CURSOR cursor_name IS select_statement;
   ```

## Working with Explicit Cursors
Working with an explicit cursor includes the following steps:
1. Declaring the cursor for initializing the memory
2. Opening the cursor for allocating the memory
3. Fetching the cursor for retrieving the data
4. Closing the cursor to release the allocated memory

### 2.1 Declaring the Cursor
Declaring the cursor defines the cursor with a name and the associated SELECT statement.
```sql
CURSOR c_customers IS SELECT id, name, address FROM customers;
```

### 2.2 Opening the Cursor
Opening the cursor allocates the memory for the cursor and makes it ready for fetching the rows returned by the SQL statement into it.
```sql
OPEN c_customers;
```

### 2.3 Fetching the Cursor
Fetching the cursor involves accessing one row at a time.
```sql
FETCH c_customers INTO c_id, c_name, c_addr;
```

### 2.4 Closing the Cursor
Closing the cursor means releasing the allocated memory.
```sql
CLOSE c_customers;
```

## QUESTIONS

### 1. To write a PL/SQL program to display customer id, name, designation, and salary of employees whose salary is greater than 28000 from the customer table using a cursor

**ALGORITHM**
1. Start
2. Create a cursor to select employee id, name, designation, and salary from the customer table
3. Fetch the cursor into id, name, designation, and salary
4. Repeat the loop while data is found
   4.1 Check if the salary is greater than 28000, then display id, name, designation, and salary of the employee
5. Stop

**PROGRAM**
```sql
SQL> SET SERVEROUTPUT ON
SQL> DECLARE
2 CURSOR CUR IS SELECT ID, NAME, DESG, SAL FROM CUSTM25 WHERE SAL > 28000;
3 C_ID CUSTM25.ID%TYPE;
4 C_NAME CUSTM25.NAME%TYPE;
5 C_DESG CUSTM25.DESG%TYPE;
6 C_SAL CUSTM25.SAL%TYPE;
7 BEGIN
8 OPEN CUR;
9 FETCH CUR INTO C_ID, C_NAME, C_DESG, C_SAL;
10 WHILE CUR%FOUND
11 LOOP
12 IF C_SAL > 28000 THEN
13 DBMS_OUTPUT.PUT_LINE(C_ID || ' ' || C_NAME || ' ' || C_DESG || ' ' || C_SAL);
14 END IF;
15 FETCH CUR INTO C_ID, C_NAME, C_DESG, C_SAL;
16 END LOOP;
17 CLOSE CUR;
18 END;
19 /
```

**OUTPUT**
```
700 SANJU HECKER 35000
900 MANJU DESIGNER 30000
1002 RENJU MANAGER 67000
780 RINJU GM 90000
PL/SQL procedure successfully completed.
```

### 2. To write a PL/SQL program to display customer id, name, designation, and salary of employees whose salary is greater than 28000 from the customer table using a cursor

**ALGORITHM**
1. Start
2. Create a cursor and select employee id, name, department, designation, and salary from the customer table
3. Read department number
4. Fetching the cursor into employee number, name, department, designation, and salary
5. Repeat while data is found
   5.1 If the department number from the table is equal to the department number entered by the user, then display employee details
6. Close the cursor
7. Stop

**PROGRAM**
```sql
SQL> SET SERVEROUTPUT ON
SQL> DECLARE
2 CURSOR CURR2 IS SELECT ID, NAME, DEP, DESG, SAL FROM CUSTM25;
3 CID CUSTM25.ID%TYPE;
4 CNAME CUSTM25.NAME%TYPE;
5 CDEP CUSTM25.DEP%TYPE;
6 CDESG CUSTM25.DESG%TYPE;
7 CSAL CUSTM25.SAL%TYPE;
8 DP NUMBER := &DID;
9 BEGIN
10 OPEN CURR2;
11 FETCH CURR2 INTO CID, CNAME, CDEP, CDESG, CSAL;
12 WHILE CURR2%FOUND
13 LOOP
14 IF CDEP = DP THEN
15 DBMS_OUTPUT.PUT_LINE(CID || ' ' || CNAME || ' ' || CDESG || ' ' || CSAL);
16 END IF;
17 FETCH CURR2 INTO CID, CNAME, CDEP, CDESG, CSAL;
18 END LOOP;
19 CLOSE CURR2;
20 END;
21 /
```

**OUTPUT**
```
Enter value for did: 1
old 8: DP NUMBER:=&DID;
new 8: DP NUMBER:=1;
1000 KUNJU CLERK 25000
1001 ANJU DESIGNER 

27000
1002 RENJU MANAGER 67000
780 RINJU GM 90000
PL/SQL procedure successfully completed.
```

### 3. To write a Cursor to display the list of 10 highest-paid Employees and their Total Salary

**INPUT**
```sql
set serveroutput on;
declare
cursor c is
select empid, empname, salary from emplo order by salary desc;
name emplo.empname%type;
id emplo.empid%type;
sal emplo.salary%type;
tot emplo.salary%type;
i int;
begin
tot:=0;
open c;
for i in 1..10
loop
fetch c into id, name, sal;
exit when c%NOTFOUND;
tot:=tot+sal;
dbms_output.put_line('EMPLOYEE ID:' || id);
dbms_output.put_line('EMPLOYEE NAME:' || name);
dbms_output.put_line('SALARY:' || sal);
dbms_output.put_line('*********************');
end loop;
dbms_output.put_line('TOTAL SALARY:' || tot);
commit;
close c;
end;
/
```
