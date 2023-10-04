## 29. `net/http` package - an overview

***

## 30. Understanding & using `ListenAndServe`

***

## 31. Foundation of `net/http: Handler`, `ListenAndServer`, `Request`, `ResponseWriter`

***

## 32. Retrieving from values - exploring `*http.Request`

***

## 33. Retrieving other request values - exploring `*http.Request`

***

## 34. Exploring `http.ResponseWriter` - writing headers to the response

***

## 35. Review

***

***

## Handler Interface

[http.Handler](https://godoc.org/net/http#Handler)
``` Go
type Handler interface {
    ServeHTTP(ResponseWriter, *Request)
}
```

``` Go
package main

import (
	"fmt"
	"net/http"
)

type hotdog int

func (m hotdog) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintln(w, "Any code you want in this func")
}

func main() {
	var d hotdog
	http.ListenAndServe(":8080", d)
}
```

* Any other type(e.g., hotdog) which has `ServeHTTP(w http.ResponseWriter, r *http.Request)` method is also of `type Handler`. 

* It implicitly implements a `http.Handler` interface.

***

# Server

[http.ListenAndServe](https://godoc.org/net/http#ListenAndServe)
```go
func ListenAndServe(addr string, handler Handler) error
```

[http.ListenAndServeTLS](https://godoc.org/net/http#ListenAndServeTLS)
```go
func ListenAndServeTLS(addr, certFile, keyFile string, handler Handler) error
```

* Notice that both of the above functions take a `http.Handler`

***

## `http.Request`

[http.Request](https://godoc.org/net/http#Request) with most of the comments and some of the fields stripped out:

```go 
type Request struct {
    Method string
    URL *url.URL
	//	Header = map[string][]string{
	//		"Accept-Encoding": {"gzip, deflate"},
	//		"Accept-Language": {"en-us"},
	//		"Foo": {"Bar", "two"},
	//	}
    Header Header
    Body io.ReadCloser
    ContentLength int64
    Host string
    // This field is only available after ParseForm is called.
    Form url.Values
    // This field is only available after ParseForm is called.
    PostForm url.Values
    MultipartForm *multipart.Form
    // RemoteAddr allows HTTP servers and other software to record
	// the network address that sent the request, usually for
	// logging. 
    RemoteAddr string
}
```

* [http.Request](https://godoc.org/net/http#Request) type is a `struct`. It has has a `Method string` field.

* [http.Request](https://godoc.org/net/http#Request) type is a `struct`. 
    - It has `Form url.Values` & `PostForm url.Values` fields. If we read the documentation on these, we'll see:
```go
    // Form contains the parsed form data, including both the URL
    // field's query parameters and the POST or PUT form data.
    // This field is only available after **ParseForm** is called.
    // The HTTP client ignores Form and uses Body instead.
    Form url.Values

    // PostForm contains the parsed form data from POST, PATCH,
    // or PUT body parameters.
    // This field is only available after **ParseForm** is called.
    // The HTTP client ignores PostForm and uses Body instead.
    PostForm url.Values

```

`Form` & `PostForm` fields are available after [ParseForm](https://pkg.go.dev/net/http#Request.ParseForm) method, which is attached to `*http.Request`
```go 
func (r *Request) ParseForm() error
```

* If we look at [FormValue](https://pkg.go.dev/net/http#Request.FormValue)
```go 
func (r *Request) FormValue(key string) string
```
we see that this is a method attached to a `*http.Request`. `FormValue` returns the first value for the named component of the query. `POST` and `PUT` body parameters take precedence over `URL` query string values. `FormValue` calls `ParseMultipartForm` and `ParseForm` if necessary and ignores any errors returned by these functions. If key is not present, `FormValue` returns the empty string. To access multiple values of the same key, call `ParseForm` and then inspect `Request Form` directly.

* The `http.Request` type is a `struct`, which has a [url.URL](https://pkg.go.dev/net/url#URL) field. Notice that the type is `*url.URL`
``` go
type URL struct {
    Scheme     string
    Opaque     string    // encoded opaque data
    User       *Userinfo // username and password information
    Host       string    // host or host:port
    Path       string
    RawPath    string // encoded path hint (Go 1.5 and later only; see EscapedPath method)
    ForceQuery bool   // append a query ('?') even if RawQuery is empty
    RawQuery   string // encoded query values, without '?'
    Fragment   string // fragment for references, without '#'
}
```

* The `http.Request` type is a `struct`, which has a [http.Header](https://pkg.go.dev/net/http#Header) field
```go
type Header map[string][]string
```

***

## `http.ResponseWriter`

[http.ResponseWriter](https://godoc.org/net/http#ResponseWriter)
```go
type ResponseWriter interface {
    // Header returns the header map that will be sent by
    // WriteHeader. Changing the header after a call to
    // WriteHeader (or Write) has no effect 
    Header() Header

    // Write writes the data to the connection as part of an HTTP reply.
    //
    // If WriteHeader has not yet been called, Write calls
    // WriteHeader(http.StatusOK) before writing the data. If the Header
    // does not contain a Content-Type line, Write adds a Content-Type set
    // to the result of passing the initial 512 bytes of written data to
    // DetectContentType.
    Write([]byte) (int, error)

    // WriteHeader sends an HTTP response header with status code.
    // If WriteHeader is not called explicitly, the first call to Write
    // will trigger an implicit WriteHeader(http.StatusOK).
    // Thus explicit calls to WriteHeader are mainly used to
    // send error codes.
    WriteHeader(int)
}
```

[http.ResponseWriter](https://pkg.go.dev/net/http#ResponseWriter) has a method `Header() Header`, which returns a `http.Header`.
```go
type Header map[string][]string
```

List of methods attached to type `http.Header`:
```go
type Header
func (h Header) Add(key, value string)
func (h Header) Del(key string)
func (h Header) Get(key string) string
func (h Header) Set(key, value string)
func (h Header) Write(w io.Writer) error
func (h Header) WriteSubset(w io.Writer, exclude map[string]bool) error
```

We can set headers for a response like this:
```go
res.Header().Set("Content-Type", "text/html; charset=utf-8")
```

***
