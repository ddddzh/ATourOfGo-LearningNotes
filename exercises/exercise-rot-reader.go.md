# Exercise: rot13Reader

<https://go.dev/tour/methods/23>

## Requirements

A common pattern is an `io.Reader` that wraps another `io.Reader`, modifying the stream in some way.

For example, the `gzip.NewReader` function takes an `io.Reader` (a stream of compressed data) and returns a `*gzip.Reader` that also implements `io.Reader` (a stream of the decompressed data).

Implement a `rot13Reader` that implements `io.Reader` and reads from an `io.Reader`, modifying the stream by applying the `rot13` substitution cipher to all alphabetical characters.

The rot13Reader type is provided for you. Make it an `io.Reader` by implementing its Read method.

## Raw

```go
package main

import (
	"io"
	"os"
	"strings"
)

type rot13Reader struct {
	r io.Reader
}

func main() {
	s := strings.NewReader("Lbh penpxrq gur pbqr!")
	r := rot13Reader{s}
	io.Copy(os.Stdout, &r)
}

```

## Solution

```go
package main

import (
	"io"
	"os"
	"strings"
)

type incorrectByteError byte

func (e incorrectByteError) Error() string {
	return "is not a letter"
}

type rot13Reader struct {
	r io.Reader
}

func (r rot13Reader) Read(buf []byte) (int, error) {
	n, err := r.Read(buf)

	if err != nil {
		return 0, err
	}

	for i := 0; i < n; i++ {
		//		var newByte byte
		//		var e error
		newByte, err := convertsByte(buf[i])

		if err != nil {
			return 0, err
		}

		buf[i] = newByte
	}

	return len(buf), nil
}

func convertsByte(b byte) (byte, error) {
	if b >= 'A' && b <= 'Z' {
		b += 13

		if b > 'Z' {
			b -= ('Z' - 'A')
		}

		return b, nil
	}

	if b >= 'a' || b <= 'z' {
		b += 13

		if b > 'z' {
			b -= ('z' - 'a')
		}

		return b, nil
	}

	return 0, incorrectByteError(b)
}

func main() {
	s := strings.NewReader("Lbh penpxrq gur pbqr!")
	r := rot13Reader{s}
	io.Copy(os.Stdout, &r)
}

```

```output


```
