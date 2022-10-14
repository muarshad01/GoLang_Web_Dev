# Writing a response

[io.Writer](https://pkg.go.dev/io#Writer)
```Go
type Writer interface {
	Write(p []byte) (n int, err error)
}
```
[io.WriteSgtring](https://pkg.go.dev/io#WriteString)
```Go
func WriteString(w Writer, s string) (n int, err error)
```
```Go
package main

import (
	"io"
	"log"
	"os"
)

func main() {
	if _, err := io.WriteString(os.Stdout, "Hello World"); err != nil {
		log.Fatal(err)
	}

}
```
[fmt.Fprintf](https://pkg.go.dev/fmt#Fprintf)
```Go
func Fprintf(w io.Writer, format string, a ...any) (n int, err error)
```
```Go

import (
	"fmt"
	"os"
)

func main() {
	const name, age = "Kim", 22
	n, err := fmt.Fprintf(os.Stdout, "%s is %d years old.\n", name, age)

	// The n and err return values from Fprintf are
	// those returned by the underlying io.Writer.
	if err != nil {
		fmt.Fprintf(os.Stderr, "Fprintf: %v\n", err)
	}
	fmt.Printf("%d bytes written.\n", n)

}
```
[fmt.Fprint](https://pkg.go.dev/fmt#Fprint)
```Go
func Fprint(w io.Writer, a ...any) (n int, err error)
```
```Go
package main

import (
	"fmt"
	"os"
)

func main() {
	const name, age = "Kim", 22
	n, err := fmt.Fprint(os.Stdout, name, " is ", age, " years old.\n")

	// The n and err return values from Fprint are
	// those returned by the underlying io.Writer.
	if err != nil {
		fmt.Fprintf(os.Stderr, "Fprint: %v\n", err)
	}
	fmt.Print(n, " bytes written.\n")

}
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
```Go
package main

import (
	"fmt"
	"strings"
)

func main() {
	fmt.Printf("Fields are: %q", strings.Fields("  foo bar  baz   "))
}

```
