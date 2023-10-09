## 66. Sessions

***

## 67. Universally unique identifier - `UUID`

```
$ cd /Users/marshad/Desktop/golang-web-dev/030_sessions/01_uuid
$ go mod init 01_uuid
$ go mod tidy
``` 

***

## 68. Your first session

```go
type User struct {
	UserName string
	First    string
	Last     string
}
```

* `Session` has `{session_id, user_id}`
* `user_id` -> determines a unique `User`

```
var dbSessions = map[string]string{}        # composite literal
var dbSessions = make(map[string]string)    # same effect as above
```
***


## 69. Sign-up

***

## 70. Encrypt password with `bcrypt`

***

## 71. Login

***

## 72. Logout

***

## 73. Permissions

***

## 74. Expire session

***
