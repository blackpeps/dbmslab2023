# DBMS Lab 2023

### Lab Experiments

| Experiment                                                                                                                                                                                                                                | Date          | Download PDFs |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- | --- |
| 1. [ Introduction to ER diagram](/01.%20Introduction%20to%20ER%20diagram%20and%20SQL/)                                                                                                                                                    | 10-08-2023    | - |
| 2. [ UNIVERSITY MANAGEMENT SYSTEM ER DIAGRAM](/02.%20UNIVERSITY%20MANAGEMENT%20SYSTEM%20ER%20DIAGRAM/)                                                                                                                                    | 10-08-2023    | - |
| 3. [ INTRODUCTION TO SQL](/03.%20INTRODUCTION%20TO%20SQL/)                                                                                                                                                                                | 10-08-2023    | - |
| 4. [ Creation, modification, configuration and deletion command ](/04.%20Creation,%20modification,%20configuration%20and%20deletion%20command/)                                                                                           | 17-08-2023    | [EXP04.pdf](https://github.com/blackpeps/dbmslab2023/files/14086997/EXP04.pdf)|
| 5. [ SQL commands for DML. ](/05.%20Practise%20SQL%20commands%20for%20DML/)                                                                                                                                                               | 17-08-2023    | [EXP05.pdf](https://github.com/blackpeps/dbmslab2023/files/14087001/EXP05.pdf)|
| 6. [ Implementation of built in functions. ](/06.%20Implementation%20of%20built%20in%20functions/)                                                                                                                                        | 24-08-2023    |[EXP06.pdf](https://github.com/blackpeps/dbmslab2023/files/14087006/EXP06.pdf)|
| 7. [ Implementation of aggregate functions. ](/07.%20Implementation%20of%20aggregate%20functions/)                                                                                                                                        | 24-08-2023    |[EXP07.pdf](https://github.com/blackpeps/dbmslab2023/files/14087009/EXP07.pdf)|
| 8. [ Implementation of orderby, group by, and having. ](/08.%20Implementation%20of%20orderby,%20group%20by,%20and%20having/)                                                                                                              | 24-08-2023    |[EXP08.pdf](https://github.com/blackpeps/dbmslab2023/files/14087012/EXP08.pdf)|
| 9. [ Implementation of Set Operations, nested and queries. ](/09.%20Implementation%20of%20Set%20Operations,%20nested%20and%20queries/)                                                                                                    | 05-10-2023    |[EXP09.pdf](https://github.com/blackpeps/dbmslab2023/files/14087016/EXP09.pdf)|
| 10. [ Practise of SQL TCL commands Rollback, commit, savepoint. ](/10.%20Practise%20of%20SQL%20TCL%20commands%20Rollback,%20commit,%20savepoint/)                                                                                         | 05-10-2023    |[EXP10.pdf](https://github.com/blackpeps/dbmslab2023/files/14087018/EXP10.pdf)|
| 11. [ Implementation of DCL commands for granting and revoking user privileges. ](/11.%20Implementation%20of%20DCL%20commands%20for%20granting%20and%20revoking%20user%20privileges/)                                                     | 07-10-2023    |[EXP11.pdf](https://github.com/blackpeps/dbmslab2023/files/14087020/EXP11.pdf)|
| 12. [ Practise of SQL Commands for creation or view assertion. ](/12.%20Practise%20of%20SQL%20Commands%20for%20creation%20or%20view%20assertion/)                                                                                         | 07-10-2023    |[EXP12.pdf](https://github.com/blackpeps/dbmslab2023/files/14087023/EXP12.pdf)|
| 13. [ Implementation of various control structures like, if then, then else, if then else, if while. ](/13.%20Implementation%20of%20various%20control%20structures%20like,%20if%20then,%20then%20else,%20if%20then%20else,%20if%20while/) | 12-10-2023    |[EXP13.pdf](https://github.com/blackpeps/dbmslab2023/files/14087024/EXP13.pdf)|
| 14. [ Creation of procedure,triggers, functions. ](/14.%20Creation%20of%20procedure,triggers,%20functions/)                                                                                                                               | 20-10-2023    |[EXP14.pdf](https://github.com/blackpeps/dbmslab2023/files/14087026/EXP14.pdf)|
| 15. [ Creation of cursor. ](/15.%20Creation%20of%20cursor/)                                                                                                                                                                               | 09-11-2023    |[EXP15.pdf](https://github.com/blackpeps/dbmslab2023/files/14087036/EXP15.pdf)|
| 16. [ Creation of Packages. ](/16.%20Creation%20of%20Packages/)                                                                                                                                                                           | 02-11-2023    |[EXP16.pdf](https://github.com/blackpeps/dbmslab2023/files/14087039/EXP16.pdf)|
| 17. [ Creation of PL/SQL block for exception handling. ](/17.%20Creation%20of%20PLSQL%20block%20for%20exception%20handling/)                                                                                                              | 16-11-2023 |[EXP17.pdf](https://github.com/blackpeps/dbmslab2023/files/14087042/EXP17.pdf)|
| 18. [ Familiarization of NoSQL Databases and CRUD operations ](/18.%20Familiarization%20of%20NoSQL%20Databases%20and%20CRUD%20operations/)                                                                                                | 23-11-2023 | - |
| 19. [ Project Using Rdbms Concepts And Front End Tools ](/19.%20Project%20Using%20Rdbms%20Concepts%20And%20Front%20End%20Tools/)                                                                                                          | 23-11-2023 | - |

## Some Basics before you start SQL

- Get mySQL for windows at following Link: [ Windows ](https://dev.mysql.com/downloads/windows/installer/) (This is an all-in-one package, so just download and install. It should be around 331 MB in size.) (You will only need to use the shell version of MySQL to move on and Workbench software is not needed as of now, so you can save some traffic of data by downloading shell version of MySQL from their website if you know to set-up afterwards, for all others use this GUI to get started).

- A note while installation, leave the default settings as it is, except for selecting the option to install all the components (Full).
- Run `MySQL 8.0 Command Line Client` from start menu (As destop shortcuts are rarely created).

![image-14](https://github.com/blackpeps/dbmslab2023/assets/126700907/9afbe459-cc75-47ea-8dc0-88c58d0d6e87)

- Do set a password for the root. Unlike linux (Ubuntu) you can directly login to your mySQL without needing to enter the following:

```
mysql -u root -p
```
