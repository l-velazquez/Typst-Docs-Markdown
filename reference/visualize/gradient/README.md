
# Gradient

A color gradient.

Typst supports linear gradients through the [`gradient.linear`
function](/reference/visualize/gradient/#definitions-linear), radial
gradients through the [`gradient.radial`
function](/reference/visualize/gradient/#definitions-radial), and conic
gradients through the [`gradient.conic`
function](/reference/visualize/gradient/#definitions-conic).

A gradient can be used for the following purposes:

- As a fill to paint the interior of a shape:
  <span class="typ-func">`rect`</span><span class="typ-punct">`(`</span>`fill`<span class="typ-punct">`:`</span>` gradient`<span class="typ-punct">`.`</span><span class="typ-func">`linear`</span><span class="typ-punct">`(`</span><span class="typ-op">`..`</span><span class="typ-punct">`)`</span><span class="typ-punct">`)`</span>
- As a stroke to paint the outline of a shape:
  <span class="typ-func">`rect`</span><span class="typ-punct">`(`</span>`stroke`<span class="typ-punct">`:`</span>` `<span class="typ-num">`1pt`</span>` `<span class="typ-op">`+`</span>` gradient`<span class="typ-punct">`.`</span><span class="typ-func">`linear`</span><span class="typ-punct">`(`</span><span class="typ-op">`..`</span><span class="typ-punct">`)`</span><span class="typ-punct">`)`</span>
- As the fill of text:
  <span class="typ-key">`set`</span>` `<span class="typ-func">`text`</span><span class="typ-punct">`(`</span>`fill`<span class="typ-punct">`:`</span>` gradient`<span class="typ-punct">`.`</span><span class="typ-func">`linear`</span><span class="typ-punct">`(`</span><span class="typ-op">`..`</span><span class="typ-punct">`)`</span><span class="typ-punct">`)`</span>
- As a color map you can
  [sample](/reference/visualize/gradient/#definitions-sample) from:
  `gradient`<span class="typ-punct">`.`</span><span class="typ-func">`linear`</span><span class="typ-punct">`(`</span><span class="typ-op">`..`</span><span class="typ-punct">`)`</span><span class="typ-punct">`.`</span><span class="typ-func">`sample`</span><span class="typ-punct">`(`</span><span class="typ-num">`50%`</span><span class="typ-punct">`)`</span>

## Examples

<div class="previewed-code">

    #stack(
      dir: ltr,
      spacing: 1fr,
      square(fill: gradient.linear(..color.map.rainbow)),
      square(fill: gradient.radial(..color.map.rainbow)),
      square(fill: gradient.conic(..color.map.rainbow)),
    )

<div class="preview">

![Preview](/assets/ff29eecb918a915ec00ed5fcec2f4488.png)

</div>

</div>

Gradients are also supported on text, but only when setting the
[relativeness](/reference/visualize/gradient/#definitions-relative) to
either <span class="typ-key">`auto`</span> (the default value) or
<span class="typ-str">`"parent"`</span>. To create word-by-word or
glyph-by-glyph gradients, you can wrap the words or characters of your
text in [boxes](/reference/layout/box/) manually or through a [show
rule](/reference/styling/#show-rules).

<div class="previewed-code">

    #set text(fill: gradient.linear(red, blue))
    #let rainbow(content) = {
      set text(fill: gradient.linear(..color.map.rainbow))
      box(content)
    }

    This is a gradient on text, but with a #rainbow[twist]!

<div class="preview">

![Preview](/assets/721d0b00b502c2e4285439f1ac4fd467.png)

</div>

</div>

## Stops

A gradient is composed of a series of stops. Each of these stops has a
color and an offset. The offset is a [ratio](/reference/layout/ratio/)
between <span class="typ-num">`0%`</span> and
<span class="typ-num">`100%`</span> or an angle between
<span class="typ-num">`0deg`</span> and
<span class="typ-num">`360deg`</span>. The offset is a relative position
that determines how far along the gradient the stop is located. The
stop's color is the color of the gradient at that position. You can
choose to omit the offsets when defining a gradient. In this case, Typst
will space all stops evenly.

Typst predefines color maps that you can use as stops. See the
[`color`](/reference/visualize/color/#predefined-color-maps)
documentation for more details.

## Relativeness

The location of the <span class="typ-num">`0%`</span> and
<span class="typ-num">`100%`</span> stops depends on the dimensions of a
container. This container can either be the shape that it is being
painted on, or the closest surrounding container. This is controlled by
the `relative` argument of a gradient constructor. By default, gradients
are relative to the shape they are being painted on, unless the gradient
is applied on text, in which case they are relative to the closest
ancestor container.

Typst determines the ancestor container as follows:

- For shapes that are placed at the root/top level of the document, the
  closest ancestor is the page itself.
- For other shapes, the ancestor is the innermost
  [`block`](/reference/layout/block/ "`block`") or
  [`box`](/reference/layout/box/ "`box`") that contains the shape. This
  includes the boxes and blocks that are implicitly created by show
  rules and elements. For example, a
  [`rotate`](/reference/layout/rotate/ "`rotate`") will not affect the
  parent of a gradient, but a [`grid`](/reference/layout/grid/ "`grid`")
  will.

## Color spaces and interpolation

Gradients can be interpolated in any color space. By default, gradients
are interpolated in the
[Oklab](/reference/visualize/color/#definitions-oklab) color space,
which is a [perceptually
uniform](https://programmingdesignsystems.com/color/perceptually-uniform-color-spaces/index.html)
color space. This means that the gradient will be perceived as having a
smooth progression of colors. This is particularly useful for data
visualization.

However, you can choose to interpolate the gradient in any supported
color space you want, but beware that some color spaces are not suitable
for perceptually interpolating between colors. Consult the table below
when choosing an interpolation space.

| Color space | Perceptually uniform? |
|----|----|
| [Oklab](/reference/visualize/color/#definitions-oklab) | *Yes* |
| [Oklch](/reference/visualize/color/#definitions-oklch) | *Yes* |
| [sRGB](/reference/visualize/color/#definitions-rgb) | *No* |
| [linear-RGB](/reference/visualize/color/#definitions-linear-rgb) | *Yes* |
| [CMYK](/reference/visualize/color/#definitions-cmyk) | *No* |
| [Grayscale](/reference/visualize/color/#definitions-luma) | *Yes* |
| [HSL](/reference/visualize/color/#definitions-hsl) | *No* |
| [HSV](/reference/visualize/color/#definitions-hsv) | *No* |

<div class="preview">

![Preview](/assets/be18b60088f1dd3f2eaeacbfe340c3b1.png)

</div>

## Direction

Some gradients are sensitive to direction. For example, a linear
gradient has an angle that determines its direction. Typst uses a
clockwise angle, with 0° being from left to right, 90° from top to
bottom, 180° from right to left, and 270° from bottom to top.

<div class="previewed-code">

    #stack(
      dir: ltr,
      spacing: 1fr,
      square(fill: gradient.linear(red, blue, angle: 0deg)),
      square(fill: gradient.linear(red, blue, angle: 90deg)),
      square(fill: gradient.linear(red, blue, angle: 180deg)),
      square(fill: gradient.linear(red, blue, angle: 270deg)),
    )

<div class="preview">

![Preview](/assets/71783179a4cfd9c8bb34bd7a6b7ac1fe.png)

</div>

</div>

## Note on file sizes

Gradients can be quite large, especially if they have many stops. This
is because gradients are stored as a list of colors and offsets, which
can take up a lot of space. If you are concerned about file sizes, you
should consider the following:

- SVG gradients are currently inefficiently encoded. This will be
  improved in the future.
- PDF gradients in the
  [`color.oklab`](/reference/visualize/color/#definitions-oklab),
  [`color.hsv`](/reference/visualize/color/#definitions-hsv),
  [`color.hsl`](/reference/visualize/color/#definitions-hsl), and
  [`color.oklch`](/reference/visualize/color/#definitions-oklch) color
  spaces are stored as a list of
  [`color.rgb`](/reference/visualize/color/#definitions-rgb) colors with
  extra stops in between. This avoids needing to encode these color
  spaces in your PDF file, but it does add extra stops to your gradient,
  which can increase the file size.


## Definitions


### linear

```
gradient.linear(
    color array
    space: any
    relative: auto str
    direction
    angle
) -> gradient
```
Creates a new linear gradient, in which colors transition along a
straight line.


##### Parameters


##### stops: color, array | _required_ _positional_

The color [stops](#stops) of the gradient.


##### space: any | _named_

The color space in which to interpolate the gradient.

Defaults to a perceptually uniform color space called
[Oklab](/reference/visualize/color/#definitions-oklab).


##### relative: auto, str | _named_

The [relative placement](#relativeness) of the gradient.

For an element placed at the root/top level of the document, the parent
is the page itself. For other elements, the parent is the innermost
block, box, column, grid, or stack that contains the element.


##### dir: direction | _positional_

The direction of the gradient.


##### angle: angle | _required_ _positional_

The angle of the gradient.


#### Example

<div class="previewed-code">

    #rect(
      width: 100%,
      height: 20pt,
      fill: gradient.linear(
        ..color.map.viridis,
      ),
    )

<div class="preview">

![Preview](/assets/def0956800e63dc52a60e2e66b8fb072.png)

</div>

</div>


### radial

```
gradient.radial(
    color array
    space: any
    relative: auto str
    center: array
    radius: ratio
    focal-center: auto array
    focal-radius: ratio
) -> gradient
```
Creates a new radial gradient, in which colors radiate away from an
origin.

The gradient is defined by two circles: the focal circle and the end
circle. The focal circle is a circle with center `focal-center` and
radius `focal-radius`, that defines the points at which the gradient
starts and has the color of the first stop. The end circle is a circle
with center `center` and radius `radius`, that defines the points at
which the gradient ends and has the color of the last stop. The gradient
is then interpolated between these two circles.

Using these four values, also called the focal point for the starting
circle and the center and radius for the end circle, we can define a
gradient with more interesting properties than a basic radial gradient.


##### Parameters


##### stops: color, array | _required_ _positional_

The color [stops](#stops) of the gradient.


##### space: any | _named_

The color space in which to interpolate the gradient.

Defaults to a perceptually uniform color space called
[Oklab](/reference/visualize/color/#definitions-oklab).


##### relative: auto, str | _named_

The [relative placement](#relativeness) of the gradient.

For an element placed at the root/top level of the document, the parent
is the page itself. For other elements, the parent is the innermost
block, box, column, grid, or stack that contains the element.


##### center: array | _named_

The center of the end circle of the gradient.

A value of
<span class="typ-punct">`(`</span><span class="typ-num">`50%`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`50%`</span><span class="typ-punct">`)`</span>
means that the end circle is centered inside of its container.


##### radius: ratio | _named_

The radius of the end circle of the gradient.

By default, it is set to <span class="typ-num">`50%`</span>. The ending
radius must be bigger than the focal radius.


##### focal-center: auto, array | _named_

The center of the focal circle of the gradient.

The focal center must be inside of the end circle.

A value of
<span class="typ-punct">`(`</span><span class="typ-num">`50%`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`50%`</span><span class="typ-punct">`)`</span>
means that the focal circle is centered inside of its container.

By default it is set to the same as the center of the last circle.


##### focal-radius: ratio | _named_

The radius of the focal circle of the gradient.

The focal center must be inside of the end circle.

By default, it is set to <span class="typ-num">`0%`</span>. The focal
radius must be smaller than the ending radius\`.


#### Example

<div class="previewed-code">

    #stack(
      dir: ltr,
      spacing: 1fr,
      circle(fill: gradient.radial(
        ..color.map.viridis,
      )),
      circle(fill: gradient.radial(
        ..color.map.viridis,
        focal-center: (10%, 40%),
        focal-radius: 5%,
      )),
    )

<div class="preview">

![Preview](/assets/21f904edb21c2e1ac7db89749e4d2c21.png)

</div>

</div>


### conic

```
gradient.conic(
    color array
    angle: angle
    space: any
    relative: auto str
    center: array
) -> gradient
```
Creates a new conic gradient, in which colors change radially around a
center point.

You can control the center point of the gradient by using the `center`
argument. By default, the center point is the center of the shape.


##### Parameters


##### stops: color, array | _required_ _positional_

The color [stops](#stops) of the gradient.


##### angle: angle | _named_

The angle of the gradient.


##### space: any | _named_

The color space in which to interpolate the gradient.

Defaults to a perceptually uniform color space called
[Oklab](/reference/visualize/color/#definitions-oklab).


##### relative: auto, str | _named_

The [relative placement](#relativeness) of the gradient.

For an element placed at the root/top level of the document, the parent
is the page itself. For other elements, the parent is the innermost
block, box, column, grid, or stack that contains the element.


##### center: array | _named_

The center of the last circle of the gradient.

A value of
<span class="typ-punct">`(`</span><span class="typ-num">`50%`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`50%`</span><span class="typ-punct">`)`</span>
means that the end circle is centered inside of its container.


#### Example

<div class="previewed-code">

    #stack(
      dir: ltr,
      spacing: 1fr,
      circle(fill: gradient.conic(
        ..color.map.viridis,
      )),
      circle(fill: gradient.conic(
        ..color.map.viridis,
        center: (20%, 30%),
      )),
    )

<div class="preview">

![Preview](/assets/32a99c7b0b1cb9e924d91b259fba0aca.png)

</div>

</div>


### sharp

```
gradient.sharp(
    int
    smoothness: ratio
) -> gradient
```
Creates a sharp version of this gradient.

Sharp gradients have discrete jumps between colors, instead of a smooth
transition. They are particularly useful for creating color lists for a
preset gradient.


##### Parameters


##### steps: int | _required_ _positional_

The number of stops in the gradient.


##### smoothness: ratio | _named_

How much to smooth the gradient.


#### Example

<div class="previewed-code">

    #set rect(width: 100%, height: 20pt)
    #let grad = gradient.linear(..color.map.rainbow)
    #rect(fill: grad)
    #rect(fill: grad.sharp(5))
    #rect(fill: grad.sharp(5, smoothness: 20%))

<div class="preview">

![Preview](/assets/93522b26f5475bd0d38d77f01dd7e1fd.png)

</div>

</div>


### repeat

```
gradient.repeat(
    int
    mirror: bool
) -> gradient
```
Repeats this gradient a given number of times, optionally mirroring it
at every second repetition.


##### Parameters


##### repetitions: int | _required_ _positional_

The number of times to repeat the gradient.


##### mirror: bool | _named_

Whether to mirror the gradient at every second repetition, i.e., the
first instance (and all odd ones) stays unchanged.


###### Example

<div class="previewed-code">

    #circle(
      radius: 40pt,
      fill: gradient
        .conic(green, black)
        .repeat(2, mirror: true)
    )

<div class="preview">

![Preview](/assets/12eb6ef0f82817124abc5d9167ff35dc.png)

</div>

</div>


#### Example

<div class="previewed-code">

    #circle(
      radius: 40pt,
      fill: gradient
        .radial(aqua, white)
        .repeat(4),
    )

<div class="preview">

![Preview](/assets/c9d6c600cc20c2f18c089a5f32cd7000.png)

</div>

</div>


### kind

```
gradient.kind(
) -> function
```
Returns the kind of this gradient.


##### Parameters


### stops

```
gradient.stops(
) -> array
```
Returns the stops of this gradient.


##### Parameters


### space

```
gradient.space(
) -> any
```
Returns the mixing space of this gradient.


##### Parameters


### relative

```
gradient.relative(
) -> auto str
```
Returns the relative placement of this gradient.


##### Parameters


### angle

```
gradient.angle(
) -> none angle
```
Returns the angle of this gradient.

Returns <span class="typ-key">`none`</span> if the gradient is neither
linear nor conic.


##### Parameters


### center

```
gradient.center(
) -> none array
```
Returns the center of this gradient.

Returns <span class="typ-key">`none`</span> if the gradient is neither
radial nor conic.


##### Parameters


### radius

```
gradient.radius(
) -> none ratio
```
Returns the radius of this gradient.

Returns <span class="typ-key">`none`</span> if the gradient is not
radial.


##### Parameters


### focal-center

```
gradient.focal-center(
) -> none array
```
Returns the focal-center of this gradient.

Returns <span class="typ-key">`none`</span> if the gradient is not
radial.


##### Parameters


### focal-radius

```
gradient.focal-radius(
) -> none ratio
```
Returns the focal-radius of this gradient.

Returns <span class="typ-key">`none`</span> if the gradient is not
radial.


##### Parameters


### sample

```
gradient.sample(
    angle ratio
) -> color
```
Sample the gradient at a given position.

The position is either a position along the gradient (a
[ratio](/reference/layout/ratio/ "ratio") between
<span class="typ-num">`0%`</span> and
<span class="typ-num">`100%`</span>) or an
[angle](/reference/layout/angle/ "angle"). Any value outside of this
range will be clamped.


##### Parameters


##### t: angle, ratio | _required_ _positional_

The position at which to sample the gradient.


### samples

```
gradient.samples(
    angle ratio
) -> array
```
Samples the gradient at multiple positions at once and returns the
results as an array.


##### Parameters


##### ts: angle, ratio | _required_ _positional_

The positions at which to sample the gradient.

