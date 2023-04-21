# Exercise: Readers

<https://go.dev/tour/methods/22>

## Requirements

Implement a `Reader` type that emits an infinite stream of the ASCII character `'A'`.

## Raw

```go
package main

import "golang.org/x/tour/reader"

type MyReader struct{}

// TODO: Add a Read([]byte) (int, error) method to MyReader.

func main() {
	reader.Validate(MyReader{})
}

```

## Solution

```go
package main

import "golang.org/x/tour/reader"

type MyReader struct{}

func (reader MyReader) Read(buffer []byte) (int, error) {
	size := len(buffer)
	for i := 0; i < size; i++ {
		buffer[i] = 'A'
	}
	
	return size, nil
}


func main() {
	reader.Validate(MyReader{})
}
```

```output
OK!

```
