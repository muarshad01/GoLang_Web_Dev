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

***

## 135. Auto Increment Primary Key

***

## 136. Hands-on Exercise

***

## 137. Hands-on Exercise - Solution

***

## 138. Relational Databases

***

## 139. Query - Cross Join

***

## 140. Query - Inner Join

***

## 141. Query - Three Table Inner Join

***

## 142. Query - Outer Joins

***

## 143. Clauses

***

## 144. Update a Record

***

## 145. Delete a Record

***

## 146. Users - Create, Grant, Alter, Remove

***

## 147. `Go` & `Postgres`

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















