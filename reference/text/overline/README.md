
# overline

```
overline(
    stroke: auto length color gradient stroke tiling dictionary
    offset: auto length
    extent: length
    evade: bool
    background: bool
    content
) -> content
```
Adds a line over text.

## Example

<div class="previewed-code">

    #overline[A line over text.]

<div class="preview">

![Preview](/assets/50989a8ae293089193aedd0105c6c64.png)

</div>

</div>


### Parameters


### stroke: auto, length, color, gradient, stroke, tiling, dictionary | _named_

How to [stroke](/reference/visualize/stroke/ "stroke") the line.

If set to <span class="typ-key">`auto`</span>, takes on the text's color
and a thickness defined in the current font.


#### Example

<div class="previewed-code">

    #set text(fill: olive)
    #overline(
      stroke: green.darken(20%),
      offset: -12pt,
      [The Forest Theme],
    )

<div class="preview">

![Preview](/assets/8d710067177d3459c2b6071b0d597321.png)

</div>

</div>


### offset: auto, length | _named_

The position of the line relative to the baseline. Read from the font
tables if <span class="typ-key">`auto`</span>.


#### Example

<div class="previewed-code">

    #overline(offset: -1.2em)[
      The Tale Of A Faraway Line II
    ]

<div class="preview">

![Preview](/assets/1404884c3853de7e6a5eda657a4d3ae.png)

</div>

</div>


### extent: length | _named_

The amount by which to extend the line beyond (or within if negative)
the content.


#### Example

<div class="previewed-code">

    #set overline(extent: 4pt)
    #set underline(extent: 4pt)
    #overline(underline[Typography Today])

<div class="preview">

![Preview](/assets/d7574586783bdfe3cf728b98d641aec4.png)

</div>

</div>


### evade: bool | _named_

Whether the line skips sections in which it would collide with the
glyphs.


#### Example

<div class="previewed-code">

    #overline(
      evade: false,
      offset: -7.5pt,
      stroke: 1pt,
      extent: 3pt,
      [Temple],
    )

<div class="preview">

![Preview](/assets/e2dca96fc9f5aedf3819c18ac04be640.png)

</div>

</div>


### background: bool | _named_

Whether the line is placed behind the content it overlines.


#### Example

<div class="previewed-code">

    #set overline(stroke: (thickness: 1em, paint: maroon, cap: "round"))
    #overline(background: true)[This is stylized.] \
    #overline(background: false)[This is partially hidden.]

<div class="preview">

![Preview](/assets/275a85d06ae4812de1068593a2fad9fc.png)

</div>

</div>


### body: content | _required_ _positional_

The content to add a line over.

