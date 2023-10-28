## 04. Creation, modification, configuration and deletion command.

### Create Database

```
create database database_name;
```

### Create Table

```
create table table_name (
    column_name datatype(size) constraints,
    ...
);
```

### Modification

```
alter table table_name modify column_name datatype(size);
```

_Note:_ **_If you are getting error, use the following command as an alternative:_**

```
alter table table_name change old_column_name new_column_name datatype(size);
```

### Clear all values

```
Truncate table table_name;
```

or

```
delete from table_name;
```

### Delete both Schema and datas

```
drop table table_name;
```
