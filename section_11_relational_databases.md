## 82. Overview

***

## 83. Installing MySQL - Locally

* [How To Download And Install MYSQL Server In Macbook M1](https://www.youtube.com/watch?v=aWZKws7RWic)

### Check if `MySQL` is installed
```
$ mysql
$ mysql -u root -p
```

### Install `MySQL` & `MySQL Workbench`

* [MySQL Community Downloads](https://dev.mysql.com/downloads/mysql/)
    - No thanks, just start my download.
    - Use Strong Password Encryption -> Next
    - Please enter a password for the "root" user: `1-8#`

* [MySQL Workbench](https://dev.mysql.com/downloads/workbench/)
    - No thanks, just start my download.

* Apple -> System Preferences -> search `mysql`

### `MySQL` access through command-line

```
$ vim ~/.bash_profile

export PATH=$PATH:/usr/local/mysql/bin

$ source ~/.bash_profile
```

```
$ mysql -u root -p

mysql> show databases;
```

***

## 84. Installing `MySQL` - `AWS`

* `aws.amazon.com` -> My Account -> `AWS Management Console` 

* `Services` -> `RDS`

* `Choose a database creation method` -> `Easy Create`    
    - `Databases` -> `Create database` -> `MySQL`
    - `MySQL Community`    
    - `DB instance size` -> `Dev/Test`
    - DB instance identifier (database-1; admin; 1-8#)
    - `Availability and durability` -> `Single DB Instance`

***

## 85. Connect Workbench to `MySQL` on `AWS`


***


### MySQL driver
  - go get github.com/go-sql-driver/mysql
  - [read the documentation](https://github.com/go-sql-driver/mysql#installation)
  - [see all SQL drivers](https://github.com/golang/go/wiki/SQLDrivers)
  - [Astaxie's book](https://astaxie.gitbooks.io/build-web-application-with-golang/content/en/05.2.html)

### Include the driver in your imports
  - _ "github.com/go-sql-driver/mysql"
  - [Read the documentation](https://github.com/go-sql-driver/mysql#usage)

### Determine the Data Source Name
  - user:password@tcp(localhost:5555)/dbname?charset=utf8
  - [Read the documentation](https://github.com/go-sql-driver/mysql#dsn-data-source-name)

### Open a connection
  - db, err := sql.Open("mysql", "user:password@tcp(localhost:5555)/dbname?charset=utf8")

[package sql](https://godoc.org/database/sql)

***

## 86. Go & SQL - Setup

* `godoc.org` -> search `sql`

* [SQL Drivers](https://github.com/golang/go/wiki/SQLDrivers)
* [Example Usage Patterns](https://github.com/golang/go/wiki/SQLInterface)

```
$ cd /Users/marshad/Desktop/golang-web-dev/032_rdbms/01_connect
$ go mod init 01_connect
$ go mod tidy

$ go run main.go
```

***

## 87. Go & SQL - In Practice

***
