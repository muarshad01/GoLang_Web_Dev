# HMAC

***

[hash.Hash](https://pkg.go.dev/hash#Hash)
```go

type Hash interface {
	// Write (via the embedded io.Writer interface) adds more data to the running hash.
	// It never returns an error.
	io.Writer

	// Sum appends the current hash to b and returns the resulting slice.
	// It does not change the underlying hash state.
	Sum(b []byte) []byte

	// Reset resets the Hash to its initial state.
	Reset()

	// Size returns the number of bytes Sum will return.
	Size() int

	// BlockSize returns the hash's underlying block size.
	// The Write method must be able to accept any amount
	// of data, but it may operate more efficiently if all writes
	// are a multiple of the block size.
	BlockSize() int
}
```

***
[encoding/base64](https://pkg.go.dev/encoding/base64#pkg-index)
```go
type Encoding
func NewEncoding(encoder string) *Encoding
func (enc *Encoding) Decode(dst, src []byte) (n int, err error)
func (enc *Encoding) DecodeString(s string) ([]byte, error)
func (enc *Encoding) DecodedLen(n int) int
func (enc *Encoding) Encode(dst, src []byte)
func (enc *Encoding) EncodeToString(src []byte) string
func (enc *Encoding) EncodedLen(n int) int
func (enc Encoding) Strict() *Encoding
func (enc Encoding) WithPadding(padding rune) *Encoding
```
