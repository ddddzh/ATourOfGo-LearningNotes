# Exercise: Fibonacci closure

<https://go.dev/tour/moretypes/26>

## Requirements

Let's have some fun with functions.

Implement a fibonacci function that returns a function (a closure) that returns successive fibonacci numbers (0, 1, 1, 2, 3, 5, ...).

## Raw

```go
package main

import "fmt"

// fibonacci is a function that returns
// a function that returns an int.
func fibonacci() func() int {
}

func main() {
	f := fibonacci()
	for i := 0; i < 10; i++ {
		fmt.Println(f())
	}
}

```

## Solution

```go
package main

import "fmt"

// fibonacci is a function that returns
// a function that returns an int.
func fibonacci() func() int {
	var i1, i2 int

	return func() int {		
		if i2 == 0 {
			i2 = 1
			return 0
		}
		
		i1, i2 = i2, i1 + i2
		return i1
	}
}

func main() {
	f := fibonacci()
	for i := 0; i < 10; i++ {
		fmt.Println(f())
	}
}
```

```output
0
1
1
2
3
5
8
13
21
34

```
