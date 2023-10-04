## 36. Understanding ServerMux

***

## 37. Disambiguation: `func(ResponseWriter, *Request)` vs `HandleFunc`

### HandleFunc

[http.HandleFunc](https://godoc.org/net/http#HandleFunc)
```go
func HandleFunc(pattern string, handler func(ResponseWriter, *Request))
```

* `http.HandleFunc` registers the handler function `handler func(ResponseWriter, *Request)` for the given pattern in the `DefaultServeMux`. The documentation for `ServeMux` explains how patterns are matched.

```go
package main

import (
    "io"
    "net/http"
)

func d(res http.ResponseWriter, req *http.Request) {
    io.WriteString(res, "dog dog dog")
}

func c(res http.ResponseWriter, req *http.Request) {
    io.WriteString(res, "cat cat cat")
}

func main() {

    http.HandleFunc("/dog", d)
    http.HandleFunc("/cat", c)

    http.ListenAndServe(":8080", nil)
}
```


### HandlerFunc

[http.HandlerFunc](https://godoc.org/net/http#HandlerFunc)
```go
type HandlerFunc func(ResponseWriter, *Request)
```

* The `http.HandlerFunc` type is an adapter to allow the use of ordinary functions as HTTP handlers. If f is a function with the appropriate signature, `http.HandlerFunc(f)` is a Handler that calls `f`.

```go
func (f HandlerFunc) ServeHTTP(w ResponseWriter, r *Request)
```

***

* Question: Could you get `http.Handle()` to take a `func()` with this signature: func(ResponseWriter, *Request)?

```go
package main

import (
    "io"
    "net/http"
)

func d(res http.ResponseWriter, req *http.Request) {
    io.WriteString(res, "dog dog dog")
}

func c(res http.ResponseWriter, req *http.Request) {
    io.WriteString(res, "cat cat cat")
}

func main() {

    http.Handle("/dog", http.HandlerFunc(d))                    # Conversion to handler
    http.Handle("/cat", http.HandlerFunc(c))

    http.ListenAndServe(":8080", nil)
}
```

***

## 38. Third-party servermux - julien schmidts's

***

## 39. Hands-on exercises

***

## 40. hands-on exercises - solutions #1

***

## 41. Hands-on exercises - solutions #2

***

