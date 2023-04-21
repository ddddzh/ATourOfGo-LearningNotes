# Exercise: Images

<https://go.dev/tour/methods/25>

## Requirements

Remember the picture generator you wrote earlier? Let's write another one, but this time it will return an implementation of `image.Image` instead of a slice of data.

Define your own `Image` type, implement the necessary methods, and call `pic.ShowImage`.

`Bounds` should return a `image.Rectangle`, like `image.Rect(0, 0, w, h)`.

`ColorModel` should return `color.RGBAModel`.

`At` should return a color; the value v in the last picture generator corresponds to `color.RGBA{v, v, 255, 255}` in this one.

## Raw

```go
package main

import "golang.org/x/tour/pic"

type Image struct{}

func main() {
	m := Image{}
	pic.ShowImage(m)
}

```

## Solution

```go
package main

import (
	"image"
	"image/color"

	"golang.org/x/tour/pic"
)

type Image struct {
	height int
	width  int
}

func (image Image) ColorModel() color.Model {
	return color.RGBAModel
}
func (i Image) Bounds() image.Rectangle {
	return image.Rect(0, 0, i.width, i.height)
}
func (image Image) At(x, y int) color.Color {
	return color.RGBA{
		uint8((x*x*3 + x*y*234 + y*y*123 + 23*x + 214*y + 214) % 256),
		uint8((-2*x*x*3 + x*y*12 + y*y*83 - 48*x - 24*y - 344) % 256),
		uint8((2*x*x*3 - x*y*12 - y*y*83 + 48*x + 24*y + 344) % 256),
		255,
	}
}

func main() {
	m := Image{height: 500, width: 500}
	pic.ShowImage(m)
}

```

```output
it's an image
```
