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

***

# insert a record
```
INSERT INTO employees (ID,NAME,RANK,ADDRESS,SALARY,BDAY) VALUES (1, 'Mark', 7, '1212 E. Lane, Someville, AK, 57483', 43000.00 ,'1992-01-13');
```

## list records in a table
```
SELECT * FROM <table name>;
```

## insert a record - variations
omitted values will have the [default value](https://www.postgresql.org/docs/9.3/static/ddl-default.html):
```
INSERT INTO employees (ID,NAME,RANK,ADDRESS,BDAY) VALUES (2, 'Marian', 8, '7214 Wonderlust Ave, Lost Lake, KS, 22897', '1989-11-21');
```

we can use DEFAULT rather leaving a field blank or specifying a value:
```
INSERT INTO employees (ID,NAME,RANK,ADDRESS,SALARY,BDAY) VALUES (3, 'Maxwell', 6, '7215 Jasmine Place, Corinda, CA 98743', 87500.00, DEFAULT);
```

we can insert multiple rows:
```
INSERT INTO employees (ID,NAME,RANK,ADDRESS,SALARY,BDAY) VALUES 
(4, 'Jasmine', 5, '983 Star Ave., Brooklyn, NY, 00912 ', 55700.00, '1997-12-13' ), 
(5, 'Orranda', 9, '745 Hammer Lane, Hammerfield, Texas, 75839', 65350.00 , '1992-12-13');
```

***

# auto increment key field
Instead of creating a unique ID number ourselves, we can have postgres automatically increment this ID field.
 
 To do this we use the data types smallserial, serial or bigserial (not true types but for convenience).
 
 This is like AUTO_INCREMENT in other databases.

```
CREATE TABLE phonenumbers(
	ID  SERIAL PRIMARY KEY,
	PHONE           TEXT      NOT NULL
);
```

```
INSERT INTO phonenumbers (PHONE) VALUES ( '234-432-5234'), ('543-534-6543'), ('312-123-5432');
```

```
\d phonenumbers
```

```
SELECT * FROM phonenumbers;
```

```
CREATE TABLE phonenumbers (
	ID  	SERIAL	PRIMARY KEY			NOT NULL,
   	PHONE           CHAR(50) 			NOT NULL,
   	EMP_ID         	INT		references 	employees(ID)
);
```

```
INSERT INTO phonenumbers (PHONE,EMP_ID) VALUES ('555-777-8888', 4), ('555-222-3345', 4), ('777-543-3451', 1), ('544-756-2334', 2);
```

***

# Cross Join
```
SELECT <fields> FROM <table1> CROSS JOIN <table2>;
```

# Inner Join
```
SELECT <fields> FROM <table> INNER JOIN <table> ON <pkey> = <fkey>;
```

# Outer Join
```
SELECT <fields> FROM <table1> LEFT OUTER JOIN  <table2> ON <pkey> = <fkey>;
SELECT <fields> FROM <table1> RIGHT OUTER JOIN <table2> ON <pkey> = <fkey>;
SELECT <fields> FROM <table1> FULL OUTER JOIN  <table2> ON <pkey> = <fkey>;
```
***
