## 53. State overview

* State setup with `cookies`

***

## 54. Passing values through the URL

### `Form` Submission

* We can pass values from the `client` to the `server` through the `URL` or through the `request body's payload`.

* When you submit a `form`, you can use either the `POST` or `GET` method. 
```
<form method="POST">
    <input type="submit">
</form>
```
* If `form` method attribute is `POST`, then the values of the `form` are send to the server through `request body's payload`. 

```
<form method="GET">
    <input type="submit">
</form>
```
* If `form` method attributed is `GET`, then the value of the `form` are send to the server through the `URL`.

* I remember this like this:
    - `POST` and `Body` both have 4 letters
    - `GET` and `URL` both have 3 letters

```
protocol://<subdomain>.<domain>:<port>/path?<identifier-1>=<value-1>&<identifier-2>=<value-2>#<fragment>
```
* `?` is the query. You can have multiple identifiers and values
```
https://<video>.<google.co.uk>:80/docid=abcd&hl=en#00hasfds
```

### Retrieving values

[func (*Request) FormValue](https://godoc.org/net/http#Request.FormValue)
``` Go
func (r *Request) FormValue(key string) string
```

`http://localhost:8080/?q=dog`

***

## 55. Passing values from forms

***

## 56. Uploading a file, reading the file, creating a file on the server

[request.FormFile](https://pkg.go.dev/net/http#Request.FormFile)
```go
func (r *Request) FormFile(key string) (multipart.File, *multipart.FileHeader, error)
```

```
<form method="POST" enctype="multipart/form-data">
    <input type="file" name="q">
    <input type="submit">
</form>
```

* Note: type="file"

* enctype="multipart/form-data"

***

## 57. `Enctype`

* `enctype="application/x-www-form-urlencoded"`     
* `enctype="multipart/form-data"`                       # If a `form` contains `<input type="file">`
* `enctype="text/plain"`

***

## 58. Redirects - overview

***

## 59. Redirects - diagrams & documentation

***

## 60. Redirects - in practice

***

## 61. Cookies - overview

***

## 62. Cookies - writing and reading

***

## 63. Writing multiple cookies & hands-on exercises

***

## 64. Hands-on exercise solution: creating a counter with cookies

***

## 65. Deleting a cookie

***


