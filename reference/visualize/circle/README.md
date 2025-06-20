
# circle

```
circle(
    radius: length
    width: auto relative
    height: auto relative fraction
    fill: none color gradient tiling
    stroke: none auto length color gradient stroke tiling dictionary
    inset: relative dictionary
    outset: relative dictionary
    none content
) -> content
```
A circle with optional content.

## Example

<div class="previewed-code">

    // Without content.
    #circle(radius: 25pt)

    // With content.
    #circle[
      #set align(center + horizon)
      Automatically \
      sized to fit.
    ]

<div class="preview">

![Preview](/assets/1f59e2c057a82944d5833baa72667f56.png)

</div>

</div>


### Parameters


### radius: length | _named_

The circle's radius. This is mutually exclusive with `width` and
`height`.


### width: auto, relative | _named_

The circle's width. This is mutually exclusive with `radius` and
`height`.

In contrast to `radius`, this can be relative to the parent container's
width.


### height: auto, relative, fraction | _named_

The circle's height. This is mutually exclusive with `radius` and
`width`.

In contrast to `radius`, this can be relative to the parent container's
height.


### fill: none, color, gradient, tiling | _named_

How to fill the circle. See the [rectangle's
documentation](/reference/visualize/rect/#parameters-fill) for more
details.


### stroke: none, auto, length, color, gradient, stroke, tiling, dictionary | _named_

How to stroke the circle. See the [rectangle's
documentation](/reference/visualize/rect/#parameters-stroke) for more
details.


### inset: relative, dictionary | _named_

How much to pad the circle's content. See the [box's
documentation](/reference/layout/box/#parameters-inset) for more
details.


### outset: relative, dictionary | _named_

How much to expand the circle's size without affecting the layout. See
the [box's documentation](/reference/layout/box/#parameters-outset) for
more details.


### body: none, content | _positional_

The content to place into the circle. The circle expands to fit this
content, keeping the 1-1 aspect ratio.

