## 131. Installing `Postgres`

* [How to Install PostgreSql in Mac M1/M2](https://www.youtube.com/watch?v=fwPR-PCY0h8)

* `postgresql.org` -> Download -> `macOS` -> `Postgres.app` -> `Postgres.app with PostgreSQL 16 (Universal)` -> Download
    - search 'Postgres' -> Initialize (`marshad`, `postgres`, `template1`)
    - click `marshad`

```
marshad# \conninfo
You are connected to database "marshad" as user "marshad" via socket in "/tmp" at port "5432".
marshad-# \q 
```

* Configure your `$PATH` to use the included command line tools (optional):
```
$ sudo mkdir -p /etc/paths.d &&
$ echo /Applications/Postgres.app/Contents/Versions/latest/bin | sudo tee /etc/paths.d/postgresapp
$ exit
```
OR

```
$ /Applications/Postgres.app/Contents/Versions/latest/bin/psql -p5432
```

```
marshad@marshad-ltmnwup ~ % psql
psql (16.0)
Type "help" for help.

marshad=#
```

```
marshad=# \list
OR
marshad=# \
```

```
marshad=# create database billingdb;
marshad=# \list

marshad=# \c billingdb
You are now connected to database "billingdb" as user "marshad".
billingdb=#

billingdb=# \q
marshad@marshad-ltmnwup ~ %
```

***

## 132. Creating Database

* create database
```sql
CREATE DATABASE employees;
```

* list databases
```sql
\l
```

* connect to a database

```sql
\c <database name>                  # `c` - choose
```

* switch back to `postgres` database
```sql
\c postgres
```

* see `current_user`
```sql
SELECT current_user;
```

* see `current_database()`
```sql
SELECT current_database();
```

* drop (remove, delete) database
```sql
DROP DATABASE <database name>;
```

***

## 133. Create Table

* create table
```sql
CREATE TABLE employees (
   ID INT PRIMARY KEY     NOT NULL,
   NAME           TEXT    NOT NULL,
   RANK           INT     NOT NULL,
   ADDRESS        CHAR(50),
   SALARY         REAL DEFAULT 25500.00,
   BDAY			  DATE DEFAULT '1900-01-01'
);
```

* show tables in a database (list down)
```sql
\d
```

* show details of a table
```sql
\d <table name>
```

* drop a table
```sql
DROP TABLE <table name>;
```

### schema

* Schemas allow us to organize our database and database code.

* A schema is like a folder.

* Into this folder, you can put tables, views, indexes, sequences, data types, operators, and functions. 

* Unlike folders, however, schemas can't be nested.

* Schemas provide `namespacing`.

[Read more about schemas](https://www.tutorialspoint.com/postgresql/postgresql_schema.htm)

***

## 134. Insert Records

* insert a record
```sql
INSERT INTO employees (ID, NAME, RANK, ADDRESS, SALARY, BDAY) VALUES (1, 'Mark', 7, '1212 E. Lane, Someville, AK, 57483', 43000.00 ,'1992-01-13');
```

* list records in a table
```sql
SELECT * FROM <table name>;
```

* insert a record - variations
    - omitted values will have the [default value](https://www.postgresql.org/docs/9.3/static/ddl-default.html):
```sql
INSERT INTO employees (ID, NAME, RANK, ADDRESS, BDAY) VALUES (2, 'Marian', 8, '7214 Wonderlust Ave, Lost Lake, KS, 22897', '1989-11-21');
```

* we can use `DEFAULT` rather leaving a field blank or specifying a value:
```sql
INSERT INTO employees (ID, NAME, RANK, ADDRESS, SALARY, BDAY) VALUES (3, 'Maxwell', 6, '7215 Jasmine Place, Corinda, CA 98743', 87500.00, DEFAULT);
```

* we can insert multiple rows:
```sql
INSERT INTO employees (ID, NAME, RANK, ADDRESS, SALARY, BDAY) VALUES (4, 'Jasmine', 5, '983 Star Ave., Brooklyn, NY, 00912 ', 55700.00, '1997-12-13' ), (5, 'Orranda', 9, '745 Hammer Lane, Hammerfield, Texas, 75839', 65350.00 , '1992-12-13');
```

***

## 135. Auto Increment Primary Key

### auto increment key field

* Instead of creating a unique ID number ourselves, we can have postgres automatically increment this ID field.
 
* To do this we use the data types `smallserial`, `serial` or `bigserial` (not true types but for convenience).
 
* This is like AUTO_INCREMENT in other databases.

```sql
CREATE TABLE phonenumbers(
    ID  SERIAL PRIMARY KEY,
	PHONE           TEXT      NOT NULL
);
```

```sql
INSERT INTO phonenumbers (PHONE) VALUES ( '234-432-5234'), ('543-534-6543'), ('312-123-5432');
```

```sql
\d phonenumbers                     # `d` - display
```

```sql
SELECT * FROM phonenumbers;
```

***

## 136. Hands-on Exercise

### hands-on exercise

* delete all of your current tables.
* READ ALL OF THIS: create a new table called employees with these fields `id, name, score, salary` AND give `score` a default value of 10 AND have the `id` field automatically increment.
*. add these records and then show all of the records

```
 id |  name  | score | salary 
----+--------+-------+--------
  1 | Daniel |    23 |  55000
  2 | Arin   |    25 |  65000
  3 | Juan   |    24 |  72000
  4 | Shen   |    26 |  64000
  5 | Myke   |    27 |  58000
  6 | McLeod |    26 |  72000
  7 | James  |    32 |  35000
```

***

## 137. Hands-on Exercise - Solution

### solution
```sql
DROP TABLE employees, phonenumbers;
```

```sql
CREATE TABLE employees (
   ID  SERIAL PRIMARY KEY NOT NULL,
   NAME           TEXT    NOT NULL,
   SCORE          INT     DEFAULT 10 NOT NULL,
   SALARY         REAL
);
```

```sql
INSERT INTO employees 
(NAME, SCORE, SALARY) VALUES 
('Daniel', 23, 55000.00), 
('Arin',   25, 65000.00), 
('Juan',   24, 72000.00), 
('Shen',   26, 64000.00), 
('Myke',   27, 58000.00), 
('McLeod', 26, 72000.00), 
('James',  32, 35000.00);
```

```sql
SELECT * FROM employees;
```

***

## 138. Relational Databases

```sql
CREATE TABLE phonenumbers (
   ID  SERIAL PRIMARY KEY   NOT NULL,
   PHONE           CHAR(50) NOT NULL,
   EMP_ID          INT      references employees(ID)
);
```

```sql
INSERT INTO phonenumbers (PHONE,EMP_ID) VALUES 
('555-777-8888', 4), 
('555-222-3345', 4), 
('777-543-3451', 1), 
('544-756-2334', 2);
```

***

## 139. Query - `Cross Join (X)`

* A cross join returns the `Cartesian product` of rows from tables in the join. In other words, it will produce rows which combine each-row-from-the-first-table with each-row-from-the-second-table.

```
SELECT * FROM employees;
SELECT * FROM phonenumbera;
```

```
SELECT <fields> FROM <table1> CROSS JOIN <table2>;
```

```
SELECT * FROM employees CROSS JOIN phonenumbers;
```

***

## 140. Query - Inner Join

* If you place `Primary Key` from one table to another table, it become `Foreighn Key`.

```sql
SELECT <fields> FROM <table> INNER JOIN <table> ON <pkey> = <fkey>;
```

```sql
SELECT employees.NAME, phonenumbers.PHONE from employees INNER JOIN phonenumbers ON employees.ID = phonenumbers.EMP_ID;
```

***

## 141. Query - Three Table Inner Join

***

## 142. Query - Outer Joins

***

## 143. Clauses

* Adding `WHERE` to a SQL query allows you to filter results.
```sql
SELECT * FROM employees WHERE salary > 60000;
```

* `AND`
```sql
SELECT * FROM employees WHERE salary > 60000 AND score = 26;
```

* `IN`
```
SELECT * FROM employees WHERE score IN (25, 26);
```

* `NOT`
```sql
SELECT * FROM employees WHERE score NOT IN (25, 26);
```

* `BETWEEN`
```sql
SELECT * FROM employees WHERE score BETWEEN 23 AND 26;
```

* `IS NOT NULL`
```sql
SELECT * FROM employees WHERE score IS NOT NULL;
```

* `LIKE`
```sql
SELECT * FROM employees WHERE name LIKE '%an%';
```

* `OR`
```sql
SELECT * FROM employees WHERE score <= 24 OR salary < 50000;
```


* `LIMIT` the number of records returned
```sql
SELECT * FROM employees LIMIT 4;
```

* `ORDER BY`
```sql
SELECT * FROM employees ORDER BY id LIMIT 4;
```
***

## 144. Update a Record

* `UPDATE`

```sql
UPDATE table
SET col1 = val1, col2 = val2, ..., colN = valN
WHERE <condition>;
```

```sql
SELECT * FROM employees;
```

```sql
UPDATE employees SET score = 99 WHERE ID = 3;
```

* `ORDER BY`
```sql
SELECT * FROM employees ORDER BY id;
```

***

## 145. Delete a Record

* `DELETE`
```sql
DELETE FROM table
WHERE <condition>;
```

```sql
SELECT * FROM sport;
```

```sql
DELETE FROM sport WHERE id = 6;
```

* `WARNING`: this deletes all records:**
```sql
DELETE FROM sport;
```

***

## 146. Users - Create, Grant, Alter, Remove

* see `current user`
```sql
SELECT current_user;
```

* details of users
```sql
\du
```

* create user
```sql
CREATE USER james WITH PASSWORD 'password';
```

* grant privileges
    - privileges: SELECT, INSERT, UPDATE, DELETE, RULE, ALL
```sql
GRANT ALL PRIVILEGES ON DATABASE company to james;
```

* revoke privileges
```sql
REVOKE ALL PRIVILEGES ON DATABASE company from james;
```

* ALTER
```sql
ALTER USER james WITH SUPERUSER;
```

```sql
ALTER USER james WITH NOSUPERUSER;
```

* remove
```sql
DROP USER james;
```

***

## 147. `Go` & `Postgres`

* [SQL Database Drivers](https://github.com/golang/go/wiki/SQLDrivers)


```
$ cd /Users/marshad/Desktop/golang-web-dev/044_postgres/16_go-postgres
$ go mod init 16_go-postgres
$ go mod tidy

$ go run main.go
```

* `// urlExample := "postgres://username:password@localhost:5432/database_name"`

* create a db
```sql
CREATE DATABASE bookstore;
```

* create user
```sql
CREATE USER bond WITH PASSWORD 'password';
```

* grant privileges
```sql
GRANT ALL PRIVILEGES ON DATABASE bookstore to bond;
```

***

## 148. Select Query

***

## 149. Web App

***

## 150. Query Row

***

## 151. Insert Record

***

## 152. Update Record

***

## 153. Delete Record

***

## 154. Code Organization

***















