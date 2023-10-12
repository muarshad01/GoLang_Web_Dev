## 131. Installing `Postgres`

* [How to Install PostgreSql in Mac M1/M2](https://www.youtube.com/watch?v=fwPR-PCY0h8)
    
    - `postgresql.org` -> Download -> `macOS` -> `Postgres.app` -> `Postgres.app with PostgreSQL 16 (Universal)` -> Download
    
    - search 'Postgres' -> Initialize (marshad, postgres, template1)
    - click `marshad`

```
marshad# \conninfo
You are connected to database "marshad" as user "marshad" via socket in "/tmp" at port "5432".
marshad-# \q 
```

* Configure your $PATH to use the included command line tools (optional):
```
$ sudo mkdir -p /etc/paths.d &&
$ echo /Applications/Postgres.app/Contents/Versions/latest/bin | sudo tee /etc/paths.d/postgresapp
$ exit
```

```
marshad@marshad-ltmnwup ~ % psql
psql (16.0)
Type "help" for help.

marshad=#
```

```
marshad=# \list
```

```
marshad=# create database billingdb;
marshad=# \list

marshad=# \c billingdb
You are now connected to database "billingdb" as user "marshad".
billingdb=#

billingdb=# exit
marshad@marshad-ltmnwup ~ %
```

***

## 132. Creating Database

***

## 133. Create Table

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















