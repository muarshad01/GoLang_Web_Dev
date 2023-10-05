## 53. State overview

* State setup with `cookies`

***

## 54. Passing values through the URL

### Form Submissoion

* We can pass values from the `client` to the `server` through the `URL` or through the `body of the request`.

* When you submit a form, you can use either the `POST` or `GET` method. The `POST` method sends the form submission through the `body of the request`. The `GET` method for a form submission sends the form submission values through the `url`.

I remember this like this:
* `POST` and `Body` both have 4 letters
* `GET` and `URL` both have 3 letters

```
protocol://<subdomain>.<domain>:<port>/path?<identifier-1>=<value-1>&<identifier-2>=<value-2>#<fragment>
```

```
? is the query. You can have multiple identifiers and values
```

```
https://<video>.<google.co.uk>:80/docid=abcd&hl=en#00hasfds
```
### Retrieving values

While there are multiple ways to retrieve values, we will stick with:

[func (*Request) FormValue](https://godoc.org/net/http#Request.FormValue)
``` Go
func (r *Request) FormValue(key string) string
```

`http://localhost:8080/?q=dog`

***

## 55. Passing values from forms

***

## 56. Uploading a file, reading the file, creating a file on the server

***

## 57. `Enctype`

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


