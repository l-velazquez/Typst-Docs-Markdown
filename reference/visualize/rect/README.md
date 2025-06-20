
# rect

```
rect(
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
A rectangle with optional content.

## Example

<div class="previewed-code">

    // Without content.
    #rect(width: 35%, height: 30pt)

    // With content.
    #rect[
      Automatically sized \
      to fit the content.
    ]

<div class="preview">

![Preview](/assets/b8c2e4acab3c02639ef4bfaa5380982a.png)

</div>

</div>


### Parameters


### width: auto, relative | _named_

The rectangle's width, relative to its parent container.


### height: auto, relative, fraction | _named_

The rectangle's height, relative to its parent container.


### fill: none, color, gradient, tiling | _named_

How to fill the rectangle.

When setting a fill, the default stroke disappears. To create a
rectangle with both fill and stroke, you have to configure both.


#### Example

<div class="previewed-code">

    #rect(fill: blue)

<div class="preview">

![Preview](/assets/5e9d207b0c933ecd5aaddeb58a002324.png)

</div>

</div>


### stroke: none, auto, length, color, gradient, stroke, tiling, dictionary | _named_

How to stroke the rectangle. This can be:

- <span class="typ-key">`none`</span> to disable stroking
- <span class="typ-key">`auto`</span> for a stroke of
  <span class="typ-num">`1pt`</span>` `<span class="typ-op">`+`</span>` black`
  if and if only if no fill is given.
- Any kind of [stroke](/reference/visualize/stroke/ "stroke")
- A dictionary describing the stroke for each side individually. The
  dictionary can contain the following keys in order of precedence:
  - `top`: The top stroke.
  - `right`: The right stroke.
  - `bottom`: The bottom stroke.
  - `left`: The left stroke.
  - `x`: The horizontal stroke.
  - `y`: The vertical stroke.
  - `rest`: The stroke on all sides except those for which the
    dictionary explicitly sets a size.


#### Example

<div class="previewed-code">

    #stack(
      dir: ltr,
      spacing: 1fr,
      rect(stroke: red),
      rect(stroke: 2pt),
      rect(stroke: 2pt + red),
    )

<div class="preview">

![Preview](/assets/44d3c9c5a1d56ba8ecfcffbc7c9144c4.png)

</div>

</div>


### radius: relative, dictionary | _named_

How much to round the rectangle's corners, relative to the minimum of
the width and height divided by two. This can be:

- A relative length for a uniform corner radius.
- A dictionary: With a dictionary, the stroke for each side can be set
  individually. The dictionary can contain the following keys in order
  of precedence:
  - `top-left`: The top-left corner radius.
  - `top-right`: The top-right corner radius.
  - `bottom-right`: The bottom-right corner radius.
  - `bottom-left`: The bottom-left corner radius.
  - `left`: The top-left and bottom-left corner radii.
  - `top`: The top-left and top-right corner radii.
  - `right`: The top-right and bottom-right corner radii.
  - `bottom`: The bottom-left and bottom-right corner radii.
  - `rest`: The radii for all corners except those for which the
    dictionary explicitly sets a size.


#### Example

<div class="previewed-code">

    #set rect(stroke: 4pt)
    #rect(
      radius: (
        left: 5pt,
        top-right: 20pt,
        bottom-right: 10pt,
      ),
      stroke: (
        left: red,
        top: yellow,
        right: green,
        bottom: blue,
      ),
    )

<div class="preview">

![Preview](/assets/3fdded0cd492aef99d7d7bf62fb32661.png)

</div>

</div>


### inset: relative, dictionary | _named_

How much to pad the rectangle's content. See the [box's
documentation](/reference/layout/box/#parameters-inset) for more
details.


### outset: relative, dictionary | _named_

How much to expand the rectangle's size without affecting the layout.
See the [box's documentation](/reference/layout/box/#parameters-outset)
for more details.


### body: none, content | _positional_

The content to place into the rectangle.

When this is omitted, the rectangle takes on a default size of at most
<span class="typ-num">`45pt`</span> by
<span class="typ-num">`30pt`</span>.

