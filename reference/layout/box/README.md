
# box

```
box(
    width: auto relative fraction
    height: auto relative
    baseline: relative
    fill: none color gradient tiling
    stroke: none length color gradient stroke tiling dictionary
    radius: relative dictionary
    inset: relative dictionary
    outset: relative dictionary
    clip: bool
    none content
) -> content
```
An inline-level container that sizes content.

All elements except inline math, text, and boxes are block-level and
cannot occur inside of a [paragraph](/reference/model/par/). The box
function can be used to integrate such elements into a paragraph. Boxes
take the size of their contents by default but can also be sized
explicitly.

## Example

<div class="previewed-code">

    Refer to the docs
    #box(
      height: 9pt,
      image("docs.svg")
    )
    for more information.

<div class="preview">

![Preview](/assets/781f4d033bb6c64f8ed6689f7e8cf029.png)

</div>

</div>


### Parameters


### width: auto, relative, fraction | _named_

The width of the box.

Boxes can have [fractional](/reference/layout/fraction/) widths, as the
example below demonstrates.

*Note:* Currently, only boxes and only their widths might be
fractionally sized within paragraphs. Support for fractionally sized
images, shapes, and more might be added in the future.


#### Example

<div class="previewed-code">

    Line in #box(width: 1fr, line(length: 100%)) between.

<div class="preview">

![Preview](/assets/77326ba2a90f710f23d720fa9d9484d0.png)

</div>

</div>


### height: auto, relative | _named_

The height of the box.


### baseline: relative | _named_

An amount to shift the box's baseline by.


#### Example

<div class="previewed-code">

    Image: #box(baseline: 40%, image("tiger.jpg", width: 2cm)).

<div class="preview">

![Preview](/assets/8cd6665dc2d94162a88dbe58873dee11.png)

</div>

</div>


### fill: none, color, gradient, tiling | _named_

The box's background color. See the [rectangle's
documentation](/reference/visualize/rect/#parameters-fill) for more
details.


### stroke: none, length, color, gradient, stroke, tiling, dictionary | _named_

The box's border color. See the [rectangle's
documentation](/reference/visualize/rect/#parameters-stroke) for more
details.


### radius: relative, dictionary | _named_

How much to round the box's corners. See the [rectangle's
documentation](/reference/visualize/rect/#parameters-radius) for more
details.


### inset: relative, dictionary | _named_

How much to pad the box's content.

*Note:* When the box contains text, its exact size depends on the
current [text edges](/reference/text/text/#parameters-top-edge).


#### Example

<div class="previewed-code">

    #rect(inset: 0pt)[Tight]

<div class="preview">

![Preview](/assets/1950e9bc82ffb5ee8a9520120f78b611.png)

</div>

</div>


### outset: relative, dictionary | _named_

How much to expand the box's size without affecting the layout.

This is useful to prevent padding from affecting line layout. For a
generalized version of the example below, see the documentation for the
[raw text's block parameter](/reference/text/raw/#parameters-block).


#### Example

<div class="previewed-code">

    An inline
    #box(
      fill: luma(235),
      inset: (x: 3pt, y: 0pt),
      outset: (y: 3pt),
      radius: 2pt,
    )[rectangle].

<div class="preview">

![Preview](/assets/ebc290926fc7b24332d5a0c06d059877.png)

</div>

</div>


### clip: bool | _named_

Whether to clip the content inside the box.

Clipping is useful when the box's content is larger than the box itself,
as any content that exceeds the box's bounds will be hidden.


#### Example

<div class="previewed-code">

    #box(
      width: 50pt,
      height: 50pt,
      clip: true,
      image("tiger.jpg", width: 100pt, height: 100pt)
    )

<div class="preview">

![Preview](/assets/440635222ac048249d1f4a4ce36d3d6f.png)

</div>

</div>


### body: none, content | _positional_

The contents of the box.

