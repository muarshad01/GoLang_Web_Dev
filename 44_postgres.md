# PostgreSQL

* [Nice tutorial](https://www.tutorialspoint.com/postgresql/postgresql_create_database.htm)
* [SQL Tutorial](https://www.w3schools.com/sql/default.asp)
* [documenation reference](https://www.postgresql.org/docs/9.4/static/app-psql.html)

***

## install
[postgresql website](https://www.postgresql.org/download/)

### mac
Postgres.app is fine.

***

## log in

```
psql
```

or 
```
/Applications/Postgres.app/Contents/Versions/9.6/bin/psql -p5432
```

## list databases
```
\l
```

## log out
```
\q
```
***

#  create database
```
CREATE DATABASE employees;
```

## list databases
```
\l
```

## connect to a database
```
\c <database name>
```

## switch back to postgres database
```
\c postgres
```

## see current user
```
SELECT current_user;
```

## see current database
```
SELECT current_database();
```

## drop (remove, delete) database
```
DROP DATABASE <database name>;
```

***

# create table
```
CREATE TABLE employees (
   ID             INT         PRIMARY KEY     NOT NULL,
   NAME           TEXT                        NOT NULL,
   RANK           INT                          NOT NULL,
   ADDRESS        CHAR(50),
   SALARY         REAL        DEFAULT         25500.00,
   BDAY			      DATE        DEFAULT         '1900-01-01'
);
```

## show tables in a database (list down)
```
\d
```

## show details of a table
```
\d <table name>
```

## drop a table
```
DROP TABLE <table name>;
```

## schema
Schemas allow us to organize our database and database code.

A schema is like a folder.

Into this folder, you can put tables, views, indexes, sequences, data types, operators, and functions. 

Unlike folders, however, schemas can't be nested.

Schemas provide namespacing.

[Read more about schemas](https://www.tutorialspoint.com/postgresql/postgresql_schema.htm)
