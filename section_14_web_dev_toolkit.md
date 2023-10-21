## 101. Keyed-Hash Message Authentication Code (HMAC)

***

## 102. Base64 Encoding

***

## 103. Web Storage

***

## 104. Context

***

## 105. TLS & HTTPS

***

## 106. JSON - JavaScript Object Notation

***


## 107. Go and JSON - Marshal & Encode

[Encoding/JSON](https://pkg.go.dev/encoding/json)

* `godoc.org` -> Community -> Go Blog -> [JSON and Go](https://go.dev/blog/json)

* Marshal: Take a Go data structure -> Turn it into JSON -> Assign it to a variable

* Encode:  Take a Go data structure -> Turn it into JSON -> Send it over the wire

```go
type Decoder
    func NewDecoder(r io.Reader) *Decoder
    func (dec *Decoder) Decode(v any) error

type Encoder
    func NewEncoder(w io.Writer) *Encoder
    func (enc *Encoder) Encode(v any) error
```

```go
func Marshal(v any) ([]byte, error)
func Unmarshal(data []byte, v any) error
```

***

## 108. Unmarshal JSON with Go

***

## 109 Unmarshal JSON with Go using Tags

***

## 110. Hands-On Exercise Solution

***

## 111. AJAX Introduction

***

## 112. AJAX Server Side

***
