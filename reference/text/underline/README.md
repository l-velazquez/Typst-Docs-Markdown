
# underline

```
underline(
    stroke: auto length color gradient stroke tiling dictionary
    offset: auto length
    extent: length
    evade: bool
    background: bool
    content
) -> content
```
Underlines text.

## Example

<div class="previewed-code">

    This is #underline[important].

<div class="preview">

![Preview](/assets/c55f85cbccf075521fc87c8ea5d93ff4.png)

</div>

</div>


### Parameters


### stroke: auto, length, color, gradient, stroke, tiling, dictionary | _named_

How to [stroke](/reference/visualize/stroke/ "stroke") the line.

If set to <span class="typ-key">`auto`</span>, takes on the text's color
and a thickness defined in the current font.


#### Example

<div class="previewed-code">

    Take #underline(
      stroke: 1.5pt + red,
      offset: 2pt,
      [care],
    )

<div class="preview">

![Preview](/assets/b5b2ca73d8986a085d842f4d70968939.png)

</div>

</div>


### offset: auto, length | _named_

The position of the line relative to the baseline, read from the font
tables if <span class="typ-key">`auto`</span>.


#### Example

<div class="previewed-code">

    #underline(offset: 5pt)[
      The Tale Of A Faraway Line I
    ]

<div class="preview">

![Preview](/assets/a76b54597718abe13f65b0edc33083ac.png)

</div>

</div>


### extent: length | _named_

The amount by which to extend the line beyond (or within if negative)
the content.


#### Example

<div class="previewed-code">

    #align(center,
      underline(extent: 2pt)[Chapter 1]
    )

<div class="preview">

![Preview](/assets/b5b4f604e2cfb5c5d6f9a9503dbf2aeb.png)

</div>

</div>


### evade: bool | _named_

Whether the line skips sections in which it would collide with the
glyphs.


#### Example

<div class="previewed-code">

    This #underline(evade: true)[is great].
    This #underline(evade: false)[is less great].

<div class="preview">

![Preview](/assets/3da25cdaa529a21d6cf7b13a359633d1.png)

</div>

</div>


### background: bool | _named_

Whether the line is placed behind the content it underlines.


#### Example

<div class="previewed-code">

    #set underline(stroke: (thickness: 1em, paint: maroon, cap: "round"))
    #underline(background: true)[This is stylized.] \
    #underline(background: false)[This is partially hidden.]

<div class="preview">

![Preview](/assets/5bdf0cec09671684959e5b7d8396c8b0.png)

</div>

</div>


### body: content | _required_ _positional_

The content to underline.

