
# Color

A color in a specific color space.

Typst supports:

- sRGB through the [`rgb`
  function](/reference/visualize/color/#definitions-rgb)
- Device CMYK through [`cmyk`
  function](/reference/visualize/color/#definitions-cmyk)
- D65 Gray through the [`luma`
  function](/reference/visualize/color/#definitions-luma)
- Oklab through the [`oklab`
  function](/reference/visualize/color/#definitions-oklab)
- Oklch through the [`oklch`
  function](/reference/visualize/color/#definitions-oklch)
- Linear RGB through the [`color.linear-rgb`
  function](/reference/visualize/color/#definitions-linear-rgb)
- HSL through the [`color.hsl`
  function](/reference/visualize/color/#definitions-hsl)
- HSV through the [`color.hsv`
  function](/reference/visualize/color/#definitions-hsv)

## Example

<div class="previewed-code">

    #rect(fill: aqua)

<div class="preview">

![Preview](/assets/93eeb087697d4d35e63e1cd9c696a18d.png)

</div>

</div>

## Predefined colors

Typst defines the following built-in colors:

| Color | Definition |
|----|:---|
| `black` | <span class="typ-func">`luma`</span><span class="typ-punct">`(`</span><span class="typ-num">`0`</span><span class="typ-punct">`)`</span> |
| `gray` | <span class="typ-func">`luma`</span><span class="typ-punct">`(`</span><span class="typ-num">`170`</span><span class="typ-punct">`)`</span> |
| `silver` | <span class="typ-func">`luma`</span><span class="typ-punct">`(`</span><span class="typ-num">`221`</span><span class="typ-punct">`)`</span> |
| `white` | <span class="typ-func">`luma`</span><span class="typ-punct">`(`</span><span class="typ-num">`255`</span><span class="typ-punct">`)`</span> |
| `navy` | <span class="typ-func">`rgb`</span><span class="typ-punct">`(`</span><span class="typ-str">`"#001f3f"`</span><span class="typ-punct">`)`</span> |
| `blue` | <span class="typ-func">`rgb`</span><span class="typ-punct">`(`</span><span class="typ-str">`"#0074d9"`</span><span class="typ-punct">`)`</span> |
| `aqua` | <span class="typ-func">`rgb`</span><span class="typ-punct">`(`</span><span class="typ-str">`"#7fdbff"`</span><span class="typ-punct">`)`</span> |
| `teal` | <span class="typ-func">`rgb`</span><span class="typ-punct">`(`</span><span class="typ-str">`"#39cccc"`</span><span class="typ-punct">`)`</span> |
| `eastern` | <span class="typ-func">`rgb`</span><span class="typ-punct">`(`</span><span class="typ-str">`"#239dad"`</span><span class="typ-punct">`)`</span> |
| `purple` | <span class="typ-func">`rgb`</span><span class="typ-punct">`(`</span><span class="typ-str">`"#b10dc9"`</span><span class="typ-punct">`)`</span> |
| `fuchsia` | <span class="typ-func">`rgb`</span><span class="typ-punct">`(`</span><span class="typ-str">`"#f012be"`</span><span class="typ-punct">`)`</span> |
| `maroon` | <span class="typ-func">`rgb`</span><span class="typ-punct">`(`</span><span class="typ-str">`"#85144b"`</span><span class="typ-punct">`)`</span> |
| `red` | <span class="typ-func">`rgb`</span><span class="typ-punct">`(`</span><span class="typ-str">`"#ff4136"`</span><span class="typ-punct">`)`</span> |
| `orange` | <span class="typ-func">`rgb`</span><span class="typ-punct">`(`</span><span class="typ-str">`"#ff851b"`</span><span class="typ-punct">`)`</span> |
| `yellow` | <span class="typ-func">`rgb`</span><span class="typ-punct">`(`</span><span class="typ-str">`"#ffdc00"`</span><span class="typ-punct">`)`</span> |
| `olive` | <span class="typ-func">`rgb`</span><span class="typ-punct">`(`</span><span class="typ-str">`"#3d9970"`</span><span class="typ-punct">`)`</span> |
| `green` | <span class="typ-func">`rgb`</span><span class="typ-punct">`(`</span><span class="typ-str">`"#2ecc40"`</span><span class="typ-punct">`)`</span> |
| `lime` | <span class="typ-func">`rgb`</span><span class="typ-punct">`(`</span><span class="typ-str">`"#01ff70"`</span><span class="typ-punct">`)`</span> |

The predefined colors and the most important color constructors are
available globally and also in the color type's scope, so you can write
either `color.red` or just `red`.

<div class="preview">

![Preview](/assets/216bd4010ab6d547b5ceef60c23721fa.png)

</div>

## Predefined color maps

Typst also includes a number of preset color maps that can be used for
[gradients](/reference/visualize/gradient/#stops). These are simply
arrays of colors defined in the module `color.map`.

<div class="previewed-code">

    #circle(fill: gradient.linear(..color.map.crest))

<div class="preview">

![Preview](/assets/b86ea2560990c07ffaffed4de36c8a1f.png)

</div>

</div>

| Map | Details |
|----|:---|
| `turbo` | A perceptually uniform rainbow-like color map. Read [this blog post](https://ai.googleblog.com/2019/08/turbo-improved-rainbow-colormap-for.html) for more details. |
| `cividis` | A blue to gray to yellow color map. See [this blog post](https://bids.github.io/colormap/) for more details. |
| `rainbow` | Cycles through the full color spectrum. This color map is best used by setting the interpolation color space to [HSL](/reference/visualize/color/#definitions-hsl). The rainbow gradient is **not suitable** for data visualization because it is not perceptually uniform, so the differences between values become unclear to your readers. It should only be used for decorative purposes. |
| `spectral` | Red to yellow to blue color map. |
| `viridis` | A purple to teal to yellow color map. |
| `inferno` | A black to red to yellow color map. |
| `magma` | A black to purple to yellow color map. |
| `plasma` | A purple to pink to yellow color map. |
| `rocket` | A black to red to white color map. |
| `mako` | A black to teal to white color map. |
| `vlag` | A light blue to white to red color map. |
| `icefire` | A light teal to black to orange color map. |
| `flare` | A orange to purple color map that is perceptually uniform. |
| `crest` | A light green to blue color map. |

Some popular presets are not included because they are not available
under a free licence. Others, like
[Jet](https://jakevdp.github.io/blog/2014/10/16/how-bad-is-your-colormap/),
are not included because they are not color blind friendly. Feel free to
use or create a package with other presets that are useful to you!

<div class="preview">

![Preview](/assets/4b6131a130d12b7d177fdc1725b58866.png)

</div>


## Definitions


### luma

```
color.luma(
    int ratio
    ratio
    color
) -> color
```
Create a grayscale color.

A grayscale color is represented internally by a single `lightness`
component.

These components are also available using the
[`components`](/reference/visualize/color/#definitions-components)
method.


##### Parameters


##### lightness: int, ratio | _required_ _positional_

The lightness component.


##### alpha: ratio | _required_ _positional_

The alpha component.


##### color: color | _required_ _positional_

Alternatively: The color to convert to grayscale.

If this is given, the `lightness` should not be given.


#### Example

<div class="previewed-code">

    #for x in range(250, step: 50) {
      box(square(fill: luma(x)))
    }

<div class="preview">

![Preview](/assets/6c24ce5a43ada433e3b83da23e04da8d.png)

</div>

</div>


### oklab

```
color.oklab(
    ratio
    float ratio
    float ratio
    ratio
    color
) -> color
```
Create an [Oklab](https://bottosson.github.io/posts/oklab/) color.

This color space is well suited for the following use cases:

- Color manipulation such as saturating while keeping perceived hue
- Creating grayscale images with uniform perceived lightness
- Creating smooth and uniform color transition and gradients

A linear Oklab color is represented internally by an array of four
components:

- lightness ([`ratio`](/reference/layout/ratio/ "`ratio`"))
- a ([`float`](/reference/foundations/float/ "`float`") or
  [`ratio`](/reference/layout/ratio/ "`ratio`"). Ratios are relative to
  <span class="typ-num">`0.4`</span>; meaning
  <span class="typ-num">`50%`</span> is equal to
  <span class="typ-num">`0.2`</span>)
- b ([`float`](/reference/foundations/float/ "`float`") or
  [`ratio`](/reference/layout/ratio/ "`ratio`"). Ratios are relative to
  <span class="typ-num">`0.4`</span>; meaning
  <span class="typ-num">`50%`</span> is equal to
  <span class="typ-num">`0.2`</span>)
- alpha ([`ratio`](/reference/layout/ratio/ "`ratio`"))

These components are also available using the
[`components`](/reference/visualize/color/#definitions-components)
method.


##### Parameters


##### lightness: ratio | _required_ _positional_

The lightness component.


##### a: float, ratio | _required_ _positional_

The a ("green/red") component.


##### b: float, ratio | _required_ _positional_

The b ("blue/yellow") component.


##### alpha: ratio | _required_ _positional_

The alpha component.


##### color: color | _required_ _positional_

Alternatively: The color to convert to Oklab.

If this is given, the individual components should not be given.


#### Example

<div class="previewed-code">

    #square(
      fill: oklab(27%, 20%, -3%, 50%)
    )

<div class="preview">

![Preview](/assets/d5d1b30dbc1d63361be4dcc913343314.png)

</div>

</div>


### oklch

```
color.oklch(
    ratio
    float ratio
    angle
    ratio
    color
) -> color
```
Create an [Oklch](https://bottosson.github.io/posts/oklab/) color.

This color space is well suited for the following use cases:

- Color manipulation involving lightness, chroma, and hue
- Creating grayscale images with uniform perceived lightness
- Creating smooth and uniform color transition and gradients

A linear Oklch color is represented internally by an array of four
components:

- lightness ([`ratio`](/reference/layout/ratio/ "`ratio`"))
- chroma ([`float`](/reference/foundations/float/ "`float`") or
  [`ratio`](/reference/layout/ratio/ "`ratio`"). Ratios are relative to
  <span class="typ-num">`0.4`</span>; meaning
  <span class="typ-num">`50%`</span> is equal to
  <span class="typ-num">`0.2`</span>)
- hue ([`angle`](/reference/layout/angle/ "`angle`"))
- alpha ([`ratio`](/reference/layout/ratio/ "`ratio`"))

These components are also available using the
[`components`](/reference/visualize/color/#definitions-components)
method.


##### Parameters


##### lightness: ratio | _required_ _positional_

The lightness component.


##### chroma: float, ratio | _required_ _positional_

The chroma component.


##### hue: angle | _required_ _positional_

The hue component.


##### alpha: ratio | _required_ _positional_

The alpha component.


##### color: color | _required_ _positional_

Alternatively: The color to convert to Oklch.

If this is given, the individual components should not be given.


#### Example

<div class="previewed-code">

    #square(
      fill: oklch(40%, 0.2, 160deg, 50%)
    )

<div class="preview">

![Preview](/assets/80426dd4f0691936a37149b8e92f8936.png)

</div>

</div>


### linear-rgb

```
color.linear-rgb(
    int ratio
    int ratio
    int ratio
    int ratio
    color
) -> color
```
Create an RGB(A) color with linear luma.

This color space is similar to sRGB, but with the distinction that the
color component are not gamma corrected. This makes it easier to perform
color operations such as blending and interpolation. Although, you
should prefer to use the [`oklab`
function](/reference/visualize/color/#definitions-oklab) for these.

A linear RGB(A) color is represented internally by an array of four
components:

- red ([`ratio`](/reference/layout/ratio/ "`ratio`"))
- green ([`ratio`](/reference/layout/ratio/ "`ratio`"))
- blue ([`ratio`](/reference/layout/ratio/ "`ratio`"))
- alpha ([`ratio`](/reference/layout/ratio/ "`ratio`"))

These components are also available using the
[`components`](/reference/visualize/color/#definitions-components)
method.


##### Parameters


##### red: int, ratio | _required_ _positional_

The red component.


##### green: int, ratio | _required_ _positional_

The green component.


##### blue: int, ratio | _required_ _positional_

The blue component.


##### alpha: int, ratio | _required_ _positional_

The alpha component.


##### color: color | _required_ _positional_

Alternatively: The color to convert to linear RGB(A).

If this is given, the individual components should not be given.


#### Example

<div class="previewed-code">

    #square(fill: color.linear-rgb(
      30%, 50%, 10%,
    ))

<div class="preview">

![Preview](/assets/b7f5d6072aad409a0124394f175f691.png)

</div>

</div>


### rgb

```
color.rgb(
    int ratio
    int ratio
    int ratio
    int ratio
    str
    color
) -> color
```
Create an RGB(A) color.

The color is specified in the sRGB color space.

An RGB(A) color is represented internally by an array of four
components:

- red ([`ratio`](/reference/layout/ratio/ "`ratio`"))
- green ([`ratio`](/reference/layout/ratio/ "`ratio`"))
- blue ([`ratio`](/reference/layout/ratio/ "`ratio`"))
- alpha ([`ratio`](/reference/layout/ratio/ "`ratio`"))

These components are also available using the
[`components`](/reference/visualize/color/#definitions-components)
method.


##### Parameters


##### red: int, ratio | _required_ _positional_

The red component.


##### green: int, ratio | _required_ _positional_

The green component.


##### blue: int, ratio | _required_ _positional_

The blue component.


##### alpha: int, ratio | _required_ _positional_

The alpha component.


##### hex: str | _required_ _positional_

Alternatively: The color in hexadecimal notation.

Accepts three, four, six or eight hexadecimal digits and optionally a
leading hash.

If this is given, the individual components should not be given.


###### Example

<div class="previewed-code">

    #text(16pt, rgb("#239dad"))[
      *Typst*
    ]

<div class="preview">

![Preview](/assets/aca7c8b7a9ea4b3a01457b7b93b04c3b.png)

</div>

</div>


##### color: color | _required_ _positional_

Alternatively: The color to convert to RGB(a).

If this is given, the individual components should not be given.


#### Example

<div class="previewed-code">

    #square(fill: rgb("#b1f2eb"))
    #square(fill: rgb(87, 127, 230))
    #square(fill: rgb(25%, 13%, 65%))

<div class="preview">

![Preview](/assets/7968af65b92aee8168b4cd3a39e2bdd8.png)

</div>

</div>


### cmyk

```
color.cmyk(
    ratio
    ratio
    ratio
    ratio
    color
) -> color
```
Create a CMYK color.

This is useful if you want to target a specific printer. The conversion
to RGB for display preview might differ from how your printer reproduces
the color.

A CMYK color is represented internally by an array of four components:

- cyan ([`ratio`](/reference/layout/ratio/ "`ratio`"))
- magenta ([`ratio`](/reference/layout/ratio/ "`ratio`"))
- yellow ([`ratio`](/reference/layout/ratio/ "`ratio`"))
- key ([`ratio`](/reference/layout/ratio/ "`ratio`"))

These components are also available using the
[`components`](/reference/visualize/color/#definitions-components)
method.

Note that CMYK colors are not currently supported when PDF/A output is
enabled.


##### Parameters


##### cyan: ratio | _required_ _positional_

The cyan component.


##### magenta: ratio | _required_ _positional_

The magenta component.


##### yellow: ratio | _required_ _positional_

The yellow component.


##### key: ratio | _required_ _positional_

The key component.


##### color: color | _required_ _positional_

Alternatively: The color to convert to CMYK.

If this is given, the individual components should not be given.


#### Example

<div class="previewed-code">

    #square(
      fill: cmyk(27%, 0%, 3%, 5%)
    )

<div class="preview">

![Preview](/assets/d4b1e282da4509956348db3cddf3f478.png)

</div>

</div>


### hsl

```
color.hsl(
    angle
    int ratio
    int ratio
    int ratio
    color
) -> color
```
Create an HSL color.

This color space is useful for specifying colors by hue, saturation and
lightness. It is also useful for color manipulation, such as saturating
while keeping perceived hue.

An HSL color is represented internally by an array of four components:

- hue ([`angle`](/reference/layout/angle/ "`angle`"))
- saturation ([`ratio`](/reference/layout/ratio/ "`ratio`"))
- lightness ([`ratio`](/reference/layout/ratio/ "`ratio`"))
- alpha ([`ratio`](/reference/layout/ratio/ "`ratio`"))

These components are also available using the
[`components`](/reference/visualize/color/#definitions-components)
method.


##### Parameters


##### hue: angle | _required_ _positional_

The hue angle.


##### saturation: int, ratio | _required_ _positional_

The saturation component.


##### lightness: int, ratio | _required_ _positional_

The lightness component.


##### alpha: int, ratio | _required_ _positional_

The alpha component.


##### color: color | _required_ _positional_

Alternatively: The color to convert to HSL.

If this is given, the individual components should not be given.


#### Example

<div class="previewed-code">

    #square(
      fill: color.hsl(30deg, 50%, 60%)
    )

<div class="preview">

![Preview](/assets/32a4753614fe9bf2260435f6de163bc6.png)

</div>

</div>


### hsv

```
color.hsv(
    angle
    int ratio
    int ratio
    int ratio
    color
) -> color
```
Create an HSV color.

This color space is useful for specifying colors by hue, saturation and
value. It is also useful for color manipulation, such as saturating
while keeping perceived hue.

An HSV color is represented internally by an array of four components:

- hue ([`angle`](/reference/layout/angle/ "`angle`"))
- saturation ([`ratio`](/reference/layout/ratio/ "`ratio`"))
- value ([`ratio`](/reference/layout/ratio/ "`ratio`"))
- alpha ([`ratio`](/reference/layout/ratio/ "`ratio`"))

These components are also available using the
[`components`](/reference/visualize/color/#definitions-components)
method.


##### Parameters


##### hue: angle | _required_ _positional_

The hue angle.


##### saturation: int, ratio | _required_ _positional_

The saturation component.


##### value: int, ratio | _required_ _positional_

The value component.


##### alpha: int, ratio | _required_ _positional_

The alpha component.


##### color: color | _required_ _positional_

Alternatively: The color to convert to HSL.

If this is given, the individual components should not be given.


#### Example

<div class="previewed-code">

    #square(
      fill: color.hsv(30deg, 50%, 60%)
    )

<div class="preview">

![Preview](/assets/7443a35ccc65557f31800b8c145fa091.png)

</div>

</div>


### components

```
color.components(
    alpha: bool
) -> array
```
Extracts the components of this color.

The size and values of this array depends on the color space. You can
obtain the color space using
[`space`](/reference/visualize/color/#definitions-space). Below is a
table of the color spaces and their components:

| Color space | C1 | C2 | C3 | C4 |
|----|----|----|----|----|
| [`luma`](/reference/visualize/color/#definitions-luma) | Lightness |  |  |  |
| [`oklab`](/reference/visualize/color/#definitions-oklab) | Lightness | `a` | `b` | Alpha |
| [`oklch`](/reference/visualize/color/#definitions-oklch) | Lightness | Chroma | Hue | Alpha |
| [`linear-rgb`](/reference/visualize/color/#definitions-linear-rgb) | Red | Green | Blue | Alpha |
| [`rgb`](/reference/visualize/color/#definitions-rgb) | Red | Green | Blue | Alpha |
| [`cmyk`](/reference/visualize/color/#definitions-cmyk) | Cyan | Magenta | Yellow | Key |
| [`hsl`](/reference/visualize/color/#definitions-hsl) | Hue | Saturation | Lightness | Alpha |
| [`hsv`](/reference/visualize/color/#definitions-hsv) | Hue | Saturation | Value | Alpha |

For the meaning and type of each individual value, see the documentation
of the corresponding color space. The alpha component is optional and
only included if the `alpha` argument is `true`. The length of the
returned array depends on the number of components and whether the alpha
component is included.


##### Parameters


##### alpha: bool | _named_

Whether to include the alpha component.


#### Example

<div class="previewed-code">

    // note that the alpha component is included by default
    #rgb(40%, 60%, 80%).components()

<div class="preview">

![Preview](/assets/77307f77341fe1233f3aed1e01c147f4.png)

</div>

</div>


### space

```
color.space(
) -> any
```
Returns the constructor function for this color's space:

- [`luma`](/reference/visualize/color/#definitions-luma)
- [`oklab`](/reference/visualize/color/#definitions-oklab)
- [`oklch`](/reference/visualize/color/#definitions-oklch)
- [`linear-rgb`](/reference/visualize/color/#definitions-linear-rgb)
- [`rgb`](/reference/visualize/color/#definitions-rgb)
- [`cmyk`](/reference/visualize/color/#definitions-cmyk)
- [`hsl`](/reference/visualize/color/#definitions-hsl)
- [`hsv`](/reference/visualize/color/#definitions-hsv)


##### Parameters


#### Example

<div class="previewed-code">

    #let color = cmyk(1%, 2%, 3%, 4%)
    #(color.space() == cmyk)

<div class="preview">

![Preview](/assets/b5f89cffa16ef490db9384f3dab62028.png)

</div>

</div>


### to-hex

```
color.to-hex(
) -> str
```
Returns the color's RGB(A) hex representation (such as `#ffaa32` or
`#020304fe`). The alpha component (last two digits in `#020304fe`) is
omitted if it is equal to `ff` (255 / 100%).


##### Parameters


### lighten

```
color.lighten(
    ratio
) -> color
```
Lightens a color by a given factor.


##### Parameters


##### factor: ratio | _required_ _positional_

The factor to lighten the color by.


### darken

```
color.darken(
    ratio
) -> color
```
Darkens a color by a given factor.


##### Parameters


##### factor: ratio | _required_ _positional_

The factor to darken the color by.


### saturate

```
color.saturate(
    ratio
) -> color
```
Increases the saturation of a color by a given factor.


##### Parameters


##### factor: ratio | _required_ _positional_

The factor to saturate the color by.


### desaturate

```
color.desaturate(
    ratio
) -> color
```
Decreases the saturation of a color by a given factor.


##### Parameters


##### factor: ratio | _required_ _positional_

The factor to desaturate the color by.


### negate

```
color.negate(
    space: any
) -> color
```
Produces the complementary color using a provided color space. You can
think of it as the opposite side on a color wheel.


##### Parameters


##### space: any | _named_

The color space used for the transformation. By default, a perceptual
color space is used.


#### Example

<div class="previewed-code">

    #square(fill: yellow)
    #square(fill: yellow.negate())
    #square(fill: yellow.negate(space: rgb))

<div class="preview">

![Preview](/assets/a015995bf8bf799f00f4aff8eb05cb69.png)

</div>

</div>


### rotate

```
color.rotate(
    angle
    space: any
) -> color
```
Rotates the hue of the color by a given angle.


##### Parameters


##### angle: angle | _required_ _positional_

The angle to rotate the hue by.


##### space: any | _named_

The color space used to rotate. By default, this happens in a perceptual
color space ([`oklch`](/reference/visualize/color/#definitions-oklch)).


### mix

```
color.mix(
    color array
    space: any
) -> color
```
Create a color by mixing two or more colors.

In color spaces with a hue component (hsl, hsv, oklch), only two colors
can be mixed at once. Mixing more than two colors in such a space will
result in an error!


##### Parameters


##### colors: color, array | _required_ _positional_

The colors, optionally with weights, specified as a pair (array of
length two) of color and weight (float or ratio).

The weights do not need to add to <span class="typ-num">`100%`</span>,
they are relative to the sum of all weights.


##### space: any | _named_

The color space to mix in. By default, this happens in a perceptual
color space ([`oklab`](/reference/visualize/color/#definitions-oklab)).


#### Example

<div class="previewed-code">

    #set block(height: 20pt, width: 100%)
    #block(fill: red.mix(blue))
    #block(fill: red.mix(blue, space: rgb))
    #block(fill: color.mix(red, blue, white))
    #block(fill: color.mix((red, 70%), (blue, 30%)))

<div class="preview">

![Preview](/assets/d23013ea064fa345f4d82557526ed8a4.png)

</div>

</div>


### transparentize

```
color.transparentize(
    ratio
) -> color
```
Makes a color more transparent by a given factor.

This method is relative to the existing alpha value. If the scale is
positive, calculates `alpha - alpha * scale`. Negative scales behave
like `color.opacify(-scale)`.


##### Parameters


##### scale: ratio | _required_ _positional_

The factor to change the alpha value by.


#### Example

<div class="previewed-code">

    #block(fill: red)[opaque]
    #block(fill: red.transparentize(50%))[half red]
    #block(fill: red.transparentize(75%))[quarter red]

<div class="preview">

![Preview](/assets/6e735785029f8dce00615699d53ddedf.png)

</div>

</div>


### opacify

```
color.opacify(
    ratio
) -> color
```
Makes a color more opaque by a given scale.

This method is relative to the existing alpha value. If the scale is
positive, calculates `alpha + scale - alpha * scale`. Negative scales
behave like `color.transparentize(-scale)`.


##### Parameters


##### scale: ratio | _required_ _positional_

The scale to change the alpha value by.


#### Example

<div class="previewed-code">

    #let half-red = red.transparentize(50%)
    #block(fill: half-red.opacify(100%))[opaque]
    #block(fill: half-red.opacify(50%))[three quarters red]
    #block(fill: half-red.opacify(-50%))[one quarter red]

<div class="preview">

![Preview](/assets/d5fabefb63ab2121f583cfddbd406ba0.png)

</div>

</div>

