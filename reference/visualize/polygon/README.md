
# polygon

```
polygon(
    fill: none color gradient tiling
    fill-rule: str
    stroke: none auto length color gradient stroke tiling dictionary
    array
) -> content
```
A closed polygon.

The polygon is defined by its corner points and is closed automatically.

## Example

<div class="previewed-code">

    #polygon(
      fill: blue.lighten(80%),
      stroke: blue,
      (20%, 0pt),
      (60%, 0pt),
      (80%, 2cm),
      (0%,  2cm),
    )

<div class="preview">

![Preview](/assets/4eecc04e899aad583ed0d99456edd014.png)

</div>

</div>


### Parameters


### fill: none, color, gradient, tiling | _named_

How to fill the polygon.

When setting a fill, the default stroke disappears. To create a
rectangle with both fill and stroke, you have to configure both.


### fill-rule: str | _named_

The drawing rule used to fill the polygon.

See the [curve
documentation](/reference/visualize/curve/#parameters-fill-rule) for an
example.


### stroke: none, auto, length, color, gradient, stroke, tiling, dictionary | _named_

How to [stroke](/reference/visualize/stroke/ "stroke") the polygon. This
can be:

Can be set to <span class="typ-key">`none`</span> to disable the stroke
or to <span class="typ-key">`auto`</span> for a stroke of
<span class="typ-num">`1pt`</span> black if and if only if no fill is
given.


### vertices: array | _required_ _positional_

The vertices of the polygon. Each point is specified as an array of two
[relative lengths](/reference/layout/relative/).


## Definitions


### regular

```
polygon.regular(
    fill: none color gradient tiling
    stroke: none auto length color gradient stroke tiling dictionary
    size: length
    vertices: int
) -> content
```
A regular polygon, defined by its size and number of vertices.


##### Parameters


##### fill: none, color, gradient, tiling | _named_

How to fill the polygon. See the general [polygon's
documentation](/reference/visualize/polygon/#parameters-fill) for more
details.


##### stroke: none, auto, length, color, gradient, stroke, tiling, dictionary | _named_

How to stroke the polygon. See the general [polygon's
documentation](/reference/visualize/polygon/#parameters-stroke) for more
details.


##### size: length | _named_

The diameter of the
[circumcircle](https://en.wikipedia.org/wiki/Circumcircle) of the
regular polygon.


##### vertices: int | _named_

The number of vertices in the polygon.


#### Example

<div class="previewed-code">

    #polygon.regular(
      fill: blue.lighten(80%),
      stroke: blue,
      size: 30pt,
      vertices: 3,
    )

<div class="preview">

![Preview](/assets/9d2280c3e700486008c43a2bbf75321e.png)

</div>

</div>

