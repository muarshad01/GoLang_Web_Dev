# HandleFunc

[http.HandleFunc](https://godoc.org/net/http#HandleFunc)
```go
func HandleFunc(pattern string, handler func(ResponseWriter, *Request))
```
* `http.HandleFunc` registers the handler function for the given pattern in the `DefaultServeMux`. The documentation for `ServeMux` explains how patterns are matched.

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
