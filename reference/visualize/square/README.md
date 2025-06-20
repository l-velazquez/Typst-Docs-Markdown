
# square

```
square(
    size: auto length
    width: auto relative
    height: auto relative fraction
    fill: none color gradient tiling
    stroke: none auto length color gradient stroke tiling dictionary
    radius: relative dictionary
    inset: relative dictionary
    outset: relative dictionary
    none content
) -> content
```
A square with optional content.

## Example

<div class="previewed-code">

    // Without content.
    #square(size: 40pt)

    // With content.
    #square[
      Automatically \
      sized to fit.
    ]

<div class="preview">

![Preview](/assets/e35a80a6686ae7fe68882233aa8efee.png)

</div>

</div>


### Parameters


### size: auto, length | _named_

The square's side length. This is mutually exclusive with `width` and
`height`.


### width: auto, relative | _named_

The square's width. This is mutually exclusive with `size` and `height`.

In contrast to `size`, this can be relative to the parent container's
width.


### height: auto, relative, fraction | _named_

The square's height. This is mutually exclusive with `size` and `width`.

In contrast to `size`, this can be relative to the parent container's
height.


### fill: none, color, gradient, tiling | _named_

How to fill the square. See the [rectangle's
documentation](/reference/visualize/rect/#parameters-fill) for more
details.


### stroke: none, auto, length, color, gradient, stroke, tiling, dictionary | _named_

How to stroke the square. See the [rectangle's
documentation](/reference/visualize/rect/#parameters-stroke) for more
details.


### radius: relative, dictionary | _named_

How much to round the square's corners. See the [rectangle's
documentation](/reference/visualize/rect/#parameters-radius) for more
details.


### inset: relative, dictionary | _named_

How much to pad the square's content. See the [box's
documentation](/reference/layout/box/#parameters-inset) for more
details.


### outset: relative, dictionary | _named_

How much to expand the square's size without affecting the layout. See
the [box's documentation](/reference/layout/box/#parameters-outset) for
more details.


### body: none, content | _positional_

The content to place into the square. The square expands to fit this
content, keeping the 1-1 aspect ratio.

When this is omitted, the square takes on a default size of at most
<span class="typ-num">`30pt`</span>.

