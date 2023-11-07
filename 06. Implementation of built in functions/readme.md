# 06. Implementation of built-in functions

## AIM

To implement built-in functions in RDBMS

## THEORY

### RDBMS Built-in Functions
There are two types of functions:
1. **Single Row Functions:** Single row or Scalar functions return a value for every row that is processed in a query.
2. **Group Functions:** These functions group the rows of data based on the values returned by the query. This is discussed in SQL GROUP Functions. The group functions are used to calculate aggregate values like total or average, which return just one total or one average value after processing a group of rows.

There are four types of single-row functions. They are:
1. **Numeric Functions:** These are functions that accept numeric input and return numeric values.
2. **Character or Text Functions:** These are functions that accept character input and can return both character and number values.
3. **Date Functions:** These are functions that take values that are of datatype DATE as input and return values of datatype DATE, except for the MONTHS_BETWEEN function, which returns a number.
4. **Conversion Functions:** These are functions that help us to convert a value in one form to another form. For Example: a null value into an actual value, or a value from one datatype to another datatype like NVL, TO_CHAR, TO_NUMBER, TO_DATE etc.

### String Function

- **ASCII**: Returns the ASCII value for the specific character
- **CHAR LENGTH**: Returns the length of a string (in characters)
- **CHARACTER LENGTH**: Returns the length of a string (in characters)
- **CONCAT**: Adds two or more expressions together
- **LCASE**: Converts a string to lower-case
- **LEFT**: Extracts a number of characters from a string (starting from left)
- **LENGTH**: Returns the length of a string (in bytes)
- **LOCATE**: Returns the position of the first occurrence of a substring in a string
- **LTRIM**: Removes leading spaces from a string
- **POSITION**: Returns the position of the first occurrence of a substring in a string
- **REPEAT**: Repeats a string as many times as specified
- **REPLACE**: Replaces all occurrences of a substring within a string, with a new substring
- **REVERSE**: Reverses a string and returns the result
- **RIGHT**: Extracts a number of characters from a string (starting from right)
- **RTRIM**: Removes trailing spaces from a string
- **STRCMP**: Compares two strings
- **SUBSTR**: Extracts a substring from a string (starting at any position)
- **SUBSTRING**: Extracts a substring from a string (starting at any position)

### Numeric Function

- **ABS**: Returns the absolute value of a number
- **CEIL**: Returns the smallest integer value that is greater than or equal to a number
- **FLOOR**: Returns the largest integer value that is less than or equal to a number
- **GREATEST**: Returns the greatest value of the list of arguments
- **LEAST**: Returns the smallest value of the list of arguments
- **MOD**: Returns the remainder of a number divided by another number
- **ROUND**: Rounds a number to a specified number of decimal places
- **SQRT**: Returns the square root of a number
- **SUM**: Calculates the sum of a set of values
- **TRUNCATE**: Truncates a number to the specified number of decimal places

### Data Functions

- **ADDDATE**: Adds a time/date interval to a date and then returns the date
- **ADDTIME**: Adds a time interval to a time/datetime and then returns the time/datetime
- **CURDATE**: Returns the current date
- **CURRENT DATE**: Returns the current date
- **CURRENT TIME**: Returns the current time
- **DATE**: Extracts the date part from a datetime expression
- **DAY**: Returns the day of the month for a given date
- **DAYNAME**: Returns the weekday name for a given date
- **DAYOFMONTH**: Returns the day of the month for a given date
- **HOUR**: Returns the hour part for a given date
- **MINUTE**: Returns the minute part of a time/datetime
- **MONTH**: Returns the month part for a given date
- **SECOND**: Returns the seconds part of a time/datetime

## Advanced Functions

- **CURRENT USER**: Returns the name and hostname for the MySQL account that the server used to authenticate the current client
- **SESSION USER**: Returns the current MySQL user name and hostname
- **SYSTEM USER**: Returns the current MySQL user name and hostname
- **USER**: Returns the current MySQL user name and hostname
- **VERSION**: Returns the current version of the MySQL database

### Result

Queries to implement built-in functions in RDBMS have been executed successfully and output obtained

### OUTPUT

#### String Functions
```
mysql> select ascii ('a');
+-------------+
| ascii ('a') |
+-------------+
|          97 |
+-------------+
1 row in set (0.00 sec)
```
```
mysql> select char_length ('My name is sreeram');
+------------------------------------+
| char_length ('My name is sreeram') |
+------------------------------------+
|                                 18 |
+------------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select concat ('This line',' is joined');
+-----------------------------------+
| concat ('This line',' is joined') |
+-----------------------------------+
| This line is joined               |
+-----------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select lcase ('THIS LINE IS NOW LOWERCASE');
+--------------------------------------+
| lcase ('THIS LINE IS NOW LOWERCASE') |
+--------------------------------------+
| this line is now lowercase           |
+--------------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select left ('This line will be trimmed',4);
+--------------------------------------+
| left ('This line will be trimmed',4) |
+--------------------------------------+
| This                                 |
+--------------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select length ('The length of the line is something');
+------------------------------------------------+
| length ('The length of the line is something') |
+------------------------------------------------+
|                                             35 |
+------------------------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select locate ('name','Searched name from this line');
+------------------------------------------------+
| locate ('name','Searched name from this line') |
+------------------------------------------------+
|                                             10 |
+------------------------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select ltrim ('            This is the leading spaces');
+--------------------------------------------------+
| ltrim ('            This is the leading spaces') |
+--------------------------------------------------+
| This is the leading spaces                       |
+--------------------------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select position("a"in"Searched_from_this_line");
+------------------------------------------+
| position("a"in"Searched_from_this_line") |
+------------------------------------------+
|                                        3 |
+------------------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select repeat ("This line will be repeated twice. ",2);
+----------------------------------------------------------------------+
| repeat ("This line will be repeated twice. ",2)                      |
+----------------------------------------------------------------------+
| This line will be repeated twice. This line will be repeated twice.  |
+----------------------------------------------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select replace ('This is the whole string','whole','new');
+----------------------------------------------------+
| replace ('This is the whole string','whole','new') |
+----------------------------------------------------+
| This is the new string                             |
+----------------------------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select reverse ('Reversed');
+----------------------+
| reverse ('Reversed') |
+----------------------+
| desreveR             |
+----------------------+
1 row in set (0.00 sec)
```
```
mysql> select right ('This line will be trimmed',4);
+---------------------------------------+
| right ('This line will be trimmed',4) |
+---------------------------------------+
| mmed                                  |
+---------------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select rtrim ('This is the leading spaces         ');
+-----------------------------------------------+
| rtrim ('This is the leading spaces         ') |
+-----------------------------------------------+
| This is the leading spaces                    |
+-----------------------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select strcmp ('same','same');
+------------------------+
| strcmp ('same','same') |
+------------------------+
|                      0 |
+------------------------+
1 row in set (0.01 sec)
```
```
mysql> select strcmp ('same','not');
+-----------------------+
| strcmp ('same','not') |
+-----------------------+
|                     1 |
+-----------------------+
1 row in set (0.00 sec)
```
```
mysql> select substring("This line is extracted",6,4);
+-----------------------------------------+
| substring("This line is extracted",6,4) |
+-----------------------------------------+
| line                                    |
+-----------------------------------------+
1 row in set (0.00 sec)
```

#### Numeric Functions
```
mysql> select abs (-100);
+------------+
| abs (-100) |
+------------+
|        100 |
+------------+
1 row in set (0.00 sec)
```
```
mysql> select ceil (8.5);
+------------+
| ceil (8.5) |
+------------+
|          9 |
+------------+
1 row in set (0.00 sec)
```
```
mysql> select floor (8.5);
+-------------+
| floor (8.5) |
+-------------+
|           8 |
+-------------+
1 row in set (0.00 sec)
```
```
mysql> select greatest (1,2,34,5,6,7,8,9,12,3.4);
+------------------------------------+
| greatest (1,2,34,5,6,7,8,9,12,3.4) |
+------------------------------------+
|                               34.0 |
+------------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select least (1,2,34,5,6,7,8,9,12,3.4);
+---------------------------------+
| least (1,2,34,5,6,7,8,9,12,3.4) |
+---------------------------------+
|                             1.0 |
+---------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select abs (-100);
+------------+
| abs (-100) |
+------------+
|        100 |
+------------+
1 row in set (0.00 sec)
```
```
mysql> select ceil (8.5);
+------------+
| ceil (8.5) |
+------------+
|          9 |
+------------+
1 row in set (0.00 sec)
```
```
mysql> select floor (8.5);
+-------------+
| floor (8.5) |
+-------------+
|           8 |
+-------------+
1 row in set (0.00 sec)
```
```
mysql> select greatest (1,2,34,5,6,7,8,9,12,3.4);
+------------------------------------+
| greatest (1,2,34,5,6,7,8,9,12,3.4) |
+------------------------------------+
|                               34.0 |
+------------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select least (1,2,34,5,6,7,8,9,12,3.4);
+---------------------------------+
| least (1,2,34,5,6,7,8,9,12,3.4) |
+---------------------------------+
|                             1.0 |
+---------------------------------+
1 row in set (0.00 sec)
```
> This section contains some aggregate functions that will actually be covered in next experiment. Since this experiment is about built-in functions, they may be also used here as well.

> **Also, aggregate functions used here requires a table to work on.**
```
mysql> create table test (
    -> name varchar(255),
    -> rollno int primary key,
    -> mark int not null
    -> ); 
Query OK, 0 rows affected (0.25 sec)

mysql> show tables;
+-------------------+
| Tables_in_sreeram |
+-------------------+
| student           |
| test              |
+-------------------+
2 rows in set (0.00 sec)

mysql> desc test;
+--------+--------------+------+-----+---------+-------+
| Field  | Type         | Null | Key | Default | Extra |
+--------+--------------+------+-----+---------+-------+
| name   | varchar(255) | YES  |     | NULL    |       |
| rollno | int(11)      | NO   | PRI | NULL    |       |
| mark   | int(11)      | NO   |     | NULL    |       |
+--------+--------------+------+-----+---------+-------+
3 rows in set (0.01 sec)

mysql> insert into test values('name_01',01,40),
    -> ('name_02',02,45),
    -> ('name_03',03,43),
    -> ('name_04',04,40),
    -> ('name_05',05,48)
    -> ;
Query OK, 5 rows affected (0.03 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> select * from test;
+---------+--------+------+
| name    | rollno | mark |
+---------+--------+------+
| name_01 |      1 |   40 |
| name_02 |      2 |   45 |
| name_03 |      3 |   43 |
| name_04 |      4 |   40 |
| name_05 |      5 |   48 |
+---------+--------+------+
5 rows in set (0.00 sec)
```
```
mysql> select min(mark) from test;
+-----------+
| min(mark) |
+-----------+
|        40 |
+-----------+
1 row in set (0.00 sec)
```
```
mysql> select max(mark) from test;
+-----------+
| max(mark) |
+-----------+
|        48 |
+-----------+
1 row in set (0.00 sec)
```
```
mysql> select round (15.1234567);
+--------------------+
| round (15.1234567) |
+--------------------+
|                 15 |
+--------------------+
1 row in set (0.00 sec)
```
```
mysql> select round (15.9234567);
+--------------------+
| round (15.9234567) |
+--------------------+
|                 16 |
+--------------------+
1 row in set (0.00 sec)
```
```
mysql> select sqrt (64);
+-----------+
| sqrt (64) |
+-----------+
|         8 |
+-----------+
1 row in set (0.01 sec)
```
```
mysql> select sum(mark) from test;
+-----------+
| sum(mark) |
+-----------+
|       216 |
+-----------+
1 row in set (0.00 sec)
```
```
mysql> select truncate (12.642734786,2);
+---------------------------+
| truncate (12.642734786,2) |
+---------------------------+
|                     12.64 |
+---------------------------+
1 row in set (0.00 sec)
```

#### Date Functions
```
mysql> select adddate('2002-12-03',10);
+--------------------------+
| adddate('2002-12-03',10) |
+--------------------------+
| 2002-12-13               |
+--------------------------+
1 row in set (0.00 sec)
```
```
mysql> select addtime('08:06:56',10000);
+---------------------------+
| addtime('08:06:56',10000) |
+---------------------------+
| 09:06:56                  |
+---------------------------+
1 row in set (0.00 sec)
```
```
mysql> select current_date();
+----------------+
| current_date() |
+----------------+
| 2023-08-24     |
+----------------+
1 row in set (0.00 sec)
```
```
mysql> select current_time();
+----------------+
| current_time() |
+----------------+
| 11:23:29       |
+----------------+
1 row in set (0.00 sec)
```
```
mysql> select date ('2023-10-13 05:10:59');
+------------------------------+
| date ('2023-10-13 05:10:59') |
+------------------------------+
| 2023-10-13                   |
+------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select time ('2023-10-13 05:10:59');
+------------------------------+
| time ('2023-10-13 05:10:59') |
+------------------------------+
| 05:10:59                     |
+------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select day ('2023-10-13 05:10:59');
+-----------------------------+
| day ('2023-10-13 05:10:59') |
+-----------------------------+
|                          13 |
+-----------------------------+
1 row in set (0.00 sec)
```
```
mysql> select dayname ('2023-10-13 05:10:59');
+---------------------------------+
| dayname ('2023-10-13 05:10:59') |
+---------------------------------+
| Friday                          |
+---------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select dayofmonth ('2023-10-13 05:10:59');
+------------------------------------+
| dayofmonth ('2023-10-13 05:10:59') |
+------------------------------------+
|                                 13 |
+------------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select hour ('2023-10-13 05:10:59');
+------------------------------+
| hour ('2023-10-13 05:10:59') |
+------------------------------+
|                            5 |
+------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select minute ('2023-10-13 05:10:59');
+--------------------------------+
| minute ('2023-10-13 05:10:59') |
+--------------------------------+
|                             10 |
+--------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select second ('2023-10-13 05:10:59');
+--------------------------------+
| second ('2023-10-13 05:10:59') |
+--------------------------------+
|                             59 |
+--------------------------------+
1 row in set (0.00 sec)
```
```
mysql> select month ('2023-10-13 05:10:59');
+-------------------------------+
| month ('2023-10-13 05:10:59') |
+-------------------------------+
|                            10 |
+-------------------------------+
1 row in set (0.00 sec)
```

#### Advanced Functions
```
mysql> select version();
+-------------------------+
| version()               |
+-------------------------+
| 5.7.33-0ubuntu0.16.04.1 |
+-------------------------+
1 row in set (0.00 sec)
```
```
mysql> select current_user();
+----------------+
| current_user() |
+----------------+
| root@localhost |
+----------------+
1 row in set (0.00 sec)
```
```
mysql> select session_user();
+----------------+
| session_user() |
+----------------+
| root@localhost |
+----------------+
1 row in set (0.00 sec)
```
```
mysql> select user();
+----------------+
| user()         |
+----------------+
| root@localhost |
+----------------+
1 row in set (0.00 sec)
```
