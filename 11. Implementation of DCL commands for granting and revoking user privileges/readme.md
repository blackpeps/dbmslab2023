## 11. Implementation of DCL commands for granting and revoking user privileges.

## Aim

To implement DCL commands for granting and revoking user privileges.

## Theory

### PRIVILEGES
A privilege is a right to execute an SQL statement or to access another user's object. In Oracle, there are two types of privileges
- System Privileges
- Object Privileges

#### System Privileges
System Privileges are those through which the user can manage the performance of database actions. It is normally granted by DBA to users. Eg: Create Session, Create Table, Create user etc.

#### Object Privileges
Object Privileges allow access to objects or privileges on objects, i.e. tables, table columns, tables, views etc. It includes alter, delete, insert, select update etc. (After creating the user, DBA grant specific system privileges to the user)

#### GRANT
The DBA uses the GRANT statement to allocate system privileges to another user.

*Syntax:*

`GRANT privilege [privilege…. … ] TO USER;`

Eg:
```sql
Grant create session, create table, create view to James;
```
Object privileges vary from object to object. An owner has all privileges or specific privileges on an object.

`GRANT object_priv [(column)] ON object TO user;`

`GRANT select, insert ON emp TO James;`

`GRANT select, update (e_name,e_address) ON emp TO James;`

#### CHANGE PASSWORD:
The DBA creates an account and initializes a password for every user. You can change your password by using the ALTER USER statement.

*Syntax:*

`Alter USER IDENTIFIED BY`

Eg:
```sql
ALTER USER James IDENTIFIED BY sam;
```
#### REVOKE
REVOKE statement is used to remove privileges granted to other users. The privileges you specify are revoked from the users.

*Syntax:*

`REVOKE [privilege.. …] ON object FROM user`

Eg:
```sql
REVOKE create session, create table from James;
REVOKE select, insert ON emp FROM James;
```

#### ROLE
A role is a named group of related privileges that can be granted to the user. In other words, a role is a predefined collection of privileges that are grouped together, thus privileges are easier to assign user.

`Create role custom;`

`Grant create table, create view TO custom;`

`SQL> Grant select, insert ON emp TO custom;`

Eg:
```sql
Grant custom to James, Steve;
```

---

## Question

1. Create a new MYSQL user account.
2. Give privileges to create a new database to a user.
3. Give privileges to a user to create new tables in a specific database.
4. Give privileges to a user to read a specific database table to a user. Give privileges to delete a database to a user.
5. Check the privileges for a specific user.
6. Revoke all privileges.

## Output

1. ```sql
   CREATE USER 'new_user'@'localhost' IDENTIFIED BY 'password';
   ```

   Replace `'new_user'` with the desired username and `'password'` with the user's password.

2. ```sql
   GRANT CREATE ON *.* TO 'new_user'@'localhost';
   ```
   
   > Be cautious with this privilege.

4. ```sql
   GRANT CREATE ON specific_database.* TO 'new_user'@'localhost';
   ```

   Replace `specific_database` with the name of the database where the user should have this privilege.

5. ```sql
   GRANT SELECT ON specific_database.specific_table TO 'new_user'@'localhost';
   GRANT DROP ON specific_database.* TO 'new_user'@'localhost';
   ```

   Replace `specific_database` with the name of the database, and `specific_table` with the name of the table.

6. ```sql
   SHOW GRANTS FOR 'new_user'@'localhost';
   ```

7. ```sql
   REVOKE ALL PRIVILEGES ON *.* FROM 'new_user'@'localhost';
   ```
