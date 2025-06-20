
# Tiling

A repeating tiling fill.

Typst supports the most common type of tilings, where a pattern is
repeated in a grid-like fashion, covering the entire area of an element
that is filled or stroked. The pattern is defined by a tile size and a
body defining the content of each cell. You can also add horizontal or
vertical spacing between the cells of the tiling.

## Examples

<div class="previewed-code">

    #let pat = tiling(size: (30pt, 30pt))[
      #place(line(start: (0%, 0%), end: (100%, 100%)))
      #place(line(start: (0%, 100%), end: (100%, 0%)))
    ]

    #rect(fill: pat, width: 100%, height: 60pt, stroke: 1pt)

<div class="preview">

![Preview](/assets/aa1d27fdbd1db81580724b895115f7d6.png)

</div>

</div>

Tilings are also supported on text, but only when setting the
[relativeness](/reference/visualize/tiling/#parameters-relative) to
either <span class="typ-key">`auto`</span> (the default value) or
<span class="typ-str">`"parent"`</span>. To create word-by-word or
glyph-by-glyph tilings, you can wrap the words or characters of your
text in [boxes](/reference/layout/box/) manually or through a [show
rule](/reference/styling/#show-rules).

<div class="previewed-code">

    #let pat = tiling(
      size: (30pt, 30pt),
      relative: "parent",
      square(
        size: 30pt,
        fill: gradient
          .conic(..color.map.rainbow),
      )
    )

    #set text(fill: pat)
    #lorem(10)

<div class="preview">

![Preview](/assets/1d49890bdcd0d3618e7fac207ef2772d.png)

</div>

</div>

You can also space the elements further or closer apart using the
[`spacing`](/reference/visualize/tiling/#parameters-spacing) feature of
the tiling. If the spacing is lower than the size of the tiling, the
tiling will overlap. If it is higher, the tiling will have gaps of the
same color as the background of the tiling.

<div class="previewed-code">

    #let pat = tiling(
      size: (30pt, 30pt),
      spacing: (10pt, 10pt),
      relative: "parent",
      square(
        size: 30pt,
        fill: gradient
         .conic(..color.map.rainbow),
      ),
    )

    #rect(
      width: 100%,
      height: 60pt,
      fill: pat,
    )

<div class="preview">

![Preview](/assets/a01f3d44bb227edd4662b2e9122d7ffe.png)

</div>

</div>

## Relativeness

The location of the starting point of the tiling is dependent on the
dimensions of a container. This container can either be the shape that
it is being painted on, or the closest surrounding container. This is
controlled by the `relative` argument of a tiling constructor. By
default, tilings are relative to the shape they are being painted on,
unless the tiling is applied on text, in which case they are relative to
the closest ancestor container.

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

## Compatibility

This type used to be called `pattern`. The name remains as an alias, but
is deprecated since Typst 0.13.


## tiling

```
tiling(
    size: auto array
    spacing: array
    relative: auto str
    content
) -> tiling
```
Construct a new tiling.


#### Parameters


#### size: auto, array | _named_

The bounding box of each cell of the tiling.


#### spacing: array | _named_

The spacing between cells of the tiling.


#### relative: auto, str | _named_

The [relative placement](#relativeness) of the tiling.

For an element placed at the root/top level of the document, the parent
is the page itself. For other elements, the parent is the innermost
block, box, column, grid, or stack that contains the element.


#### body: content | _required_ _positional_

The content of each cell of the tiling.


### Example

<div class="previewed-code">

    #let pat = tiling(
      size: (20pt, 20pt),
      relative: "parent",
      place(
        dx: 5pt,
        dy: 5pt,
        rotate(45deg, square(
          size: 5pt,
          fill: black,
        )),
      ),
    )

    #rect(width: 100%, height: 60pt, fill: pat)

<div class="preview">

![Preview](/assets/997166e01319ea437b75b8c87c9925f6.png)

</div>

</div>


## Definitions

