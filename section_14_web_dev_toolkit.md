## 101. Keyed-Hash Message Authentication Code (HMAC)

***

## 102. Base64 Encoding

***

## 103. Web Storage

***

## 104. Context

What is the context of what I'm working with.

We can pass:
    - session_ids
    - user_ids
    - deadlines

* signal to other processes

* Context makes it possible to manage a `chain-of-calls` within the `same-call-path` by signaling context’s `Done` channel.

### Leaking goroutines

* [Using contexts to avoid leaking goroutines](https://rakyll.org/leakingctx/)

***

## 105. TLS & HTTPS

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
