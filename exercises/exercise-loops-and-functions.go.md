# Exercise: Loops and Functions

<https://go.dev/tour/flowcontrol/8>

## Requirements

As a way to play with functions and loops, let's implement a square root function: given a number x, we want to find the number z for which z² is most nearly x.

Computers typically compute the square root of x using a loop. Starting with some guess z, we can adjust z based on how close z² is to x, producing a better guess:

```go
z -= (z*z - x) / (2*z)
```

Repeating this adjustment makes the guess better and better until we reach an answer that is as close to the actual square root as can be.

Implement this in the func Sqrt provided. A decent starting guess for z is 1, no matter what the input. To begin with, repeat the calculation 10 times and print each z along the way. See how close you get to the answer for various values of x (1, 2, 3, ...) and how quickly the guess improves.

Hint: To declare and initialize a floating point value, give it floating point syntax or use a conversion:

```go
z := 1.0
z := float64(1)
```

Next, change the loop condition to stop once the value has stopped changing (or only changes by a very small amount). See if that's more or fewer than 10 iterations. Try other initial guesses for z, like x, or x/2. How close are your function's results to the math.Sqrt in the standard library?

(**Note**: If you are interested in the details of the algorithm, the z² − x above is how far away z² is from where it needs to be (x), and the division by 2z is the derivative of z², to scale how much we adjust z by how quickly z² is changing. This general approach is called Newton's method. It works well for many functions but especially well for square root.)

## Raw

```go
package main

import (
	"fmt"
)

func Sqrt(x float64) float64 {
}

func main() {
	fmt.Println(Sqrt(2))
}
```

## Solution

```go
package main

import (
	"fmt"
	"math"
)

const limit = 0.00000000000001

func Sqrt(x float64) float64 {
	z := 1.0
	zSquare := z*z
	for diff := x - zSquare; diff > limit; diff = math.Abs(x - zSquare) {
		z -= (z*z - x) / (2*z)
		zSquare = z*z
		fmt.Printf("z=%g, z^2=%g, diff=%g\n",z, zSquare, diff)
	}
	
	fmt.Printf("z=%g, z^2=%g, diff=%g\n",z, zSquare, math.Abs(x - zSquare))
	return z
}

func main() {
	fmt.Println(Sqrt(2))
}
```

```output
z=1.5, z^2=2.25, diff=1
z=1.4166666666666667, z^2=2.0069444444444446, diff=0.25
z=1.4142156862745099, z^2=2.000006007304883, diff=0.006944444444444642
z=1.4142135623746899, z^2=2.0000000000045106, diff=6.007304882871267e-06
z=1.4142135623730951, z^2=2.0000000000000004, diff=4.510614104447086e-12
z=1.4142135623730951, z^2=2.0000000000000004, diff=4.440892098500626e-16
1.4142135623730951
```
