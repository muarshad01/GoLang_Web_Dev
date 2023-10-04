# Web Programming Synonymous Terms

- router
- request router
- multiplexer
- mux
- servemux
- server
---------------------
- http router
- http request router
- http multiplexer
- http mux
- http servemux
- http server

***

* `ServeMux` is an **HTTP request multiplexer*.

* A `ServeMux` matches the URL of each incoming request against a `list of registered patterns` and calls the handler for the pattern that most closely matches the URL.

*** 

# ServeMux

[http.ServeMux](https://godoc.org/net/http#ServeMux)
```go
type ServeMux
	func NewServeMux() *ServeMux
	func (mux *ServeMux) Handle(pattern string, handler Handler)
	func (mux *ServeMux) HandleFunc(pattern string, handler func(ResponseWriter, *Request))
	func (mux *ServeMux) Handler(r *Request) (h Handler, pattern string)
	func (mux *ServeMux) ServeHTTP(w ResponseWriter, r *Request)
```

* Any value of type `*http.ServeMux` implements the `http.Handler` interface.
* Remember, the `http.Handler` interface requires that a type have the `ServeHTTP()`method.

```go
type Handler interface {
    ServeHTTP(ResponseWriter, *Request)
}
```

* What this tells us is that we can pass a value of type `*http.ServeMux` into the `http.ListenAndServe()`

```go
func ListenAndServe(addr string, handler Handler) error
```

We can use `Handle`like this:
```go
	mux := http.NewServeMux()
	mux.Handle("/", h)
	mux.Handle("/cat", c)
```

* The overall game plan:
    - We will create a `NewServeMux()`
    - then attach the method `Handle()` to it to set routes, 
    - then pass our `*http.ServeMux` to `http.ListenAndServe()`.

*** 

# DefaultServeMux

`ListenAndServe()` starts an HTTP server with a given address and handler. 
The handler is usually `nil`, which means to use `DefaultServeMux`. 
`Handle()` and `type HandleFunc func()` add handlers to `DefaultServeMux`
```go
http.ListenAndServe(":8080", nil)
```

***
