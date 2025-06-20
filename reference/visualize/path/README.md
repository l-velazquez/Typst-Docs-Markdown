
# path

```
path(
    fill: none color gradient tiling
    fill-rule: str
    stroke: none auto length color gradient stroke tiling dictionary
    closed: bool
    array
) -> content
```
A path through a list of points, connected by Bézier curves.

## Example

<div class="previewed-code">

    #path(
      fill: blue.lighten(80%),
      stroke: blue,
      closed: true,
      (0pt, 50pt),
      (100%, 50pt),
      ((50%, 0pt), (40pt, 0pt)),
    )

<div class="preview">

![Preview](/assets/7c71fff7477a30492c8c5421fe00a40f.png)

</div>

</div>


### Parameters


### fill: none, color, gradient, tiling | _named_

How to fill the path.

When setting a fill, the default stroke disappears. To create a
rectangle with both fill and stroke, you have to configure both.


### fill-rule: str | _named_

The drawing rule used to fill the path.


#### Example

<div class="previewed-code">

    // We use `.with` to get a new
    // function that has the common
    // arguments pre-applied.
    #let star = path.with(
      fill: red,
      closed: true,
      (25pt, 0pt),
      (10pt, 50pt),
      (50pt, 20pt),
      (0pt, 20pt),
      (40pt, 50pt),
    )

    #star(fill-rule: "non-zero")
    #star(fill-rule: "even-odd")

<div class="preview">

![Preview](/assets/30910e51feb697b68ad0f1be1e5dc72a.png)

</div>

</div>


### stroke: none, auto, length, color, gradient, stroke, tiling, dictionary | _named_

How to [stroke](/reference/visualize/stroke/ "stroke") the path. This
can be:

Can be set to <span class="typ-key">`none`</span> to disable the stroke
or to <span class="typ-key">`auto`</span> for a stroke of
<span class="typ-num">`1pt`</span> black if and if only if no fill is
given.


### closed: bool | _named_

Whether to close this path with one last Bézier curve. This curve will
take into account the adjacent control points. If you want to close with
a straight line, simply add one last point that's the same as the start
point.


### vertices: array | _required_ _positional_

The vertices of the path.

Each vertex can be defined in 3 ways:

- A regular point, as given to the
  [`line`](/reference/visualize/line/ "`line`") or
  [`polygon`](/reference/visualize/polygon/ "`polygon`") function.
- An array of two points, the first being the vertex and the second
  being the control point. The control point is expressed relative to
  the vertex and is mirrored to get the second control point. The given
  control point is the one that affects the curve coming *into* this
  vertex (even for the first point). The mirrored control point affects
  the curve going out of this vertex.
- An array of three points, the first being the vertex and the next
  being the control points (control point for curves coming in and out,
  respectively).

