## 42. Serving a file with `io.Copy`

***

## 43. Serving a file with `http.ServeContent` & `http.ServeFile`

***

## 44. Serving a file with `http.FileServer`

***

## 45. Serving a file with `http.FileServer` & `http.StripPrefix`

***

## 46. Creating a static file server with `http.FileServer`

***

## 47. `log.Fatal` & `http.Error`

***

## 48. Hands-on exercises

***

## 49. Hands-on exercises - solutions

***

## 50. The `http.NotFoundHandler`

***

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
