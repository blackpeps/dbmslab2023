DBMS LAB 2023

17/08/2023

mysql -u root -p
show databases;
create database sreeram;
create table student (rollno int primarykey, name varchar(255), age int);
insert into student values (1, 'Kevin', 20);
insert into student values (2, 'Nikhil', 20), (3, 'Tinu', 20), (3, 'Sreeram', 20), (4, 'Merlin', 20);
alter table student add ph_no int;
alter table student change ph_no phno int;
select * from student;
alter table student add dob date;
select rollno, name from student where rollno>2;
update student set dob=2002-12-13 where rollno=4;
update student set phno=5678;
desc student;
alter table student add time time;
alter table student add date_and_time timestamp;
update student set date_and_time='2023-10-11 04:55:23' where rollno=5;
update student set time='05:30:13' where rollno=4;
delete from student where rollno=4;
delete from student;
