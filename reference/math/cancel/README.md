
# cancel

```
math.cancel(
    content
    length: relative
    inverted: bool
    cross: bool
    angle: auto angle function
    stroke: length color gradient stroke tiling dictionary
) -> content
```
Displays a diagonal line over a part of an equation.

This is commonly used to show the elimination of a term.

## Example

<div class="previewed-code">

    Here, we can simplify:
    $ (a dot b dot cancel(x)) /
        cancel(x) $

<div class="preview">

![Preview](/assets/7d5119bd78ca4e4dacdd63bcf2ddcaf0.png)

</div>

</div>


### Parameters


### body: content | _required_ _positional_

The content over which the line should be placed.


### length: relative | _named_

The length of the line, relative to the length of the diagonal spanning
the whole element being "cancelled". A value of
<span class="typ-num">`100%`</span> would then have the line span
precisely the element's diagonal.


#### Example

<div class="previewed-code">

    $ a + cancel(x, length: #200%)
        - cancel(x, length: #200%) $

<div class="preview">

![Preview](/assets/fd148a56b3439c5e7fa4027244c99cac.png)

</div>

</div>


### inverted: bool | _named_

Whether the cancel line should be inverted (flipped along the y-axis).
For the default angle setting, inverted means the cancel line points to
the top left instead of top right.


#### Example

<div class="previewed-code">

    $ (a cancel((b + c), inverted: #true)) /
        cancel(b + c, inverted: #true) $

<div class="preview">

![Preview](/assets/19696e45aa5e672f241d0899e5cdd76d.png)

</div>

</div>


### cross: bool | _named_

Whether two opposing cancel lines should be drawn, forming a cross over
the element. Overrides `inverted`.


#### Example

<div class="previewed-code">

    $ cancel(Pi, cross: #true) $

<div class="preview">

![Preview](/assets/6e2222d3d2e291c0e7c1a03459a37025.png)

</div>

</div>


### angle: auto, angle, function | _named_

How much to rotate the cancel line.

- If given an angle, the line is rotated by that angle clockwise with
  respect to the y-axis.
- If <span class="typ-key">`auto`</span>, the line assumes the default
  angle; that is, along the rising diagonal of the content box.
- If given a function `angle => angle`, the line is rotated, with
  respect to the y-axis, by the angle returned by that function. The
  function receives the default angle as its input.


#### Example

<div class="previewed-code">

    $ cancel(Pi)
      cancel(Pi, angle: #0deg)
      cancel(Pi, angle: #45deg)
      cancel(Pi, angle: #90deg)
      cancel(1/(1+x), angle: #(a => a + 45deg))
      cancel(1/(1+x), angle: #(a => a + 90deg)) $

<div class="preview">

![Preview](/assets/38212630bf4a4126384abbb4ce4dd71b.png)

</div>

</div>


### stroke: length, color, gradient, stroke, tiling, dictionary | _named_

How to [stroke](/reference/visualize/stroke/) the cancel line.


#### Example

<div class="previewed-code">

    $ cancel(
      sum x,
      stroke: #(
        paint: red,
        thickness: 1.5pt,
        dash: "dashed",
      ),
    ) $

<div class="preview">

![Preview](/assets/28257b7a29918744372f166e763f080c.png)

</div>

</div>

