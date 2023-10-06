# DBMS Lab 2023

### Lab Experiments

| Experiment                                                                                                                                                                                                                                | Date          |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| 1. [ Introduction to ER diagram and SQL](/01.%20Introduction%20to%20ER%20diagram%20and%20SQL/)                                                                                                                                            | Not yet done. |
| 2. [ Creation, modification, configuration and deletion command. ](/02.%20Creation,%20modification,%20configuration%20and%20deletion%20command/)                                                                                          | 17-08-2023    |
| 3. [ Exprot ER diagram from database and verify relationships. ](/03.%20Export%20ER%20diagram%20from%20database%20and%20verify%20relationships/)                                                                                          | Not yet done. |
| 4. [ Database Initialisation, Data Insert, Import to database. ](/04.%20Database%20Initialisation,%20Data%20Insert,%20Import%20to%20database/)                                                                                            | Not yet done. |
| 5. [ Practise SQL commands for DML. ](/05.%20Practise%20SQL%20commands%20for%20DML/)                                                                                                                                                      | 17-08-2023    |
| 6. [ Implementation of built in functions. ](/06.%20Implementation%20of%20built%20in%20functions/)                                                                                                                                        | 24-08-2023    |
| 7. [ Implementation of aggregate functions. ](/07.%20Implementation%20of%20aggregate%20functions/)                                                                                                                                        | 24-08-2023    |
| 8. [ Implementation of orderby, group by, and having. ](/08.%20Implementation%20of%20orderby,%20group%20by,%20and%20having/)                                                                                                              | 24-08-2023    |
| 9. [ Implementation of Set Operations, nested and queries. ](/09.%20Implementation%20of%20Set%20Operations,%20nested%20and%20queries/)                                                                                                    | 05-10-2023    |
| 10. [ Practise of SQL TCL commands Rollback, commit, savepoint. ](/10.%20Practise%20of%20SQL%20TCL%20commands%20Rollback,%20commit,%20savepoint/)                                                                                         | 05-10-2023    |
| 11. [ Implementation of DCL commands for granting and revoking user privileges. ](/11.%20Implementation%20of%20DCL%20commands%20for%20granting%20and%20revoking%20user%20privileges/)                                                     | 07-10-2023    |
| 12. [ Practise of SQL Commands for creation or view assertion. ](/12.%20Practise%20of%20SQL%20Commands%20for%20creation%20or%20view%20assertion/)                                                                                         | 07-10-2023    |
| 13. [ Implementation of various control structures like, if then, then else, if then else, if while. ](/13.%20Implementation%20of%20various%20control%20structures%20like,%20if%20then,%20then%20else,%20if%20then%20else,%20if%20while/) | Not yet done. |
| 14. [ Creation of procedure,triggers, functions. ](/14.%20Creation%20of%20procedure,triggers,%20functions/)                                                                                                                               | Not yet done. |
| 15. [ Creation of cursor. ](/15.%20Creation%20of%20cursor/)                                                                                                                                                                               | Not yet done. |
| 16. [ Creation of Packages. ](/16.%20Creation%20of%20Packages/)                                                                                                                                                                           | Not yet done. |
| 17. [ Creation of PL/SQL block for exception handling. ](/17.%20Creation%20of%20PLSQL%20block%20for%20exception%20handling/)                                                                                                              | Not yet done. |
| 18. [ Familiarization of NoSQL Databases and CRUD operations ](/18.%20Familiarization%20of%20NoSQL%20Databases%20and%20CRUD%20operations/)                                                                                                | Not yet done. |
| 19. [ Project Using Rdbms Concepts And Front End Tools ](/19.%20Project%20Using%20Rdbms%20Concepts%20And%20Front%20End%20Tools/)                                                                                                          | Not yet done. |

## Some Basics before you start SQL

- Get mySQL for windows at following Link: [ Windows ](https://dev.mysql.com/downloads/windows/installer/) (This is an all-in-one package, so just download and install. It should be around 331 MB in size.) (You will only need to use the shell version of MySQL to move on and Workbench software is not needed as of now, so you can save some traffic of data by downloading shell version of MySQL from their website if you know to set-up afterwards, for all others use this GUI to get started).

- A note while installation, leave the default settings as it is, except for selecting the option to install all the components (Full).
- Run `MySQL 8.0 Command Line Client` from start menu (As destop shortcuts are rarely created).

  ![Alt text](/img/image-14.png)

- Do set a password for the root. Unlike linux (Ubuntu) you can directly login to your mySQL without needing to enter the following:

```
mysql -u root -p
```
