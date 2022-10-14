# Writing a response

[type Writer](https://pkg.go.dev/io#Writer)
```Go
type Writer interface {
	Write(p []byte) (n int, err error)
}
```
[io.WriteSgtring](https://pkg.go.dev/io#WriteString)
```Go
func WriteString(w Writer, s string) (n int, err error)
```
[fmt.Fprintf](https://pkg.go.dev/fmt#Fprintf)
```Go
func Fprintf(w io.Writer, format string, a ...any) (n int, err error)
```
[fmt.Fprint](https://pkg.go.dev/fmt#Fprint)
```Go
func Fprint(w io.Writer, a ...any) (n int, err error)
```

```Go
body := "CHECK OUT THE RESPONSE BODY PAYLOAD"
io.WriteString(conn, "HTTP/1.1 200 OK\r\n") 			// status line
fmt.Fprintf(conn, "Content-Length: %d\r\n", len(body)) 		// header
fmt.Fprint(conn, "Content-Type: text/plain\r\n") 		// header
io.WriteString(conn, "\r\n") 					// blank line; CRLF; carriage-return line-feed
io.WriteString(conn, body) 					// body, aka, payload
```

***

# Useful for parsing the request-line & status-line

## Parsing String

[strings.Fields](https://godoc.org/strings#Fields)

```Go
func Fields(s string) []string
```
