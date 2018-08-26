---
title: "Art in The Age of Computers"
date: 2018-08-25T00:00:00Z
description: "Could art hold the key to explaining the mysteries of Artificial Intelligence? What if we could exploring their inner thoughts? What if we could see them dream?"
---

My wife and I recently visited the V&A and stumbled across [Chance and Control: Art in the age of computers](https://www.vam.ac.uk/exhibitions/chance-and-control-art-in-the-age-of-computers), a small display celebrating 50 years of computer generated art. Tucked away in the corner of the second room was [Schotter](http://collections.vam.ac.uk/item/O221321/schotter-print-nees-georg/), a piece by Georg Nees.

> “Nees was fascinated by the relationship between order and disorder in picture composition. To create this work, he introduced random variables into the computer program, causing orderly squares to descend into a heap.”

{{< figure height="640px" src="/img/schotter.jpg" title="Schotter, Georg Nees" attr="© Victoria and Albert Museum, London" caption="Schotter, Georg Nees">}}

I was toying with the idea of recreating the image when I came across the [Go Graphics](https://www.michaelfogleman.com/#go-graphics) package by Michael Fogleman ([GitHub](https://github.com/fogleman/gg), [GoDoc](https://godoc.org/github.com/fogleman/gg)), a beautifully simple way to get started with drawing graphics in Go. The basics involve creating a context, drawing various shapes, stroking (or filling) them and then rendering the result as a PNG image.

```go
package main

import "github.com/fogleman/gg"

func main() {
    ctx := gg.NewContext(640, 640)
    ctx.DrawRectangle(270, 270, 100, 100)
    ctx.SetRGBA(0, 0, 0, 1)
    ctx.Stroke()
    ctx.SavePNG("out.png")
}
```

{{< figure height="640px" src="/img/square.png" >}}

This code snippet creates a 640 by 640 image and draws a square of 100 by 100px in the center. To generate the image, I needed a few loops, some randomness and the ability to offset each square from it's regular position. The algorithm seemed fairly straightforward:

* Use a `for` loop to iterate over the columns
* Use a `for` loop to iterate over the rows
* Offset each square from its mid-point based on a function of the current row
* Rotate each square based on a function of the current row

<img src="/img/black_2048x4096_000_00.png" width="50%"><img src="/img/black_2048x4096_000_45.png" width="50%">

Tweaking the dimensions and weighting the offset and rotation gives us something remarkably similar to Georg's original.

{{< figure height="640px" src="/img/black_2480x3508_000.png" >}}

<img src="" width="50%">

With the ability to produce images I quickly found myself spending hours tweaking parameters, padding, colours, etc. I settled on using an exponentially increasing random offset to generate the images below.

<img src="/img/iPhone_jShine_1125x2436_020.png" width="33.3%"><img src="/img/iPhone_blueSkies_1125x2436_020.png" width="33.3%"><img src="/img/iPhoneflare_1125x2436_020.png" width="33.3%">

I’d love to try plotting some of these on paper (using a real plotter of course) but for now I’ll have to settle for generating wallpapers instead. A zip folder containing a collection of phone wallpapers is available for download below. Full access to the source code is available here: [github.com/billglover/aitaoc](https://github.com/billglover/aitaoc)

**Download:** [iPhone](/download/aitaoc_iPhone.zip), [iPad](/download/aitaoc_iPad.zip)