
# curve

```
curve(
    fill: none color gradient tiling
    fill-rule: str
    stroke: none auto length color gradient stroke tiling dictionary
    content
) -> content
```
A curve consisting of movements, lines, and Bézier segments.

At any point in time, there is a conceptual pen or cursor.

- Move elements move the cursor without drawing.
- Line/Quadratic/Cubic elements draw a segment from the cursor to a new
  position, potentially with control point for a Bézier curve.
- Close elements draw a straight or smooth line back to the start of the
  curve or the latest preceding move segment.

For layout purposes, the bounding box of the curve is a tight rectangle
containing all segments as well as the point
<span class="typ-punct">`(`</span><span class="typ-num">`0pt`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`0pt`</span><span class="typ-punct">`)`</span>.

Positions may be specified absolutely (i.e. relatively to
<span class="typ-punct">`(`</span><span class="typ-num">`0pt`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`0pt`</span><span class="typ-punct">`)`</span>),
or relative to the current pen/cursor position, that is, the position
where the previous segment ended.

Bézier curve control points can be skipped by passing
<span class="typ-key">`none`</span> or automatically mirrored from the
preceding segment by passing <span class="typ-key">`auto`</span>.

## Example

<div class="previewed-code">

    #curve(
      fill: blue.lighten(80%),
      stroke: blue,
      curve.move((0pt, 50pt)),
      curve.line((100pt, 50pt)),
      curve.cubic(none, (90pt, 0pt), (50pt, 0pt)),
      curve.close(),
    )

<div class="preview">

![Preview](/assets/f6e8a1340bbf7443c9b7a46b757beca4.png)

</div>

</div>


### Parameters


### fill: none, color, gradient, tiling | _named_

How to fill the curve.

When setting a fill, the default stroke disappears. To create a
rectangle with both fill and stroke, you have to configure both.


### fill-rule: str | _named_

The drawing rule used to fill the curve.


#### Example

<div class="previewed-code">

    // We use `.with` to get a new
    // function that has the common
    // arguments pre-applied.
    #let star = curve.with(
      fill: red,
      curve.move((25pt, 0pt)),
      curve.line((10pt, 50pt)),
      curve.line((50pt, 20pt)),
      curve.line((0pt, 20pt)),
      curve.line((40pt, 50pt)),
      curve.close(),
    )

    #star(fill-rule: "non-zero")
    #star(fill-rule: "even-odd")

<div class="preview">

![Preview](/assets/32d08694d1725fb4fc044b295913753b.png)

</div>

</div>


### stroke: none, auto, length, color, gradient, stroke, tiling, dictionary | _named_

How to [stroke](/reference/visualize/stroke/ "stroke") the curve. This
can be:

Can be set to <span class="typ-key">`none`</span> to disable the stroke
or to <span class="typ-key">`auto`</span> for a stroke of
<span class="typ-num">`1pt`</span> black if and if only if no fill is
given.


#### Example

<div class="previewed-code">

    #let down = curve.line((40pt, 40pt), relative: true)
    #let up = curve.line((40pt, -40pt), relative: true)

    #curve(
      stroke: 4pt + gradient.linear(red, blue),
      down, up, down, up, down,
    )

<div class="preview">

![Preview](/assets/6e6243695ed1c92082c2dfde5dadc46.png)

</div>

</div>


### components: content | _required_ _positional_

The components of the curve, in the form of moves, line and Bézier
segment, and closes.


## Definitions


### move

```
curve.move(
    array
    relative: bool
) -> content
```
Starts a new curve component.

If no `curve.move` element is passed, the curve will start at
<span class="typ-punct">`(`</span><span class="typ-num">`0pt`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`0pt`</span><span class="typ-punct">`)`</span>.


##### Parameters


##### start: array | _required_ _positional_

The starting point for the new component.


##### relative: bool | _named_

Whether the coordinates are relative to the previous point.


#### Example

<div class="previewed-code">

    #curve(
      fill: blue.lighten(80%),
      fill-rule: "even-odd",
      stroke: blue,
      curve.line((50pt, 0pt)),
      curve.line((50pt, 50pt)),
      curve.line((0pt, 50pt)),
      curve.close(),
      curve.move((10pt, 10pt)),
      curve.line((40pt, 10pt)),
      curve.line((40pt, 40pt)),
      curve.line((10pt, 40pt)),
      curve.close(),
    )

<div class="preview">

![Preview](/assets/1955d468f48167d68b38f68a29541b16.png)

</div>

</div>


### line

```
curve.line(
    array
    relative: bool
) -> content
```
Adds a straight line from the current point to a following one.


##### Parameters


##### end: array | _required_ _positional_

The point at which the line shall end.


##### relative: bool | _named_

Whether the coordinates are relative to the previous point.


###### Example

<div class="previewed-code">

    #curve(
      stroke: blue,
      curve.line((50pt, 0pt), relative: true),
      curve.line((0pt, 50pt), relative: true),
      curve.line((50pt, 0pt), relative: true),
      curve.line((0pt, -50pt), relative: true),
      curve.line((50pt, 0pt), relative: true),
    )

<div class="preview">

![Preview](/assets/a1d4c814689467eb4fff957d859d4f8f.png)

</div>

</div>


#### Example

<div class="previewed-code">

    #curve(
      stroke: blue,
      curve.line((50pt, 0pt)),
      curve.line((50pt, 50pt)),
      curve.line((100pt, 50pt)),
      curve.line((100pt, 0pt)),
      curve.line((150pt, 0pt)),
    )

<div class="preview">

![Preview](/assets/876b0adef11ce302e948d0dcfb2f286e.png)

</div>

</div>


### quad

```
curve.quad(
    none auto array
    array
    relative: bool
) -> content
```
Adds a quadratic Bézier curve segment from the last point to `end`,
using `control` as the control point.


##### Parameters


##### control: none, auto, array | _required_ _positional_

The control point of the quadratic Bézier curve.

- If <span class="typ-key">`auto`</span> and this segment follows
  another quadratic Bézier curve, the previous control point will be
  mirrored.
- If <span class="typ-key">`none`</span>, the control point defaults to
  `end`, and the curve will be a straight line.


###### Example

<div class="previewed-code">

    #curve(
      stroke: 2pt,
      curve.quad((20pt, 40pt), (40pt, 40pt), relative: true),
      curve.quad(auto, (40pt, -40pt), relative: true),
    )

<div class="preview">

![Preview](/assets/d47ff1e09330a54c9073cc1acf9d4f7d.png)

</div>

</div>


##### end: array | _required_ _positional_

The point at which the segment shall end.


##### relative: bool | _named_

Whether the `control` and `end` coordinates are relative to the previous
point.


#### Example

<div class="previewed-code">

    // Function to illustrate where the control point is.
    #let mark((x, y)) = place(
      dx: x - 1pt, dy: y - 1pt,
      circle(fill: aqua, radius: 2pt),
    )

    #mark((20pt, 20pt))

    #curve(
      stroke: blue,
      curve.move((0pt, 100pt)),
      curve.quad((20pt, 20pt), (100pt, 0pt)),
    )

<div class="preview">

![Preview](/assets/724a52e2ec967c1d8032ca86a12f48a9.png)

</div>

</div>


### cubic

```
curve.cubic(
    none auto array
    none array
    array
    relative: bool
) -> content
```
Adds a cubic Bézier curve segment from the last point to `end`, using
`control-start` and `control-end` as the control points.


##### Parameters


##### control-start: none, auto, array | _required_ _positional_

The control point going out from the start of the curve segment.

- If <span class="typ-key">`auto`</span> and this element follows
  another `curve.cubic` element, the last control point will be
  mirrored. In SVG terms, this makes `curve.cubic` behave like the `S`
  operator instead of the `C` operator.

- If <span class="typ-key">`none`</span>, the curve has no first control
  point, or equivalently, the control point defaults to the curve's
  starting point.


###### Example

<div class="previewed-code">

    #curve(
      stroke: blue,
      curve.move((0pt, 50pt)),
      // - No start control point
      // - End control point at `(20pt, 0pt)`
      // - End point at `(50pt, 0pt)`
      curve.cubic(none, (20pt, 0pt), (50pt, 0pt)),
      // - No start control point
      // - No end control point
      // - End point at `(50pt, 0pt)`
      curve.cubic(none, none, (100pt, 50pt)),
    )

    #curve(
      stroke: blue,
      curve.move((0pt, 50pt)),
      curve.cubic(none, (20pt, 0pt), (50pt, 0pt)),
      // Passing `auto` instead of `none` means the start control point
      // mirrors the end control point of the previous curve. Mirror of
      // `(20pt, 0pt)` w.r.t `(50pt, 0pt)` is `(80pt, 0pt)`.
      curve.cubic(auto, none, (100pt, 50pt)),
    )

    #curve(
      stroke: blue,
      curve.move((0pt, 50pt)),
      curve.cubic(none, (20pt, 0pt), (50pt, 0pt)),
      // `(80pt, 0pt)` is the same as `auto` in this case.
      curve.cubic((80pt, 0pt), none, (100pt, 50pt)),
    )

<div class="preview">

![Preview](/assets/ac3fb4a5274f0715a91fd3627b8c32dd.png)

</div>

</div>


##### control-end: none, array | _required_ _positional_

The control point going into the end point of the curve segment.

If set to <span class="typ-key">`none`</span>, the curve has no end
control point, or equivalently, the control point defaults to the
curve's end point.


##### end: array | _required_ _positional_

The point at which the curve segment shall end.


##### relative: bool | _named_

Whether the `control-start`, `control-end`, and `end` coordinates are
relative to the previous point.


#### Example

<div class="previewed-code">

    // Function to illustrate where the control points are.
    #let handle(start, end) = place(
      line(stroke: red, start: start, end: end)
    )

    #handle((0pt, 80pt), (10pt, 20pt))
    #handle((90pt, 60pt), (100pt, 0pt))

    #curve(
      stroke: blue,
      curve.move((0pt, 80pt)),
      curve.cubic((10pt, 20pt), (90pt, 60pt), (100pt, 0pt)),
    )

<div class="preview">

![Preview](/assets/7a591ac9cdc0f51d93baa039d0a04122.png)

</div>

</div>


### close

```
curve.close(
    mode: str
) -> content
```
Closes the curve by adding a segment from the last point to the start of
the curve (or the last preceding `curve.move` point).


##### Parameters


##### mode: str | _named_

How to close the curve.


#### Example

<div class="previewed-code">

    // We define a function to show the same shape with
    // both closing modes.
    #let shape(mode: "smooth") = curve(
      fill: blue.lighten(80%),
      stroke: blue,
      curve.move((0pt, 50pt)),
      curve.line((100pt, 50pt)),
      curve.cubic(auto, (90pt, 0pt), (50pt, 0pt)),
      curve.close(mode: mode),
    )

    #shape(mode: "smooth")
    #shape(mode: "straight")

<div class="preview">

![Preview](/assets/f4f90ea216d7104ae8866f4ba7a726.png)

</div>

</div>

