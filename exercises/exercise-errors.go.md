# Exercise: Errors

<https://go.dev/tour/methods/20>

## Requirements

Copy your `Sqrt` function from the earlier exercise and modify it to return an error value.

`Sqrt` should return a non-nil error value when given a negative number, as it doesn't support complex numbers.

Create a new type

```go
type ErrNegativeSqrt float64
```

and make it an `error` by giving it a

```go
func (e ErrNegativeSqrt) Error() string
```

method such that `ErrNegativeSqrt(-2).Error()` returns `"cannot Sqrt negative number: -2"`.

Note: A call to `fmt.Sprint(e)` inside the Error method will send the program into an infinite loop. You can avoid this by converting `e` first: `fmt.Sprint(float64(e))`. Why?

Change your `Sqrt` function to return an `ErrNegativeSqrt` value when given a negative number.

## Raw

```go
package main

import (
	"fmt"
)

func Sqrt(x float64) (float64, error) {
	return 0, nil
}

func main() {
	fmt.Println(Sqrt(2))
	fmt.Println(Sqrt(-2))
}
```

## Solution

```go
package main

import (
	"fmt"
)

type ErrNegativeSqrt float64

func (e ErrNegativeSqrt) Error() string {
	return "baaaad"
}

func Sqrt(x float64) (float64, error) {
	if x < 0 {
		return -666, ErrNegativeSqrt(x)
	}
	
	return 0, nil
}

func main() {
	fmt.Println(Sqrt(2))
	fmt.Println(Sqrt(-2))
}

```

```output
0 <nil>
-666 baaaad
```
