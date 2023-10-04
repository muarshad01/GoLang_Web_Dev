### `ServeContent`

* [http.ServeContent](https://godoc.org/net/http#ServeContent)
```go
func ServeContent(w ResponseWriter, req *Request, name string, modtime time.Time, content io.ReadSeeker)
```

***

### `ServeFile`

* [http.ServeFile](https://godoc.org/net/http#ServeFile)
```go
func ServeFile(w ResponseWriter, r *Request, name string)
```

***

### `FileServer` & `StripPrefix`

* [http.FileServer](https://godoc.org/net/http#FileServer)
```go
func FileServer(root FileSystem) Handler
```

* [http.StripPrefix](https://godoc.org/net/http#StripPrefix)
```go
func StripPrefix(prefix string, h Handler) Handler
```

***

[log.Fatal](https://pkg.go.dev/log#Fatal)
```go
func Fatal(v ...any)
```

***

[http.Error](https://pkg.go.dev/net/http#Error)
```go
func Error(w ResponseWriter, error string, code int)
```

***



