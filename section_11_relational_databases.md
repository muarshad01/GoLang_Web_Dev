## 82. Overview

***

## 83. Installing MySQL - Locally

* [How To Download And Install MYSQL Server In Macbook M1](https://www.youtube.com/watch?v=aWZKws7RWic)

* Check if `MySQL` is installed

```
$ mysql
$ mysql -u root -p
```

* Install `MySQL` & `MySQL Workbench`

* [MySQL Community Downloads](https://dev.mysql.com/downloads/mysql/)
    - No thanks, just start my download.
    - Use Strong Password Encryption -> Next
    - Please enter a password for the "root" user: `1-8#`

* [MySQL Workbench](https://dev.mysql.com/downloads/workbench/)
    - No thanks, just start my download.

* Apple -> System Preferences -> search `mysql`

* `MySQL` access through command-line

```
$ vim ~/.bash_profile
export PATH=$PATH:/usr/local/mysql/bin              # Add to .bash_profile
$ source ~/.bash_profile
```

```
$ mysql -u root -p
Enter Password: 1-8#
mysql> show databases;
```
***

## 84. Installing `MySQL` - `AWS`

* `aws.amazon.com` -> My Account -> `AWS Management Console` 

* `Services` -> `RDS` -> `Create database`
    - `Choose a database creation method` -> `Standard Create`    
    - `Engine options` -> `MySQL`
    - `Edition` -> `MySQL Community`    
    - `Engine Version` -> `MySQL 8.0.33` 
    - `Templates` -> `Dev/Test`
    - `Availability and durability` -> `Single DB Instance`
    - `Settings`(test-db; admin; 1-8#)
    - `Instance configuration` -> Burstable classes(`db.t3.micro`)
    - `Storage` -> gp2(10)
    - `Connectivity` -> All default; public access (YES); VPC security group: Create new -> `test-db-group`
    - 
***

## 85. Connect Workbench to `MySQL` on `AWS`

***

## 86. Go & SQL - Setup

* `godoc.org` -> search `sql`

* [SQL Drivers](https://github.com/golang/go/wiki/SQLDrivers)
* [Example Usage Patterns](https://github.com/golang/go/wiki/SQLInterface)
    - [Astaxie's book](https://astaxie.gitbooks.io/build-web-application-with-golang/content/en/05.2.html)

```
$ cd /Users/marshad/Desktop/golang-web-dev/032_rdbms/01_connect
$ go mod init 01_connect
$ go mod tidy

$ go run main.go
```

```
// [username[:password]@][protocol[(address)]]/dbname[?param1=value1&...&paramN=valueN]
// db, err = sql.Open("mysql", "user   :password  @tcp(localhost                                            :5555)/dbname?charset=utf8")
// db, err = sql.Open("mysql", "awsuser:mypassword@tcp(mydbinstance.cakwl95bxza0.us-west-1.rds.amazonaws.com:3306)/test02?charset=utf8")
```

***

## 87. Go & SQL - In Practice

```
$ cd /Users/marshad/Desktop/golang-web-dev/032_rdbms/02_SQL
$ go mod init 02_SQL
$ go mod tidy

$ go run main.go
```
***
