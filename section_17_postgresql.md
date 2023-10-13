## 131. Installing `Postgres`

* [How to Install PostgreSql in Mac M1/M2](https://www.youtube.com/watch?v=fwPR-PCY0h8)

* `postgresql.org` -> Download -> `macOS` -> `Postgres.app` -> `Postgres.app with PostgreSQL 16 (Universal)` -> Download
    - search 'Postgres' -> Initialize (`marshad`, `postgres`, `template1`)
    - click `marshad`

```unix
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
```sql
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
DELETE FROM table WHERE <condition>;
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

```sql
db, err := sql.Open("postgres", "postgres://bond    :password@localhost     /bookstore    ?sslmode=disable")
db, err := sql.Open("postgres", "postgres://username:password@localhost:5432/database_name?sslmode=disable")
```

```
$ cd /Users/marshad/Desktop/golang-web-dev/044_postgres/16_go-postgres
$ go mod init 16_go-postgres
$ go mod tidy

$ go run main.go
```

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

* We will be using the following example created in [this article by Alex Edwards](http://www.alexedwards.net/blog/practical-persistence-sql) and licensed under a [MIT license](https://opensource.org/licenses/MIT)

* In order to successfully pull records from a table in a database as our user `bond`, we will need to [ALTER](https://www.postgresql.org/docs/9.6/static/sql-alteruser.html) `bond` to have a different role.

* alter bond's role
```sql
ALTER user bond with superuser;
```

* switch to your bookstore database
    - You should already have a `bookstore` database:

* list databases
```sql
\l                  # `l` or list
```

* switch into that database
```sql
\c bookstore        # `c` or choose
```

* directory of tables, if any
```sql
\d                  # `d` or describe
```

# create table

```sql
CREATE TABLE books (
  isbn    char(14)      PRIMARY KEY NOT NULL,
  title   varchar(255)  NOT NULL,
  author  varchar(255)  NOT NULL,
  price   decimal(5, 2) NOT NULL
);
```

* directory of tables
```sql
\d                  # `d` or describe
```

* details of table `books`
```sql
\d books
```

* insert records
```sql
INSERT INTO books (isbn, title, author, price) VALUES
('978-1503261969', 'Emma',             'Jayne Austen',        9.44),
('978-1505255607', 'The Time Machine', 'H. G. Wells',         5.99),
('978-1503379640', 'The Prince',       'Niccolò Machiavelli', 6.99);
```

* view records
```sql
SELECT * FROM books;
```

* main.go

```go
_ "github.com/lib/pq"
```

* We don't use anything in the `github.com/lib/pq` package directly, which means that the `Go` compiler will raise an error if we try to import it normally. 
* But, we need the `pq` package's `init()` function to run so that our driver can register itself with database/sql. 
* We get around this by aliasing the package name to the blank identifier (`_`). 
* This means `pq.init()` still gets executed, but the alias is harmlessly discarded (and our code runs error-free). 
* This approach is standard for most of Go's SQL drivers. -- Alex Edwards

* define a book type struct
```go
type Book struct {
	isbn   string
	title  string
	author string
	price  float32
}
```

Next we define a Book type. The `struct` fields and their types must align to our books table. For completeness, I should point out that we've only been able to use the `string` and `float32` types safely because we set `NOT NULL` constraints on the columns in our table. If the table contained nullable fields we would need to use the `sql.NullString` and `sql.NullFloat64` types instead – see [this Gist](https://gist.github.com/alexedwards/dc3145c8e2e6d2fd6cd9) for a working example. Generally it's easiest to avoid nullable fields altogether if you can, which is what we've done here. -- Alex Edwards

* initialize a new sql.DB
```go
db, err := sql.Open("postgres", "postgres://bond:password@localhost/bookstore?sslmode=disable")
	if err != nil {
		panic(err)
	}
	defer db.Close()
```

* In the `main()` function we initialise a new `sql.DB` by calling `sql.Open()`. We pass in the name of our driver (in this case `postgres`) and the connection string (you'll need to check your driver documentation for the correct format). 
* It's worth emphasizing that `sql.DB` is not a database connection – it's an abstraction representing a pool of underlying connections. You can change the maximum number of open and idle connections in the pool with the `db.SetMaxOpenConns()` and `db.SetMaxIdleConns()` methods respectively. 
* A final thing to note is that `sql.DB` is safe for concurrent access, which is very convenient if you're using it in a web application (like we will shortly). -- Alex Edwards

* ping the db
```go
	if err = db.Ping(); err != nil {
		panic(err)
	}
```

* Because  `sql.Open()` doesn't actually check a connection, we also call `DB.Ping()` to make sure that everything works OK on startup. -- Alex Edwards

* query the db
```go
rows, err := db.Query("SELECT * FROM books")
	if err != nil {
		panic(err)
	}
	defer rows.Close()
```

* We will fetch a resultset from the books table using the `db.Query()` method and assign it to a  rows variable. 
* Then we defer `rows.Close()` to ensure the resultset is properly closed before the parent function returns.
* Closing a resultset properly is really important. 
* As long as a resultset is open it will keep the underlying database connection open – which in turn means the connection is not available to the pool.
* So if something goes wrong and the resultset isn't closed it can rapidly lead to all the connections in your pool being used up. 
* Another gotcha (which caught me out when I first began) is that the defer statement should come after you check for an error from `db.Query`. Otherwise, if `db.Query()` returns an error, you'll get a panic trying to close a `nil` resultset." -- Alex Edwards

* iterate through results
```go
	for rows.Next() {
		bk := Book{}
		err := rows.Scan(&bk.isbn, &bk.title, &bk.author, &bk.price) // order matters
		if err != nil {
			panic(err)
		}
		bks = append(bks, bk)
	}
```

* We then use `rows.Next()` to iterate through the rows in the resultset. 
* This preps the first (and then each subsequent) row to be acted on by the `rows.Scan()` method. 
* Note that if iteration over all of the rows completes then the resultset automatically closes itself and frees-up the connection. 
* We use the `rows.Scan()` method to copy the values from each field in the row to a new Book object that we created. We then check for any errors that occurred during Scan, and add the new Book to a slice of books. -- Alex Edwards

* make sure everything ran well
```go
	if err = rows.Err(); err != nil {
		panic(err)
	}
```

* When our `rows.Next()` loop has finished we call `rows.Err()`. 
* This returns any error that was encountered during the interation. 
* It's important to call this – don't just assume that we completed a successful iteration over the whole resultset. 
-- Alex Edwards 
* `Err()` returns the error, if any, that was encountered during iteration. `Err()` may be called after an explicit or implicit Close.

***

## 149. Web App


* Add a package level scope variable
```go
var db *sql.DB
```

*Initialize your database
    - Note: `defer.db.Close()` has been removed
```go
func init() {
	var err error
	db, err = sql.Open("postgres", "postgres://bond:password@localhost/bookstore?sslmode=disable")
	if err != nil {
		panic(err)
	}

	if err = db.Ping(); err != nil {
		panic(err)
	}
	fmt.Println("You connected to your database.")
}
```

* add routes & server
```go
func main() {
	http.HandleFunc("/", index)
	http.ListenAndServe(":8080", nil)
}
```

* add a index func
```go
func index(w http.ResponseWriter, r *http.Request){
	if r.Method != "GET" {
		http.Error(w, http.StatusText(405), http.StatusMethodNotAllowed)
		return
	}

	rows, err := db.Query("SELECT * FROM books")
	if err != nil {
		http.Error(w, http.StatusText(500), 500)
		return
	}
	defer rows.Close()

	bks := make([]Book, 0)
	for rows.Next() {
		bk := Book{}
		err := rows.Scan(&bk.isbn, &bk.title, &bk.author, &bk.price) // order matters
		if err != nil {
			http.Error(w, http.StatusText(500), 500)
			return
		}
		bks = append(bks, bk)
	}
	if err = rows.Err(); err != nil {
		http.Error(w, http.StatusText(500), 500)
		return
	}

	for _, bk := range bks {
		fmt.Fprintf(w, "%s, %s, %s, $%.2f\n", bk.isbn, bk.title, bk.author, bk.price)
	}
}
```

* run the application and make a request
```
$ curl -i localhost:8080/books
```

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















