# 13. Implementation of various control structures like, if then, then else, if then else, if while

## AIM

To Implement various control structures like IF-THEN, IF-THEN-ELSE, IF-THEN ELSIF, CASE, and WHILE using PL/SQL.

## Theory

### Introduction to PL/SQL

PL/SQL is a block-structured language used in Oracle, tightly integrated with the database. It supports multiple nested blocks and extends SQL with additional programming constraints.

### Features of PL/SQL

PL/SQL features include tight SQL integration, robust error checking, diverse data types, versatile programming structures, support for structured and object-oriented programming, and web application development.

### Advantages of PL/SQL

  - Strong SQL integration
  - Reduced network traffic
  - High programmer productivity
  - Time savings with features like exception handling and encapsulation
  - Portability and high security
  - Access to predefined SQL packages
  - Support for object-oriented programming
  - Facilitates web application development

### Basic Syntax

- PL/SQL Basic Syntax:
  1. **Declarations**: Start with DECLARE, defining variables, cursors, subprograms, etc.
  2. **Executable Commands**: Enclosed between BEGIN and END, holds executable PL/SQL statements.
  3. **Exception Handling**: Starts with EXCEPTION, and contains error-handling exceptions.

- PL/SQL Statement End: Each ends with a semicolon (;).
- Nesting: Blocks can nest using BEGIN and END.
- Basic Block Structure:
  ```plsql
  DECLARE
  <declaration section>
  BEGIN
  <executable command(s)>
  EXCEPTION
  <exception handling>
  END;
  ```

### PL/SQL Comments

- Single-line (--) and multi-line (/* */) comments to explain code.

### PL/SQL Identifiers

- Constants, variables, exceptions, procedures, and cursors.
- Letters, numerals, $, _, and #, up to 30 characters.
- Not case-sensitive, except for reserved keywords.

---

### Implementation of various control structures using PL/SQL
 
#### Decision-Making Statements

- Specify condition(s) for evaluation.
- Execute statement(s) if true.
- Optionally, execute other statement(s) if false.

##### 1. IF - THEN statement

- Associates condition with statements between THEN and END IF.
- Executes statements if the condition is true.
- Does nothing if the condition is false or NULL.

##### 2. IF-THEN-ELSE statement

  - Adds ELSE with an alternative statement sequence.
  - Executes the alternative sequence if the condition is false or NULL.
  - Ensures execution of either statement sequence.

##### 3. IF-THEN-ELSIF statement

- It allows you to choose between several alternatives.

##### 4. Case Statement

- Selects a statement sequence based on a selector.
- Uses the value of the selector to determine the sequence.
- Employs an expression to choose from multiple alternatives.

##### 5. Searched CASE statement

- Lacks a selector.
- WHEN clauses have search conditions producing Boolean values.

##### 6. Nested IF-THEN-ELSE

- Place one inside another for complex conditions.
- Enhances decision-making flexibility.

#### Looping Statements

- Enables repeated execution of a statement or group.
- Supports efficient handling of repetitive tasks.

##### 1. PL/SQL Basic LOOP

- Statements enclosed between LOOP and END LOOP.
- Executed iteratively; control returns to the loop's top at each iteration.

##### 2. PL/SQL WHILE LOOP

- Repeats statements while a specified condition is true.
- Tests condition before executing the loop body.

##### 3. PL/SQL FOR LOOP

- Executes statements iteratively.
- Simplifies loop variable management.

##### 4. Nested loops in PL/SQL

- Employ one or more loops inside another loop.
- Enhances control flow for complex scenarios.

---

# How to write the following sections in fair record?

- Question(s) on right side
- Algorithm on the right side
- Program/Output as it is printed, on the left side.
- **PROGRAM NEED NOT BE WRITTEN ON FAIR RECORD**

- Write the following as sections on each page (total of 7 programs)

---

### QUESTION

**1.** Write a PL/SQL program to find the sum of two numbers

### ALGORITHM

1. Start
2. Enter number A
3. Enter number B
4. Compute SUM1 = A+B
5. Display SUM1
6. End


### Program

```sql
SQL> SET SERVEROUTPUT ON
SQL> DECLARE
2 A NUMBER(4):=&NUM1;
3 B NUMBER(4):=&NUM2;
4 SUM1 NUMBER(8):=0;
5 BEGIN
6 SUM1:=A+B;
7 DBMS_OUTPUT.PUT_LINE('THE SUM OF TWO NUMBER IS:'||SUM1);
8 END;
9 /
```

### Output

```
Enter value for num1: 28
old 2: A NUMBER(4):=&NUM1;
new 2: A NUMBER(4):=28;
Enter value for num2: 22
old 3: B NUMBER(4):=&NUM2;
new 3: B NUMBER(4):=22;
THE SUM OF TWO NUMBER IS:50
PL/SQL procedure successfully completed.
```

---

---

## IF-THEN

### QUESTION

**2.** Write a PL/SQL program to display whether the given number is zero.

### ALGORITHM

1. Start
2. Set NUM1=0
3. Check whether NUM1 is equal to 0
4. Display the message the number is zero
5. Display the end of the program
6. End


### Program (IF-THEN)

```sql
SQL> SET SERVEROUTPUT ON
SQL> DECLARE
2 NUM1 NUMBER:=0;
3 BEGIN
4 IF NUM1 = 0 THEN
5 DBMS_OUTPUT.PUT_LINE('THE NUMBER IS ZERO');
6 END IF;
7 DBMS_OUTPUT.PUT_LINE('END OF PROGRAM');
8 END;
9 /
```

### Output

```
THE NUMBER IS ZERO
END OF PROGRAM
PL/SQL procedure successfully completed.
```
---

## IF-THEN-ELSE

### QUESTION

**3.** Write a PL/SQL program to find whether a given number is odd or even.

### ALGORITHM

1. Start
2. Enter the number to check
3. If the number is divisible by 2, then the number is Even
4. Else, the number is odd
5. Print the output
6. Stop

### Program

```sql
SQL> SET SERVEROUTPUT ON
SQL> DECLARE
2 A NUMBER(4):=&NUM;
3 BEGIN
4 IF MOD(A,2)=0 THEN
5 DBMS_OUTPUT.PUT_LINE('THE NUMBER IS EVEN');
6 ELSE
7 DBMS_OUTPUT.PUT_LINE('THE NUMBER IS ODD');
8 END IF;
9 END;
10 /
```

### Output

```
Enter value for num: 2
old 2: A NUMBER(4):=&NUM;
new 2: A NUMBER(4):=2;
THE NUMBER IS EVEN
PL/SQL procedure successfully completed.
```
```
Enter value for num: 7
old 2: A NUMBER(4):=&NUM;
new 2: A NUMBER(4):=7;
THE NUMBER IS ODD
PL/SQL procedure successfully completed.
```

---

## IF-THEN-ELSEIF

### QUESTION

**4.** Write a PL/SQL program to display the grade list of a student.

### ALGORITHM

1. Start
2. Enter three marks
3. Calculate total mark and percentage
4. Check if the percentage is greater than 90, then display grade as A grade
5. Check if the percentage is greater than 80 and less than 90, then display grade as B
6. Otherwise, display grade as C grade
7. Stop

### Program

```sql
SQL> SET SERVEROUTPUT ON
SQL>  DECLARE
  2   SUB1 NUMBER(4):=&NUM1;
  3   SUB2 NUMBER(4):=&NUM2;
  4   SUB3 NUMBER(4):=&NUM3;
  5   TOTAL NUMBER(4):=0;
  6   PER DECIMAL(18,2):=0;
  7   BEGIN
  8   TOTAL:=SUB1+SUB2+SUB3;
  9   DBMS_OUTPUT.PUT_LINE('TOTAL='||TOTAL);
 10   PER:=(TOTAL/300)*100;
 11   DBMS_OUTPUT.PUT_LINE('PERCENTAGE='||PER);
 12   IF PER>=90 THEN
 13   DBMS_OUTPUT.PUT_LINE('GRADE:A');
 14   ELSIF PER>=80 AND PER<90 THEN
 15   DBMS_OUTPUT.PUT_LINE('GRADE:B');
 16   ELSE
 17   DBMS_OUTPUT.PUT_LINE('GRADE:C');
 18   END IF;
 19   END;
 20   /
```

### output

```sql
Enter value for num1: 80
old   2:  SUB1 NUMBER(4):=&NUM1;
new   2:  SUB1 NUMBER(4):=80;
Enter value for num2: 60
old   3:  SUB2 NUMBER(4):=&NUM2;
new   3:  SUB2 NUMBER(4):=60;
Enter value for num3: 40
old   4:  SUB3 NUMBER(4):=&NUM3;
new   4:  SUB3 NUMBER(4):=40;
TOTAL=180
PERCENTAGE=60
GRADE:C

PL/SQL procedure successfully completed.
```

---


## CASE

### QUESTION

**5.** Write a PL/SQL program to find the area of geometric shapes using CASE.

### ALGORITHM

1. Start
2. Take input for choice and then for area variables from the user
3. Case 1: Circle: 3.14 * radius * radius Case 2: Triangle: 0.5 * base * height;
4. Display output according to the case
5. Stop

### Program

```sql
SQL> SET SERVEROUTPUT ON
SQL> DECLARE
2 CHOICE NUMBER;
3 RADIUS NUMBER;
4 AREA NUMBER;
5 BASE NUMBER;
6 HEIGHT NUMBER;
7 BEGIN
8 DBMS_OUTPUT.PUT_LINE('1.AREA OF CIRCLE');
9 DBMS_OUTPUT.PUT_LINE('2.AREA OF TRIANGLE');
10 CHOICE:=&CHOICE;
11 CASE CHOICE
12 WHEN 1 THEN
13 RADIUS:=&RADIUS;
14 AREA:=RADIUS*RADIUS*3.14;
15 DBMS_OUTPUT.PUT_LINE('AREA OF CIRCLE IS:'||AREA);
16 WHEN 2 THEN
17 BASE:=&BASE;
18 HEIGHT:=&HEIGHT;
19 AREA:=0.5*BASE*HEIGHT;
20 DBMS_OUTPUT.PUT_LINE('AREA OF TRIANGLE IS :'||AREA);
21 ELSE
22 DBMS_OUTPUT.PUT_LINE('INVALID CHOICE');
23 END CASE;
24 END;
25 /
```

### Output

```
Enter value for choice: 1
old 10: CHOICE:=&CHOICE;
new 10: CHOICE:=1;
Enter value for radius: 2
old 13: RADIUS:=&RADIUS;
new 13: RADIUS:=2;
Enter value for base: 3
old 17: BASE:=&BASE;
new 17: BASE:=3;
Enter value for height: 4
old 18: HEIGHT:=&HEIGHT;
new 18: HEIGHT:=4;
1.AREA OF CIRCLE
2.AREA OF TRIANGLE
AREA OF CIRCLE IS:12.56
PL/SQL procedure successfully completed.
```

---

## WHILE

### QUESTION

**6.** Write a PL/SQL program to check whether the number is an Armstrong number or not.

### ALGORITHM

1. Start
2. Read a number from the user
3. Initialize variables sum1 and D to zero
4. Set X = A
5. Repeat until A > 0
   5.1. Calculate D = MOD(A, 10)
   5.2. Calculate the sum, sum1 + (D * D * D)
   5.3. Set A as A / 10
6. Check whether sum1 is equal to X
   6.1. If true, display the number is Armstrong
   6.2. If false, display the number is not an Armstrong
7. Stop

### Program

```sql
SQL> SET SERVEROUTPUT ON
SQL> DECLARE
2 A NUMBER(5):=&NUM1;
3 D NUMBER(5):=0;
4 X NUMBER(5);
5 SUM1 NUMBER(10):=0;
6 BEGIN
7 X:=A;
8 WHILE A>0
9 LOOP
10 D:=MOD(A,10);
11 SUM1:=SUM1+(D*D*D);
12 A:=FLOOR(A/10);
13 END LOOP;
14 IF SUM1=X THEN
15 DBMS_OUTPUT.PUT_LINE('THE NUMBER IS ARMSTRONG');
16 ELSE
17 DBMS_OUTPUT.PUT_LINE('THE NUMBER IS NOT ARMSRONG');
18 END IF;
19 END;
20 /
```

### Output

```
Enter value for num1: 153
old 2: A NUMBER(5):=&NUM1;
new 2: A NUMBER(5):=153;
THE NUMBER IS ARMSTRONG
PL/SQL procedure successfully completed.
```
```
Enter value for num1: 231
old 2: A NUMBER(5):=&NUM1;
new 2: A NUMBER(5):=231;
THE NUMBER IS NOT ARMSTRONG
PL/SQL procedure successfully completed.
```

---

## FOR LOOP

### QUESTION

7. Write a PL/SQL program to display the prime numbers up to 'n'.

### ALGORITHM

1. Start
2. Read the limit
3. Initialize variables
4. Repeat loop for B = 1 to limit
   4.1. Repeat loop for I = 1 to limit
        a. Check if MOD(B, I) is equal to 0, then set C as C + 1
   4.2. Check if C is equal to 2, then display prime numbers
5. Stop

### Program

```sql
SQL> SET SERVEROUTPUT ON
SQL> DECLARE
  2   A NUMBER(4):=&LIMIT;
  3   B NUMBER(4):=1;
  4   C NUMBER:=0;
  5   BEGIN
  6   DBMS_OUTPUT.PUT_LINE('THE PRIME NUMBERS ARE:');
  7   FOR B IN 1 ..A
  8   LOOP
  9   C:=0;
 10   FOR I IN 1 ..A
 11  LOOP
 12   IF MOD(B,I)=0 THEN
 13   C:=C+1;
 14   END IF;
 15   END LOOP;
 16   IF C=2 THEN
 17   DBMS_OUTPUT.PUT_LINE(B);
 18   END IF;
 19   END LOOP;
 20  END;
 21   /
```

### Output

```sql
Enter value for limit: 5
old   2:  A NUMBER(4):=&LIMIT;
new   2:  A NUMBER(4):=5;
THE PRIME NUMBERS ARE:
2
3
5

PL/SQL procedure successfully completed.
```
