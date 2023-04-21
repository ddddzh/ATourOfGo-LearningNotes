# Go Tutorial

<https://go.dev/tour>

## Packages, variables, and functions

### Package

```go
package main
```

### Imports

```go
import (
    "fmt"
    "math"
)
```

### Functions

```go
func add(x int, y int) int {
    return x + y
}

func add(x, y int) int {
    return x + y
}
```

```go
func name(a type, b type, c type) (return_type, return_type, return_type) {
    //...
}

func swap(x, y string) (string, string) {
    return y, x
}
```

### Vairables

```go
var variable_name VairableType

var c, python, java bool
```

#### Initialization

```go
var variable_name VairableType

variable_name = value

var i, j int = 1, 2
```

```go
variable_name := value

k := 3
```

#### Basic Types and Zero Values

- `bool`
  - `false`
- `string`
  - `""`
- `int`
  - 0
- `uint`
  - 0
- `float32`
  - 0
- `float64`
  - 0
- `complex64`
  - 0
- `complex128`
  - 0

#### Type Conversion

```go
a = int(b)
```

### Constants

```go
const Pi = 3.14

const (
    // Create a huge number by shifting a 1 bit left 100 places.
    // In other words, the binary number that is 1 followed by 100 zeroes.
    Big = 1 << 100
    // Shift it right again 99 places, so we end up with 1<<1, or 2.
    Small = Big >> 99
)
```

## Flow control statements: for, if, else, switch and defer

### for

```go
// regular
for i := 0; i < n; i++ {
    // ...
}

// while
for count < 100 {
    // ...
}

// forever loop
for {
    // ...
}
```

### if

```go
// regular
if x < 0 {
    // ...
}

// with short statement
if x := GetX(); x < 0 {
    // ...
}

// if...else...
if x := GetX(); x < 0 {
    // ...
} else {
    // ...
}
```

### switch

```go
// with condition
os = //...
switch os {
case "darwin":
    //...
case "linux":
    //...
default:
    //...
}

// with short statement and condition
switch os:= runtime.GOOS; os {
case "darwin":
    //...
case "linux":
    //...
default:
    //...
}

// without condition
t := time.Now()

switch {
case t.Hour() < 12:
    //...
case t.Hour() < 17:
    //...
default:
    //...
}
```

#### Evaluation order

by coding order, automatic integrate `break` in each case

### Defer

execute after function returns, stacked as LIFO

```go
func main() {
    defer fmt.Println("world")

    fmt.Println("hello")
}
```

## More types: structs, slices, and maps

### Pointers

```go
var p *int
```

#### Reference

```go
var i int = 42
p := &i         // point to i
fmt.Println(*p) // read i through the pointer
*p = 21         // set i through the pointer
fmt.Println(i)  // see the new value of i
```

#### DeReference

```go
p = &j         // point to j
*p = *p / 37   // divide j through the pointer
fmt.Println(j) // see the new value of j
```

### Struct

```go
type Vertex struct {
    X int
    Y int
}

v := Vertex{1, 2}
v.X = 4
fmt.Println(v.X)

p := &v
p.X = 1e9
fmt.Println(v.X, v.Y, v, *p, p)
```

#### Literal

```go
var (
 v1 = Vertex{1, 2}  // has type Vertex
 v2 = Vertex{X: 1}  // Y:0 is implicit
 v3 = Vertex{}      // X:0 and Y:0
 p  = &Vertex{1, 2} // has type *Vertex
)
```

### Arrays

```go
var a [2]string
a[0] = "Hello"
a[1] = "World"
fmt.Println(a[0], a[1])
fmt.Println(a)
```

#### Literal

```go
a := [3]bool{true, true, false}
```

### Slices

```go
primes := [6]int{2, 3, 5, 7, 11, 13}

var s []int = primes[1:4]
fmt.Println(s)
```

#### Literal

```go
q := []int{2, 3, 5, 7, 11, 13}
fmt.Println(q)

r := []bool{true, false, true, true, false, true}
fmt.Println(r)

s := []struct {
    i int
    b bool
}{
    {2, true},
    {3, false},
    {5, true},
    {7, true},
    {11, false},
    {13, true},
}
fmt.Println(s)
```

#### Defaults

```go
var a [10]int

// same slice
a[0:10]
a[:10]
a[0:]
a[:]
```

#### Length and Capacity

```go
s := []int{2, 3, 5, 7, 11, 13}
printSlice(s)

// Slice the slice to give it zero length.
s = s[:0]
printSlice(s)

// Extend its length.
s = s[:4]
printSlice(s)

// Drop its first two values.
s = s[2:7]

len(s)
cap(s)
```

#### Create with `make`

```go
make(slice type, length, capacity)

a := make([]int, 5)
printSlice("a", a)

b := make([]int, 0, 5)
printSlice("b", b)

c := b[:2]
printSlice("c", c)

d := c[2:5]
printSlice("d", d)
```

```txt
a len=5 cap=5 [0 0 0 0 0]
b len=0 cap=5 []
c len=2 cap=5 [0 0]
d len=3 cap=3 [0 0 0]
```

#### Appending

```go
var s []int
printSlice(s)

// append works on nil slices.
s = append(s, 0)
printSlice(s)

// The slice grows as needed.
s = append(s, 1)
printSlice(s)

// We can add more than one element at a time.
s = append(s, 2, 3, 4)
printSlice(s)
```

```txt
len=0 cap=0 []
len=1 cap=1 [0]
len=2 cap=2 [0 1]
len=5 cap=6 [0 1 2 3 4]
```

#### Range

```go
var pow = []int{1, 2, 4, 8, 16, 32, 64, 128}

for i, v := range pow {
    fmt.Printf("2**%d = %d\n", i, v)
}
```

### Maps

#### Initialization

```go
m = make(map[string]int)
```

#### Literals

```go
type Vertex struct {
    Lat, Long float64
}

var m = map[string]Vertex{
    "Bell Labs": Vertex{
        40.68433, -74.39967,
    },
    "Google": Vertex{
        37.42202, -122.08408,
    },
}

var m = map[string]Vertex{
    "Bell Labs": {40.68433, -74.39967},
    "Google":    {37.42202, -122.08408},
}
```

#### Mutating

```go
m := make(map[string]int)

// Create, Update
m["Answer"] = 42
fmt.Println("The value:", m["Answer"])

m["Answer"] = 48
fmt.Println("The value:", m["Answer"])

// Delete
delete(m, "Answer")
fmt.Println("The value:", m["Answer"])

// Read
v, ok := m["Answer"]
fmt.Println("The value:", v, "Present?", ok)

if !ok {
    fmt.Println("doesn't have it!")
} else {
    fmt.Println("we have it!")
}
```

### Function Values

```go
func compute(fn func(float64, float64) float64) float64 {
    return fn(3, 4)
}

hypot := func(x, y float64) float64 {
    return math.Sqrt(x*x + y*y)
}
fmt.Println(hypot(5, 12))

fmt.Println(compute(hypot))
fmt.Println(compute(math.Pow))
```

```txt
13
5
81
```

## Methods and interfaces

### Methods

#### Receiver

```go
type Vertex struct {
    X, Y float64
}

func (v Vertex) Abs() float64 {
    return math.Sqrt(v.X*v.X + v.Y*v.Y)
}
```

```go
type MyFloat float64

func (f MyFloat) Abs() float64 {
    if f < 0 {
        return float64(-f)
    }
    return float64(f)
}
```

#### Pointer Receiver

``` go
func (v Vertex) Abs() float64 {
    return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

// Only pointer receiver can change its values
func (v *Vertex) Scale(f float64) {
    v.X = v.X * f
    v.Y = v.Y * f
}
```

### Interface

Interface is used to define a collection of types that all have one specific method

```go
type Abser interface {
    Abs() float64
}

type MyFloat float64

func (f MyFloat) Abs() float64 {
    if f < 0 {
        return float64(-f)
    }
    return float64(f)
}

type Vertex struct {
    X, Y float64
}

func (v *Vertex) Abs() float64 {
    return math.Sqrt(v.X*v.X + v.Y*v.Y)
}
```

#### Type Assertions

```go
var i interface{} = "hello"

s := i.(string)
fmt.Println(s)

s, ok := i.(string)
fmt.Println(s, ok)

f, ok := i.(float64)
fmt.Println(f, ok)

f = i.(float64) // panic
fmt.Println(f)
```

```txt
hello
hello true
0 false
panic: interface conversion: interface {} is string, not float64
```

#### Type Switches

```go
switch v := i.(type) {
case T:
    // here v has type T
case S:
    // here v has type S
default:
    // no match; here v has the same type as i
}
```

### Errors

```go
type error interface {
    Error() string
}

// Example error implementation
type MyError struct {
    When time.Time
    What string
}

func (e *MyError) Error() string {
    return fmt.Sprintf("at %v, %s",
        e.When, e.What)
}
```

### Readers

```go
func (T) Read(b []byte) (n int, err error)
```

```go
r := strings.NewReader("Hello, Reader!")

b := make([]byte, 8)
for {
    n, err := r.Read(b)
    fmt.Printf("n = %v err = %v b = %v\n", n, err, b)
    fmt.Printf("b[:n] = %q\n", b[:n])
    if err == io.EOF {
        break
    }
}
```

### Images

```go
package image

type Image interface {
    ColorModel() color.Model
    Bounds() Rectangle
    At(x, y int) color.Color
}
```

## Generics

### Type Parameters

```go
func Index[T comparable](s []T, x T) int
```

```go
// Index returns the index of x in s, or -1 if not found.
func Index[T comparable](s []T, x T) int {
    for i, v := range s {
        // v and x are type T, which has the comparable
        // constraint, so we can use == here.
        if v == x {
            return i
        }
    }
    return -1
}
```

### Generic types

```go
// List represents a singly-linked list that holds
// values of any type.
type List[T any] struct {
    next *List[T]
    val  T
}

head := List[int]{nil, 0}
node := &head

for i := 1; i < 10; i++ {
    node.next = &List[int]{nil, i}
    node = node.next
}

node = &head
for node != nil {
    fmt.Println(node)
    node = node.next
}
```

## Concurrency

### Goroutines

```go
f(x, y, z)

go f(x, y, z)
```

### Channels

```go
ch := make(chan int)

ch <- v    // Send v to channel ch.
v := <-ch  // Receive from ch, and assign value to v.
```

### Buffered Channels

```go
ch := make(chan int, 10)
for i := 0; i < 10; i++ {
    ch <- i
    fmt.Printf("channel len=%d\n", len(ch))
}


for i := 0; i < 10; i++ {
    <- ch
    fmt.Printf("channel len=%d\n", len(ch))
}
```

```output
channel len=1
channel len=2
channel len=3
channel len=4
channel len=5
channel len=6
channel len=7
channel len=8
channel len=9
channel len=10
channel len=9
channel len=8
channel len=7
channel len=6
channel len=5
channel len=4
channel len=3
channel len=2
channel len=1
channel len=0
```

### Range and Close

```go
func fibonacci(n int, c chan int) {
    x, y := 0, 1
    for i := 0; i < n; i++ {
        c <- x
        x, y = y, x+y
    }
    close(c)
}

func main() {
    c := make(chan int, 10)
    go fibonacci(cap(c), c)
    for i := range c {
        fmt.Println(i)
    }
}
```

### Select

```go
func fibonacci(c, quit chan int) {
    x, y := 0, 1
    for {
        select {
        case c <- x:
            x, y = y, x+y
        case <-quit:
            fmt.Println("quit")
            return
        }
    }
}
```

### Select Default

```go
tick := time.Tick(100 * time.Millisecond)
boom := time.After(500 * time.Millisecond)
for {
    select {
    case <-tick:
        fmt.Println("tick.")
    case <-boom:
        fmt.Println("BOOM!")
        return
    default:
        fmt.Println("    .")
        time.Sleep(50 * time.Millisecond)
    }
}
```

```output
    .
    .
    .
tick.
    .
tick.
    .
    .
tick.
    .
    .
tick.
    .
    .
tick.
BOOM!
```

### sync.Mutex

```go
// SafeCounter is safe to use concurrently.
type SafeCounter struct {
    mu sync.Mutex
    v  map[string]int
}

// Inc increments the counter for the given key.
func (c *SafeCounter) Inc(key string) {
    c.mu.Lock()
    // Lock so only one goroutine at a time can access the map c.v.
    c.v[key]++
    c.mu.Unlock()
}

// Value returns the current value of the counter for the given key.
func (c *SafeCounter) Value(key string) int {
    c.mu.Lock()
    // Lock so only one goroutine at a time can access the map c.v.
    defer c.mu.Unlock()
    return c.v[key]
}
```
