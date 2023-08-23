## 05. Practise SQL commands for DML.

> Creating database

```
create database sqlpractice;
```

![Alt text](img/image001.png)

> Creating table

```
create table student (
    rollno int primary key,
    name varchar(255),
    age int
);
```

![Alt text](img/image002.png)

> Inserting values into table

```
insert into student values
(1, 'Kevin', 20),
(2, 'Nikhil Philip', 20),
(3, 'Tinu', 20),
(4, 'Sreeram', 20),
(5, 'Merlin', 20),
(6, 'Nikhil Abraham', 20);
```

![Alt text](img/image.png)

> Adding an extra column after table is already created.

```
alter table student add ph_no int;
```

![Alt text](img/image-1.png)

```
alter table student add dob date;
```

![Alt text](img/image-2.png)

> Changing the column name heading from one to another

```
alter table student change ph_no phone_no int;
```

![Alt text](img/image-3.png)

> Modifying datatypes of an existing attribute

```
alter table student modify name varchar(100);
```

![Alt text](img/image-4.png)

> Inserting values into an existing tuple

```
update student set dob='2002-12-13' where rollno=4;
```

The above action is restricted to tuples of the condition provided.

![Alt text](img/image-5.png)

```
update student set phone_no=5678;
```

The above action updates every values in the selected attribute of the table.

![Alt text](img/image-6.png)

> Inserting date and time column and values to the same

```
alter table student add time time;
```

![Alt text](img/image-7.png)

```
alter table student add date_and_time timestamp;
```

![Alt text](img/image-8.png)

```
update student set date_and_time='2023-10-11 04:55:23' where rollno=5;
```

![Alt text](img/image-9.png)

```
update student set time='05:30:13' where rollno=4;
```

![Alt text](img/image-10.png)

> Displaying table in various ways

```
select * from student;
```

![Alt text](img/image-11.png)

```
select rollno, name from student where rollno>2;
```

![Alt text](img/image-12.png)

```
delete from student where rollno=4;
```

![Alt text](img/image-13.png)
