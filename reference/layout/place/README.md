
# place

```
place(
    auto alignment
    scope: str
    float: bool
    clearance: length
    dx: relative
    dy: relative
    content
) -> content
```
Places content relatively to its parent container.

Placed content can be either overlaid (the default) or floating.
Overlaid content is aligned with the parent container according to the
given [`alignment`](/reference/layout/place/#parameters-alignment), and
shown over any other content added so far in the container. Floating
content is placed at the top or bottom of the container, displacing
other content down or up respectively. In both cases, the content
position can be adjusted with
[`dx`](/reference/layout/place/#parameters-dx) and
[`dy`](/reference/layout/place/#parameters-dy) offsets without affecting
the layout.

The parent can be any container such as a
[`block`](/reference/layout/block/ "`block`"),
[`box`](/reference/layout/box/ "`box`"),
[`rect`](/reference/visualize/rect/ "`rect`"), etc. A top level `place`
call will place content directly in the text area of the current page.
This can be used for absolute positioning on the page: with a
`top + left`
[`alignment`](/reference/layout/place/#parameters-alignment), the
offsets `dx` and `dy` will set the position of the element's top left
corner relatively to the top left corner of the text area. For absolute
positioning on the full page including margins, you can use `place` in
[`page.foreground`](/reference/layout/page/#parameters-foreground) or
[`page.background`](/reference/layout/page/#parameters-background).

## Examples

<div class="previewed-code">

    #set page(height: 120pt)
    Hello, world!

    #rect(
      width: 100%,
      height: 2cm,
      place(horizon + right, square()),
    )

    #place(
      top + left,
      dx: -5pt,
      square(size: 5pt, fill: red),
    )

<div class="preview">

![Preview](/assets/6f751edfbb0d9761c3a6c972a39b6b7e.png)

</div>

</div>

## Effect on the position of other elements

Overlaid elements don't take space in the flow of content, but a `place`
call inserts an invisible block-level element in the flow. This can
affect the layout by breaking the current paragraph. To avoid this, you
can wrap the `place` call in a [`box`](/reference/layout/box/ "`box`")
when the call is made in the middle of a paragraph. The alignment and
offsets will then be relative to this zero-size box. To make sure it
doesn't interfere with spacing, the box should be attached to a word
using a word joiner.

For example, the following defines a function for attaching an
annotation to the following word:

<div class="previewed-code">

    #let annotate(..args) = {
      box(place(..args))
      sym.wj
      h(0pt, weak: true)
    }

    A placed #annotate(square(), dy: 2pt)
    square in my text.

<div class="preview">

![Preview](/assets/40826a3ec000a798ea7be101e1b645d6.png)

</div>

</div>

The zero-width weak spacing serves to discard spaces between the
function call and the next word.


### Parameters


### alignment: auto, alignment | _positional_

Relative to which position in the parent container to place the content.

- If `float` is <span class="typ-key">`false`</span>, then this can be
  any alignment other than <span class="typ-key">`auto`</span>.
- If `float` is <span class="typ-key">`true`</span>, then this must be
  <span class="typ-key">`auto`</span>, `top`, or `bottom`.

When `float` is <span class="typ-key">`false`</span> and no vertical
alignment is specified, the content is placed at the current position on
the vertical axis.


### scope: str | _named_

Relative to which containing scope something is placed.

The parent scope is primarily used with figures and, for this reason,
the figure function has a mirrored [`scope`
parameter](/reference/model/figure/#parameters-scope). Nonetheless, it
can also be more generally useful to break out of the columns. A typical
example would be to [create a single-column title
section](/guides/page-setup-guide/#columns) in a two-column document.

Note that parent-scoped placement is currently only supported if `float`
is <span class="typ-key">`true`</span>. This may change in the future.


#### Example

<div class="previewed-code">

    #set page(height: 150pt, columns: 2)
    #place(
      top + center,
      scope: "parent",
      float: true,
      rect(width: 80%, fill: aqua),
    )

    #lorem(25)

<div class="preview">

![Preview](/assets/f718445c168dda0dcdf558eeec653317.png)

</div>

</div>


### float: bool | _named_

Whether the placed element has floating layout.

Floating elements are positioned at the top or bottom of the parent
container, displacing in-flow content. They are always placed in the
in-flow order relative to each other, as well as before any content
following a later
[`place.flush`](/reference/layout/place/#definitions-flush "`place.flush`")
element.


#### Example

<div class="previewed-code">

    #set page(height: 150pt)
    #let note(where, body) = place(
      center + where,
      float: true,
      clearance: 6pt,
      rect(body),
    )

    #lorem(10)
    #note(bottom)[Bottom 1]
    #note(bottom)[Bottom 2]
    #lorem(40)
    #note(top)[Top]
    #lorem(10)

<div class="preview">

![Preview](/assets/b79489e3dba54a5087e52813387db424.png)

</div>

</div>


### clearance: length | _named_

The spacing between the placed element and other elements in a floating
layout.

Has no effect if `float` is <span class="typ-key">`false`</span>.


### dx: relative | _named_

The horizontal displacement of the placed content.


#### Example

<div class="previewed-code">

    #set page(height: 100pt)
    #for i in range(16) {
      let amount = i * 4pt
      place(center, dx: amount - 32pt, dy: amount)[A]
    }

<div class="preview">

![Preview](/assets/900a86ccdad2c8f732b5d603c1366069.png)

</div>

</div>

This does not affect the layout of in-flow content. In other words, the
placed content is treated as if it were wrapped in a
[`move`](/reference/layout/move/ "`move`") element.


### dy: relative | _named_

The vertical displacement of the placed content.

This does not affect the layout of in-flow content. In other words, the
placed content is treated as if it were wrapped in a
[`move`](/reference/layout/move/ "`move`") element.


### body: content | _required_ _positional_

The content to place.


## Definitions


### flush

```
place.flush(
) -> content
```
Asks the layout algorithm to place pending floating elements before
continuing with the content.

This is useful for preventing floating figures from spilling into the
next section.


##### Parameters


#### Example

<div class="previewed-code">

    #lorem(15)

    #figure(
      rect(width: 100%, height: 50pt),
      placement: auto,
      caption: [A rectangle],
    )

    #place.flush()

    This text appears after the figure.

<div class="preview">

![Preview](/assets/f2aa79bdf50898cb675e77738d00ac35.png)

</div>

</div>

