
# line

```
line(
    start: array
    end: none array
    length: relative
    angle: angle
    stroke: length color gradient stroke tiling dictionary
) -> content
```
A line from one point to another.

## Example

<div class="previewed-code">

    #set page(height: 100pt)

    #line(length: 100%)
    #line(end: (50%, 50%))
    #line(
      length: 4cm,
      stroke: 2pt + maroon,
    )

<div class="preview">

![Preview](/assets/20174b08a5b487d90d5ace96ffc0ca03.png)

</div>

</div>


### Parameters


### start: array | _named_

The start point of the line.

Must be an array of exactly two relative lengths.


### end: none, array | _named_

The point where the line ends.


### length: relative | _named_

The line's length. This is only respected if `end` is
<span class="typ-key">`none`</span>.


### angle: angle | _named_

The angle at which the line points away from the origin. This is only
respected if `end` is <span class="typ-key">`none`</span>.


### stroke: length, color, gradient, stroke, tiling, dictionary | _named_

How to [stroke](/reference/visualize/stroke/ "stroke") the line.


#### Example

<div class="previewed-code">

    #set line(length: 100%)
    #stack(
      spacing: 1em,
      line(stroke: 2pt + red),
      line(stroke: (paint: blue, thickness: 4pt, cap: "round")),
      line(stroke: (paint: blue, thickness: 1pt, dash: "dashed")),
      line(stroke: (paint: blue, thickness: 1pt, dash: ("dot", 2pt, 4pt, 2pt))),
    )

<div class="preview">

![Preview](/assets/4a1c2aa65f57ad6920e80d57cc1a24e8.png)

</div>

</div>

