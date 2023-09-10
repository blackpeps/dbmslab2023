## 07. Implementation of aggregate functions.

### **This page is under maintenance.**

> Refer [this PDF](pdfs/exp7.pdf) from my repository for any assistance. This PDF may contain additional informations that may not be mentioned here.

### Example

In this experiment, create a table of your liking or use any exisiting table. Then using the table use the aggregate functions such as *sum*,*min*,*max*,*avg* and *count*.

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

Now, that you have a familiarity of using built-in functions, including aggregating function, create the tables with the following fields:

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

#### Performing Queries

1. Display the number of faculties.

```
SELECT COUNT(*) FROM Faculty;
```

2. Display the total mark for each student.
```
SELECT StudentCode, SUM(Mark) FROM M_Mark GROUP BY StudentCode;
```
3. Display the subject, average mark for each subject.

```
SELECT SubjectCode, AVG(Mark) FROM M_Mark GROUP BY SubjectCode;
```
4. Display the name of subjects for which at least one student got below 40%.

```
SELECT SubjectName FROM Subject WHERE SubjectCode IN (SELECT SubjectCode FROM M_Mark WHERE Mark < 0.4 * (SELECT MaxMark FROM Subject WHERE Subject.SubjectCode = M_Mark.SubjectCode));
```
5. Display the name, subject and percentage of mark who got below 40%.

```
SELECT StudentName, SubjectName, (Mark / MaxMark * 100) AS Percentage FROM Student, Subject, M_Mark WHERE Student.StudentCode = M_Mark.StudentCode AND Subject.SubjectCode = M_Mark.SubjectCode AND Mark < 0.4 * MaxMark;
```
6. Display the faculties and allotted subjects for each faculty.

```
SELECT FacultyName, GROUP_CONCAT(SubjectName) FROM Faculty JOIN Subject ON Faculty.FacultyCode = Subject.FacultyCode GROUP BY FacultyName;
```
7. Display the name of faculties who take more than one subject.

```
SELECT FacultyName FROM Faculty WHERE FacultyCode IN (SELECT FacultyCode FROM Subject GROUP BY FacultyCode HAVING COUNT(*) > 1);
```
8. Display name, subject, mark, % of mark in ascending order of mark.

```
SELECT StudentName, SubjectName, Mark, (Mark / MaxMark * 100) AS Percentage FROM Student, Subject, M_Mark WHERE Student.StudentCode = M_Mark.StudentCode AND Subject.SubjectCode = M_Mark.SubjectCode ORDER BY Mark;
```
