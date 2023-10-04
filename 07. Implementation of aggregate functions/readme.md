## 07. Implementation of aggregate functions.

> Refer [this PDF](pdfs/exp7.pdf) from my repository for any assistance. This PDF may contain additional information that may not be mentioned here.

### Example

In this experiment, create a table of your liking or use any existing table. Then using the table use the aggregate functions such as *sum*,*min*,*max*,*avg* and *count*.

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
    -> ('name_05',05,48);
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
mysql> select sum(mark) from test;
+-----------+
| sum(mark) |
+-----------+
|       216 |
+-----------+
1 row in set (0.00 sec)
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
mysql> select avg(mark) from test;
+-----------+
| avg(mark) |
+-----------+
|   43.2000 |
+-----------+
1 row in set (0.00 sec)
```
```
mysql> select count(mark) from test;
+-------------+
| count(mark) |
+-------------+
|           5 |
+-------------+
1 row in set (0.00 sec)
```
### Practise

Now, that you have a familiarity with using built-in functions, including the aggregating function, create the tables with the following fields:

> Question

`Faculty (FacultyCode, FacultyName)`

`Subject (SubjectCode, SubjectName, MaxMark, FacultyCode)`

`Student (StudentCode, StudentName, DOB, StudentsBranch(CS/EC/EE/ME), AdmissionDate)`

`M_Mark (StudentCode, SubjectCode, Mark)`

Do the following queries:

1. Display the number of faculties.
2. Display the total mark for each student.
3. Display the subject, average mark for each subject.
4. Display the name of subjects for which at least one student got below 40%.
5. Display the name, subject and percentage of mark who got below 40%.
6. Display the faculties and allotted subjects for each faculty.
7. Display the name of faculties who take more than one subject.
8. Display name, subject, mark, % of mark in ascending order of mark.

> Answer

#### Creating Tables

```
CREATE TABLE Faculty (
    FacultyCode INT PRIMARY KEY,
    FacultyName VARCHAR(255)
);
```
```
CREATE TABLE Subject (
    SubjectCode INT PRIMARY KEY,
    SubjectName VARCHAR(255),
    MaxMark INT,
    FacultyCode INT,
    FOREIGN KEY (FacultyCode) REFERENCES Faculty(FacultyCode)
);
```
```
CREATE TABLE Student (
    StudentCode INT PRIMARY KEY,
    StudentName VARCHAR(255),
    DOB DATE,
    StudentsBranch ENUM('CS', 'EC', 'EE', 'ME'),
    AdmissionDate DATE
);
```
```
CREATE TABLE M_Mark (
    StudentCode INT,
    SubjectCode INT,
    Mark INT,
    FOREIGN KEY (StudentCode) REFERENCES Student(StudentCode),
    FOREIGN KEY (SubjectCode) REFERENCES Subject(SubjectCode)
);
```

#### Table contents

> I had purposefully skipped the portion to insert entities into the table as you are already familiar with the same. So please go through the contents that are already present in the table I created for you.


> **"desc table_name" need not be written down, only write down "select * from table_name"**

##### **WHOLE_TABLE**

> Only refer

```
mysql> show tables;
+-----------------+
| Tables_in_exp07 |
+-----------------+
| faculty         |
| m_mark          |
| student         |
| subject         |
+-----------------+
4 rows in set (0.00 sec)
```

##### faculty

> *Only Refer*

```
mysql> desc faculty;
+-------------+--------------+------+-----+---------+-------+
| Field       | Type         | Null | Key | Default | Extra |
+-------------+--------------+------+-----+---------+-------+
| FacultyCode | int          | NO   | PRI | NULL    |       |
| FacultyName | varchar(255) | YES  |     | NULL    |       |
+-------------+--------------+------+-----+---------+-------+
2 rows in set (0.00 sec)
```

> *Write down the following*

```
mysql> select * from faculty;
+-------------+-------------+
| FacultyCode | FacultyName |
+-------------+-------------+
|           1 | faculty001  |
|           2 | faculty002  |
|           3 | faculty003  |
|           4 | faculty004  |
|           5 | faculty005  |
+-------------+-------------+
5 rows in set (0.00 sec)
```

##### subject

> *Only Refer*

```
mysql> desc subject;
+-------------+--------------+------+-----+---------+-------+
| Field       | Type         | Null | Key | Default | Extra |
+-------------+--------------+------+-----+---------+-------+
| SubjectCode | int          | NO   | PRI | NULL    |       |
| SubjectName | varchar(255) | YES  |     | NULL    |       |
| MaxMark     | int          | YES  |     | NULL    |       |
| FacultyCode | int          | YES  | MUL | NULL    |       |
+-------------+--------------+------+-----+---------+-------+
4 rows in set (0.00 sec)
```

> *Write down the following*

```
mysql> select * from subject;
+-------------+-------------+---------+-------------+
| SubjectCode | SubjectName | MaxMark | FacultyCode |
+-------------+-------------+---------+-------------+
|         101 | SUB101      |     100 |           1 |
|         102 | SUB102      |     100 |           2 |
|         103 | SUB103      |     100 |           3 |
|         104 | SUB104      |     100 |           4 |
|         105 | SUB105      |     100 |           5 |
|         106 | SUB106      |     100 |           1 |
|         107 | SUB107      |     100 |           2 |
+-------------+-------------+---------+-------------+
7 rows in set (0.00 sec)
```

##### student

> *Only Refer*

```
mysql> desc student;
+----------------+---------------------------+------+-----+---------+-------+
| Field          | Type                      | Null | Key | Default | Extra |
+----------------+---------------------------+------+-----+---------+-------+
| StudentCode    | int                       | NO   | PRI | NULL    |       |
| StudentName    | varchar(255)              | YES  |     | NULL    |       |
| DOB            | date                      | YES  |     | NULL    |       |
| StudentsBranch | enum('CS','EC','EE','ME') | YES  |     | NULL    |       |
| AdmissionDate  | date                      | YES  |     | NULL    |       |
+----------------+---------------------------+------+-----+---------+-------+
5 rows in set (0.00 sec)
```

> *Write down the following*

```
mysql> select * from student;
+-------------+-------------+------------+----------------+---------------+
| StudentCode | StudentName | DOB        | StudentsBranch | AdmissionDate |
+-------------+-------------+------------+----------------+---------------+
|        1001 | STUD1001    | 2000-01-01 | CS             | 2020-06-01    |
|        1002 | STUD1002    | 2000-02-02 | EC             | 2020-06-02    |
|        1003 | STUD1003    | 2000-03-03 | EE             | 2020-06-03    |
|        1004 | STUD1004    | 2000-04-04 | ME             | 2020-06-04    |
|        1005 | STUD1005    | 2000-05-05 | CS             | 2020-06-05    |
+-------------+-------------+------------+----------------+---------------+
5 rows in set (0.00 sec)
```

##### m_mark

> Note: The below marks need not be assigned for every student concerning the subject. As there are 7 subjects and 5 students in total, there will be 35 entries in total. This will be reduced while writing the fair record. Right now, I'm stressed and feeling sleepy, please adjust to what you have right now. If you are planning to reduce the entries, try to answer the corresponding question (8) with the reduced input.

> *Only Refer*

```
mysql> desc m_mark;
+-------------+------+------+-----+---------+-------+
| Field       | Type | Null | Key | Default | Extra |
+-------------+------+------+-----+---------+-------+
| StudentCode | int  | YES  | MUL | NULL    |       |
| SubjectCode | int  | YES  | MUL | NULL    |       |
| Mark        | int  | YES  |     | NULL    |       |
+-------------+------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

> *Write down the following with respect to my previous suggestion*

```
mysql> select * from m_mark;
+-------------+-------------+------+
| StudentCode | SubjectCode | Mark |
+-------------+-------------+------+
|        1001 |         101 |   95 |
|        1001 |         102 |   96 |
|        1001 |         103 |   94 |
|        1001 |         104 |   92 |
|        1001 |         105 |   98 |
|        1002 |         101 |   83 |
|        1002 |         102 |   90 |
|        1002 |         103 |   93 |
|        1002 |         104 |   80 |
|        1002 |         105 |   89 |
|        1003 |         101 |   39 |
|        1003 |         102 |   48 |
|        1003 |         103 |   56 |
|        1003 |         104 |   33 |
|        1003 |         105 |   50 |
|        1004 |         101 |   66 |
|        1004 |         102 |   45 |
|        1004 |         103 |   36 |
|        1004 |         105 |   30 |
|        1005 |         101 |   54 |
|        1005 |         102 |   30 |
|        1005 |         103 |   70 |
|        1005 |         104 |   81 |
|        1005 |         105 |   88 |
|        1004 |         104 |   44 |
|        1001 |         106 |   98 |
|        1001 |         107 |   91 |
|        1002 |         106 |   82 |
|        1002 |         107 |   85 |
|        1003 |         106 |   73 |
|        1003 |         107 |   79 |
|        1004 |         106 |   45 |
|        1004 |         107 |   55 |
|        1005 |         106 |   52 |
|        1005 |         107 |   67 |
+-------------+-------------+------+
35 rows in set (0.00 sec)
```

#### Performing Queries

1. Display the number of faculties.

```
mysql> SELECT COUNT(*) FROM Faculty;
+----------+
| COUNT(*) |
+----------+
|        5 |
+----------+
1 row in set (0.00 sec)
```

2. Display the total mark for each student.
```
mysql> SELECT StudentCode, SUM(Mark) FROM M_Mark GROUP BY StudentCode;
+-------------+-----------+
| StudentCode | SUM(Mark) |
+-------------+-----------+
|        1001 |       664 |
|        1002 |       602 |
|        1003 |       378 |
|        1004 |       321 |
|        1005 |       442 |
+-------------+-----------+
5 rows in set (0.00 sec)
```
3. Display the subject, average mark for each subject.

```
mysql> SELECT SubjectCode, AVG(Mark) FROM M_Mark GROUP BY SubjectCode;
+-------------+-----------+
| SubjectCode | AVG(Mark) |
+-------------+-----------+
|         101 |   67.4000 |
|         102 |   61.8000 |
|         103 |   69.8000 |
|         104 |   66.0000 |
|         105 |   71.0000 |
|         106 |   70.0000 |
|         107 |   75.4000 |
+-------------+-----------+
7 rows in set (0.00 sec)
```
4. Display the name of subjects for which at least one student got below 40%.

```
mysql> SELECT SubjectName FROM Subject WHERE SubjectCode IN (SELECT SubjectCode FROM M_Mark WHERE Mark < 0.4 * (SELECT MaxMark FROM Subject WHERE Subject.SubjectCode = M_Mark.SubjectCode));
+-------------+
| SubjectName |
+-------------+
| SUB101      |
| SUB102      |
| SUB103      |
| SUB104      |
| SUB105      |
+-------------+
5 rows in set (0.00 sec)
```
5. Display the name, subject and percentage of mark who got below 40%.

```
mysql> SELECT StudentName, SubjectName, (Mark / MaxMark * 100) AS Percentage FROM Student, Subject, M_Mark WHERE Student.StudentCode = M_Mark.StudentCode AND Subject.SubjectCode = M_Mark.SubjectCode AND Mark < 0.4 * MaxMark;
+-------------+-------------+------------+
| StudentName | SubjectName | Percentage |
+-------------+-------------+------------+
| STUD1003    | SUB101      |    39.0000 |
| STUD1005    | SUB102      |    30.0000 |
| STUD1004    | SUB103      |    36.0000 |
| STUD1003    | SUB104      |    33.0000 |
| STUD1004    | SUB105      |    30.0000 |
+-------------+-------------+------------+
5 rows in set (0.00 sec)
```
6. Display the faculties and allotted subjects for each faculty.

```
mysql> SELECT FacultyName, GROUP_CONCAT(SubjectName) FROM Faculty JOIN Subject ON Faculty.FacultyCode = Subject.FacultyCode GROUP BY FacultyName;
+-------------+---------------------------+
| FacultyName | GROUP_CONCAT(SubjectName) |
+-------------+---------------------------+
| faculty001  | SUB101,SUB106             |
| faculty002  | SUB102,SUB107             |
| faculty003  | SUB103                    |
| faculty004  | SUB104                    |
| faculty005  | SUB105                    |
+-------------+---------------------------+
5 rows in set (0.00 sec)
```
7. Display the name of faculties who take more than one subject.

```
mysql> SELECT FacultyName FROM Faculty WHERE FacultyCode IN (SELECT FacultyCode FROM Subject GROUP BY FacultyCode HAVING COUNT(*) > 1);
+-------------+
| FacultyName |
+-------------+
| faculty001  |
| faculty002  |
+-------------+
2 rows in set (0.00 sec)
```
8. Display name, subject, mark, % of mark in ascending order of mark.

```
mysql> SELECT StudentName, SubjectName, Mark, (Mark / MaxMark * 100) AS Percentage FROM Student, Subject, M_Mark WHERE Student.StudentCode = M_Mark.StudentCode AND Subject.SubjectCode = M_Mark.SubjectCode ORDER BY Mark;
+-------------+-------------+------+------------+
| StudentName | SubjectName | Mark | Percentage |
+-------------+-------------+------+------------+
| STUD1005    | SUB102      |   30 |    30.0000 |
| STUD1004    | SUB105      |   30 |    30.0000 |
| STUD1003    | SUB104      |   33 |    33.0000 |
| STUD1004    | SUB103      |   36 |    36.0000 |
| STUD1003    | SUB101      |   39 |    39.0000 |
| STUD1004    | SUB104      |   44 |    44.0000 |
| STUD1004    | SUB106      |   45 |    45.0000 |
| STUD1004    | SUB102      |   45 |    45.0000 |
| STUD1003    | SUB102      |   48 |    48.0000 |
| STUD1003    | SUB105      |   50 |    50.0000 |
| STUD1005    | SUB106      |   52 |    52.0000 |
| STUD1005    | SUB101      |   54 |    54.0000 |
| STUD1004    | SUB107      |   55 |    55.0000 |
| STUD1003    | SUB103      |   56 |    56.0000 |
| STUD1004    | SUB101      |   66 |    66.0000 |
| STUD1005    | SUB107      |   67 |    67.0000 |
| STUD1005    | SUB103      |   70 |    70.0000 |
| STUD1003    | SUB106      |   73 |    73.0000 |
| STUD1003    | SUB107      |   79 |    79.0000 |
| STUD1002    | SUB104      |   80 |    80.0000 |
| STUD1005    | SUB104      |   81 |    81.0000 |
| STUD1002    | SUB106      |   82 |    82.0000 |
| STUD1002    | SUB101      |   83 |    83.0000 |
| STUD1002    | SUB107      |   85 |    85.0000 |
| STUD1005    | SUB105      |   88 |    88.0000 |
| STUD1002    | SUB105      |   89 |    89.0000 |
| STUD1002    | SUB102      |   90 |    90.0000 |
| STUD1001    | SUB107      |   91 |    91.0000 |
| STUD1001    | SUB104      |   92 |    92.0000 |
| STUD1002    | SUB103      |   93 |    93.0000 |
| STUD1001    | SUB103      |   94 |    94.0000 |
| STUD1001    | SUB101      |   95 |    95.0000 |
| STUD1001    | SUB102      |   96 |    96.0000 |
| STUD1001    | SUB106      |   98 |    98.0000 |
| STUD1001    | SUB105      |   98 |    98.0000 |
+-------------+-------------+------+------------+
35 rows in set (0.00 sec)
```
