
# Stroke

Defines how to draw a line.

A stroke has a *paint* (a solid color or gradient), a *thickness,* a
line *cap,* a line *join,* a *miter limit,* and a *dash* pattern. All of
these values are optional and have sensible defaults.

## Example

<div class="previewed-code">

    #set line(length: 100%)
    #stack(
      spacing: 1em,
      line(stroke: 2pt + red),
      line(stroke: (paint: blue, thickness: 4pt, cap: "round")),
      line(stroke: (paint: blue, thickness: 1pt, dash: "dashed")),
      line(stroke: 2pt + gradient.linear(..color.map.rainbow)),
    )

<div class="preview">

![Preview](/assets/dcda1fb9b6f022596876c15ac2535df3.png)

</div>

</div>

## Simple strokes

You can create a simple solid stroke from a color, a thickness, or a
combination of the two. Specifically, wherever a stroke is expected you
can pass any of the following values:

- A length specifying the stroke's thickness. The color is inherited,
  defaulting to black.
- A color to use for the stroke. The thickness is inherited, defaulting
  to <span class="typ-num">`1pt`</span>.
- A stroke combined from color and thickness using the `+` operator as
  in
  <span class="typ-num">`2pt`</span>` `<span class="typ-op">`+`</span>` red`.

For full control, you can also provide a
[dictionary](/reference/foundations/dictionary/ "dictionary") or a
`stroke` object to any function that expects a stroke. The dictionary's
keys may include any of the parameters for the constructor function,
shown below.

## Fields

On a stroke object, you can access any of the fields listed in the
constructor function. For example,
<span class="typ-punct">`(`</span><span class="typ-num">`2pt`</span>` `<span class="typ-op">`+`</span>` blue`<span class="typ-punct">`)`</span><span class="typ-punct">`.`</span>`thickness`
is <span class="typ-num">`2pt`</span>. Meanwhile,
<span class="typ-func">`stroke`</span><span class="typ-punct">`(`</span>`red`<span class="typ-punct">`)`</span><span class="typ-punct">`.`</span>`cap`
is <span class="typ-key">`auto`</span> because it's unspecified. Fields
set to <span class="typ-key">`auto`</span> are inherited.


## stroke

```
stroke(
    auto color gradient tiling
    auto length
    auto str
    auto str
    none auto str array dictionary
    auto float
) -> stroke
```
Converts a value to a stroke or constructs a stroke with the given
parameters.

Note that in most cases you do not need to convert values to strokes in
order to use them, as they will be converted automatically. However,
this constructor can be useful to ensure a value has all the fields of a
stroke.


#### Parameters


#### paint: auto, color, gradient, tiling | _required_ _positional_

The color or gradient to use for the stroke.

If set to <span class="typ-key">`auto`</span>, the value is inherited,
defaulting to `black`.


#### thickness: auto, length | _required_ _positional_

The stroke's thickness.

If set to <span class="typ-key">`auto`</span>, the value is inherited,
defaulting to <span class="typ-num">`1pt`</span>.


#### cap: auto, str | _required_ _positional_

How the ends of the stroke are rendered.

If set to <span class="typ-key">`auto`</span>, the value is inherited,
defaulting to <span class="typ-str">`"butt"`</span>.


#### join: auto, str | _required_ _positional_

How sharp turns are rendered.

If set to <span class="typ-key">`auto`</span>, the value is inherited,
defaulting to <span class="typ-str">`"miter"`</span>.


#### dash: none, auto, str, array, dictionary | _required_ _positional_

The dash pattern to use. This can be:

- One of the predefined patterns:
  - <span class="typ-str">`"solid"`</span> or
    <span class="typ-key">`none`</span>
  - <span class="typ-str">`"dotted"`</span>
  - <span class="typ-str">`"densely-dotted"`</span>
  - <span class="typ-str">`"loosely-dotted"`</span>
  - <span class="typ-str">`"dashed"`</span>
  - <span class="typ-str">`"densely-dashed"`</span>
  - <span class="typ-str">`"loosely-dashed"`</span>
  - <span class="typ-str">`"dash-dotted"`</span>
  - <span class="typ-str">`"densely-dash-dotted"`</span>
  - <span class="typ-str">`"loosely-dash-dotted"`</span>
- An [array](/reference/foundations/array/ "array") with alternating
  lengths for dashes and gaps. You can also use the string
  <span class="typ-str">`"dot"`</span> for a length equal to the line
  thickness.
- A [dictionary](/reference/foundations/dictionary/ "dictionary") with
  the keys `array` (same as the array above), and `phase` (of type
  [length](/reference/layout/length/ "length")), which defines where in
  the pattern to start drawing.

If set to <span class="typ-key">`auto`</span>, the value is inherited,
defaulting to <span class="typ-key">`none`</span>.


##### Example

<div class="previewed-code">

    #set line(length: 100%, stroke: 2pt)
    #stack(
      spacing: 1em,
      line(stroke: (dash: "dashed")),
      line(stroke: (dash: (10pt, 5pt, "dot", 5pt))),
      line(stroke: (dash: (array: (10pt, 5pt, "dot", 5pt), phase: 10pt))),
    )

<div class="preview">

![Preview](/assets/3f7f20165b8a65cc3ae1675947ce671e.png)

</div>

</div>


#### miter-limit: auto, float | _required_ _positional_

Number at which protruding sharp bends are rendered with a bevel instead
or a miter join. The higher the number, the sharper an angle can be
before it is bevelled. Only applicable if `join` is
<span class="typ-str">`"miter"`</span>.

Specifically, the miter limit is the maximum ratio between the corner's
protrusion length and the stroke's thickness.

If set to <span class="typ-key">`auto`</span>, the value is inherited,
defaulting to <span class="typ-num">`4.0`</span>.


##### Example

<div class="previewed-code">

    #let items = (
      curve.move((15pt, 0pt)),
      curve.line((0pt, 30pt)),
      curve.line((30pt, 30pt)),
      curve.line((10pt, 20pt)),
    )

    #set curve(stroke: 6pt + blue)
    #stack(
      dir: ltr,
      spacing: 1cm,
      curve(stroke: (miter-limit: 1), ..items),
      curve(stroke: (miter-limit: 4), ..items),
      curve(stroke: (miter-limit: 5), ..items),
    )

<div class="preview">

![Preview](/assets/33818a9431604770d2115dd8e445c269.png)

</div>

</div>


### Example

<div class="previewed-code">

    #let my-func(x) = {
        x = stroke(x) // Convert to a stroke
        [Stroke has thickness #x.thickness.]
    }
    #my-func(3pt) \
    #my-func(red) \
    #my-func(stroke(cap: "round", thickness: 1pt))

<div class="preview">

![Preview](/assets/a2e95c5c335ca6e9c24b156f08f5cc25.png)

</div>

</div>


## Definitions

