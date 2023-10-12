## 14. Creation of procedure,triggers, functions

1. Procedures
A subprogram is a program unit/module is a program unit/module that performs a
particular task. These subprograms are combined to form larger programs. This is that
performs a particular task. This is basically called the 'Modular design'. A subprogram
can be invoked by another subprogram or program which is called the calling program.
At the schema level, subprogram is a standalone subprogram. It is created with the
CREATE PROCEDURE or the CREATE FUNCTION statement. It is stored in the
database and can be deleted with the DROP PROCEDURE or DROP FUNCTION
statement. A subprogram created inside a package is a packaged subprogram. It is
stored in the database and can be deleted only when the package is deleted with the
DROP PACKAGE statement.
PL/SQL subprograms are named PL/SQL blocks that can be invoked with a set of
parameters.
PL/SQL provides two kinds of subprograms –
 Functions − These subprograms return a single value; mainly used to compute and
return a value.
 Procedures − These subprograms do not return a value directly; mainly used to
perform an action.
1.1 Creating a Procedure
A procedure is created with the CREATE OR REPLACE PROCEDURE statement.
The simplified syntax for the CREATE OR REPLACE PROCEDURE statement is as
follows –
CREATE [OR REPLACE] PROCEDURE procedure_name[(parameter_name [IN | OUT | IN
OUT] type [, ...])]
{IS | AS}
BEGIN
 < procedure_body >
END procedure_name;
Where,
 procedure-name specifies the name of the procedure.
 [OR REPLACE] option allows the modification of an existing procedure.
 The optional parameter list contains name, mode and types of the parameters. IN
represents the value that will be passed from outside and OUT represents the
parameter that will be used to return a value outside of the procedure.
 procedure-body contains the executable part.
 The AS keyword is used instead of the IS keyword for creating a standalone
procedure.
1.2 Deleting a Standalone Procedure
A standalone procedure is deleted with the DROP PROCEDURE statement. Syntax for
deleting a procedure is –
 DROP PROCEDURE procedure-name;
1.3 Parameter Modes in PL/SQL Subprograms
The following table lists out the parameter modes in PL/SQL subprograms –
S.NO PARAMETER MODE & DESCRIPTION
1 IN
An IN parameter lets you pass a value to the subprogram. It is a read-only
parameter. Inside the subprogram, an IN parameter acts like a constant. It
cannot be assigned a value. You can pass a constant, literal, initialized
variable, or expression as an IN parameter. You can also initialize it to a
default value; however, in that case, it is omitted from the subprogram call. It
is the default mode of parameter passing. Parameters are passed by
reference.
2 OUT
An OUT parameter returns a value to the calling program. Inside the
subprogram, an OUT parameter acts like a variable. You can change its value
and reference the value after assigning it. The actual parameter must be
variable, and it is passed by value
.
3 IN OUT
An IN OUT parameter passes an initial value to a subprogram and returns an
updated value to the caller. It can be assigned a value and the value can be
read.
The actual parameter corresponding to an IN OUT formal parameter must be
a variable, not a constant or an expression. Formal parameter must be
assigned a value. Actual parameter is passed by value.
2. Function
2.1 Creating a Function
A standalone function is created using the CREATE FUNCTION statement. The
simplified syntax for the CREATE OR REPLACE PROCEDURE statement is as follows
CREATE [OR REPLACE] FUNCTION function_name [(parameter_name [IN | OUT | IN
OUT] type [, ...])]
RETURN return_datatype
{IS | AS}
BEGIN
 < function_body >
END [function_name];
Where,
 function-name specifies the name of the function.
 [OR REPLACE] option allows the modification of an existing function.
 The optional parameter list contains name, mode and types of the parameters. IN
represents the value that will be passed from outside and OUT represents the
parameter that will be used to return a value outside of the procedure.
 The function must contain a return statement.
 The RETURN clause specifies the data type you are going to return from the function.
 function-body contains the executable part.
 The AS keyword is used instead of the IS keyword for creating a standalone function.
2.2 Calling a Function
 While creating a function, you give a definition of what the function has to do. To use a
function, you will have to call that function to perform the defined task. When a program
calls a function, the program control is transferred to the called function.
 A called function performs the defined task and when its return statement is executed or
when the last end statement is reached, it returns the program control back to the main
program
3. Trigger
Triggers are stored programs, which are automatically executed or fired when some
events occur. Triggers can be defined on the table, view, schema, or database with which
the event is associated.
3.1 Benefits of Triggers
Triggers can be written for the following purposes –
 Generating some derived column values automatically
 Enforcing referential integrity
 Event logging and storing information on table access
 Auditing
 Synchronous replication of tables
 Imposing security authorizations
 Preventing invalid transactions
3.2Creating Triggers
The syntax:
CREATE [OR REPLACE ] TRIGGER trigger_name {BEFORE | AFTER |
INSTEAD OF }{INSERT [OR] | UPDATE [OR] | DELETE}
[OF col_name]
ON table_name [
REFERENCING OLD AS.NEW AS n][FOR EACH ROW]
WHEN (condition)
DECLARE
Declaration-statements
BEGIN
Executable-statements
EXCEPTION
Exception-handling-statements
END;
Where,
 CREATE [OR REPLACE] TRIGGER trigger_name − Creates or replaces an existing
trigger with the trigger_name.
 {BEFORE | AFTER | INSTEAD OF} − This specifies when the trigger will be
executed. The INSTEAD OF clause is used for creating trigger on a view.
 {INSERT [OR] | UPDATE [OR] | DELETE} − This specifies the DML operation. •
 [OF col_name] − This specifies the column name that will be updated.
 [ON table_name] − This specifies the name of the table associated with the trigger.
 [REFERENCING OLD AS o NEW AS n] − This allows you to refer new and old
values for various DML statements, such as INSERT, UPDATE, and DELETE.
 [FOR EACH ROW] − This specifies a row-level trigger, i.e., the trigger will be
executed for each row being affected. Otherwise the trigger will execute just once
when the SQL statement is executed, which is called a table level trigger.
 WHEN (condition) − This provides a condition for rows for which the trigger would
fire. This clause is valid only for row-level triggers
PROGRAM
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
Procedure created
1. PROCEDURE
QUESTION
1. Write a PL/SQL program to generate Fibonacci series using procedure
ALGORITHM
Step 1: Start
Step 2 : read the limit
Step 3: Call procedure, FIB(number)
Step 4: Stop
FIB(number)
Step 1: Start
Step 2: Initialize A and VAL as zero
Step 3: Display the first two terms of series
Step 4: Repeat until VAL!= N-2
4:1 Calculate C=A+B
4:2 Display C
4:3 Perform swapping
4:4 Set Val as Val+1
Step 5: Stop 
