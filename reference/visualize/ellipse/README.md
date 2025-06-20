
# ellipse

```
ellipse(
    width: auto relative
    height: auto relative fraction
    fill: none color gradient tiling
    stroke: none auto length color gradient stroke tiling dictionary
    inset: relative dictionary
    outset: relative dictionary
    none content
) -> content
```
An ellipse with optional content.

## Example

<div class="previewed-code">

    // Without content.
    #ellipse(width: 35%, height: 30pt)

    // With content.
    #ellipse[
      #set align(center)
      Automatically sized \
      to fit the content.
    ]

<div class="preview">

![Preview](/assets/bb7e4b149327d0b0cbc5406a39d8e6be.png)

</div>

</div>


### Parameters


### width: auto, relative | _named_

The ellipse's width, relative to its parent container.


### height: auto, relative, fraction | _named_

The ellipse's height, relative to its parent container.


### fill: none, color, gradient, tiling | _named_

How to fill the ellipse. See the [rectangle's
documentation](/reference/visualize/rect/#parameters-fill) for more
details.


### stroke: none, auto, length, color, gradient, stroke, tiling, dictionary | _named_

How to stroke the ellipse. See the [rectangle's
documentation](/reference/visualize/rect/#parameters-stroke) for more
details.


### inset: relative, dictionary | _named_

How much to pad the ellipse's content. See the [box's
documentation](/reference/layout/box/#parameters-inset) for more
details.


### outset: relative, dictionary | _named_

How much to expand the ellipse's size without affecting the layout. See
the [box's documentation](/reference/layout/box/#parameters-outset) for
more details.


### body: none, content | _positional_

The content to place into the ellipse.

When this is omitted, the ellipse takes on a default size of at most
<span class="typ-num">`45pt`</span> by
<span class="typ-num">`30pt`</span>.

