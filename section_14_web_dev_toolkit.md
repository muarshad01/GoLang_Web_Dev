## 101. Keyed-Hash Message Authentication Code (HMAC)

* [crypto/hmac](https://pkg.go.dev/crypto/hmac)

```go
func getCode(s string) string {
	h := hmac.New(sha256.New, []byte("ourkey"))
	io.WriteString(h, s)
	return fmt.Sprintf("%x", h.Sum(nil))
}
```

***

## 102. Base64 Encoding

[encoding/base64](https://pkg.go.dev/encoding/base64#pkg-index)
```go
type Encoding
    func NewEncoding(encoder string) *Encoding
    func (enc *Encoding) EncodeToString(src []byte) string
```

```go
s := "Hello"
encodeStd := "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/"
s64 := base64.NewEncoding(encodeStd).EncodeToString([]byte(s))

OR

s64 :=     base64.StdEncoding.EncodeToString([]byte(s))

bs, err := base64.StdEncoding.DecodeString(s64)

```

***

## 103. Web Storage

* DevTools -> Application -> Storage
    - Local storage 
    - Session storage 
    - Cookies

***

## 104. Context

[context](https://pkg.go.dev/context)

* What is the context of what I'm working with.

* We can pass:
    - session_ids
    - user_ids
    - deadlines

* Signal to other processes

* Context makes it possible to manage a `chain-of-calls` within the `same-call-path` by signaling context’s `Done` channel.

### Leaking goroutines

* [Using contexts to avoid leaking goroutines](https://rakyll.org/leakingctx/)

***

## 105. TLS & HTTPS

* Transport Layer Security (TLS)
* Secure Socket Layer (SSL) 

```go
func ListenAndServe(addr string, handler Handler) error
func ListenAndServeTLS(addr, certFile, keyFile string, handler Handler) error
```

```
$ vim ~/.bash_profile

export GOROOT=/usr/local/go
export GOPATH=$HOME/goworkspace
export GOBIN=$GOPATH/bin
export PATH=$PATH:$GOPATH/bin
export GO111MODULE="on"

$ source ~/.bash_profile
```

```
$ cd $GOROOT
$ pwd
--/usr/local/go

$ sudo go run /usr/local/go/src/crypto/tls/generate_cert.go --host=localhost
-- 2023/10/22 11:55:00 wrote cert.pem
-- 2023/10/22 11:55:00 wrote key.pem
```

```
`https://localhost:10443/` or `https://127.0.0.1:10443/`
```

***

## 106. JSON - JavaScript Object Notation

***


## 107. Go and JSON - `Marshal` & `Encode`

[Encoding/JSON](https://pkg.go.dev/encoding/json)

* `godoc.org` -> Community -> Go Blog -> [JSON and Go](https://go.dev/blog/json)

```go
func Marshal(v any) ([]byte, error)
```
* `Marshal`: Take a Go data structure -> Turn it into JSON -> Assign it to a variable

```go
type Encoder
    func NewEncoder(w io.Writer) *Encoder
    func (enc *Encoder) Encode(v any) error
```
* `Encode`:  Take a Go data structure -> Turn it into JSON -> Send it over the wire

***

## 108. `Unmarshal` JSON with Go

[Convert JSON to Go Instantly](https://mholt.github.io/json-to-go/)


```go
func Unmarshal(data []byte, v any) error
```
* `Unmarshal` parses the JSON-encoded data and stores the result in the `value pointed to by v`, i.e., `v` need to be a pointer.

```go
type Decoder
    func NewDecoder(r io.Reader) *Decoder
    func (dec *Decoder) Decode(v any) error
```
* `Decode` reads the next JSON-encoded value from its input and stores it in the `value pointed to by v`, i.e., `v` needs to be a pointer.

***

## 109 Unmarshal JSON with Go using Tags

***

## 110. Hands-On Exercise Solution

***

## 111. AJAX Introduction

* `AJAX` - Asynchronous JavaScript and XML

Allows Browser to communicate with the Server without reloading the entire page.

***

## 112. AJAX Server Side

***
