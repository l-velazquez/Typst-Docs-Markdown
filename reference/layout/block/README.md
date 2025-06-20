
# block

```
block(
    width: auto relative
    height: auto relative fraction
    breakable: bool
    fill: none color gradient tiling
    stroke: none length color gradient stroke tiling dictionary
    radius: relative dictionary
    inset: relative dictionary
    outset: relative dictionary
    spacing: relative fraction
    above: auto relative fraction
    below: auto relative fraction
    clip: bool
    sticky: bool
    none content
) -> content
```
A block-level container.

Such a container can be used to separate content, size it, and give it a
background or border.

Blocks are also the primary way to control whether text becomes part of
a paragraph or not. See [the paragraph
documentation](/reference/model/par/#what-becomes-a-paragraph) for more
details.

## Examples

With a block, you can give a background to content while still allowing
it to break across multiple pages.

<div class="previewed-code">

    #set page(height: 100pt)
    #block(
      fill: luma(230),
      inset: 8pt,
      radius: 4pt,
      lorem(30),
    )

<div class="preview">

![Preview](/assets/d35b757571be311e1c4ebaa94cc073.png)

</div>

</div>

Blocks are also useful to force elements that would otherwise be inline
to become block-level, especially when writing show rules.

<div class="previewed-code">

    #show heading: it => it.body
    = Blockless
    More text.

    #show heading: it => block(it.body)
    = Blocky
    More text.

<div class="preview">

![Preview](/assets/a31ac3f6f1c0a9c6fef602c490517f3d.png)

</div>

</div>


### Parameters


### width: auto, relative | _named_

The block's width.


#### Example

<div class="previewed-code">

    #set align(center)
    #block(
      width: 60%,
      inset: 8pt,
      fill: silver,
      lorem(10),
    )

<div class="preview">

![Preview](/assets/ae64d29594fe17355970f40654b3888b.png)

</div>

</div>


### height: auto, relative, fraction | _named_

The block's height. When the height is larger than the remaining space
on a page and
[`breakable`](/reference/layout/block/#parameters-breakable) is
<span class="typ-key">`true`</span>, the block will continue on the next
page with the remaining height.


#### Example

<div class="previewed-code">

    #set page(height: 80pt)
    #set align(center)
    #block(
      width: 80%,
      height: 150%,
      fill: aqua,
    )

<div class="preview">

![Preview](/assets/95ecf1fed181223374cbbda47ab8fbc9.png)

</div>

</div>


### breakable: bool | _named_

Whether the block can be broken and continue on the next page.


#### Example

<div class="previewed-code">

    #set page(height: 80pt)
    The following block will
    jump to its own page.
    #block(
      breakable: false,
      lorem(15),
    )

<div class="preview">

![Preview](/assets/2381cccce0230146d6f912b46bf6151c.png)

</div>

</div>


### fill: none, color, gradient, tiling | _named_

The block's background color. See the [rectangle's
documentation](/reference/visualize/rect/#parameters-fill) for more
details.


### stroke: none, length, color, gradient, stroke, tiling, dictionary | _named_

The block's border color. See the [rectangle's
documentation](/reference/visualize/rect/#parameters-stroke) for more
details.


### radius: relative, dictionary | _named_

How much to round the block's corners. See the [rectangle's
documentation](/reference/visualize/rect/#parameters-radius) for more
details.


### inset: relative, dictionary | _named_

How much to pad the block's content. See the [box's
documentation](/reference/layout/box/#parameters-inset) for more
details.


### outset: relative, dictionary | _named_

How much to expand the block's size without affecting the layout. See
the [box's documentation](/reference/layout/box/#parameters-outset) for
more details.


### spacing: relative, fraction | _named_

The spacing around the block. When <span class="typ-key">`auto`</span>,
inherits the paragraph
[`spacing`](/reference/model/par/#parameters-spacing).

For two adjacent blocks, the larger of the first block's `above` and the
second block's `below` spacing wins. Moreover, block spacing takes
precedence over paragraph
[`spacing`](/reference/model/par/#parameters-spacing).

Note that this is only a shorthand to set `above` and `below` to the
same value. Since the values for `above` and `below` might differ, a
[context](/reference/context/ "context") block only provides access to
`block`<span class="typ-punct">`.`</span>`above` and
`block`<span class="typ-punct">`.`</span>`below`, not to
`block`<span class="typ-punct">`.`</span>`spacing` directly.

This property can be used in combination with a show rule to adjust the
spacing around arbitrary block-level elements.


#### Example

<div class="previewed-code">

    #set align(center)
    #show math.equation: set block(above: 8pt, below: 16pt)

    This sum of $x$ and $y$:
    $ x + y = z $
    A second paragraph.

<div class="preview">

![Preview](/assets/f99d00eb0b5ee536c467a984c133ef9e.png)

</div>

</div>


### above: auto, relative, fraction | _named_

The spacing between this block and its predecessor.


### below: auto, relative, fraction | _named_

The spacing between this block and its successor.


### clip: bool | _named_

Whether to clip the content inside the block.

Clipping is useful when the block's content is larger than the block
itself, as any content that exceeds the block's bounds will be hidden.


#### Example

<div class="previewed-code">

    #block(
      width: 50pt,
      height: 50pt,
      clip: true,
      image("tiger.jpg", width: 100pt, height: 100pt)
    )

<div class="preview">

![Preview](/assets/555e171d6e5e2c7fe5b28e8cc072baa5.png)

</div>

</div>


### sticky: bool | _named_

Whether this block must stick to the following one, with no break in
between.

This is, by default, set on heading blocks to prevent orphaned headings
at the bottom of the page.


#### Example

<div class="previewed-code">

    // Disable stickiness of headings.
    #show heading: set block(sticky: false)
    #lorem(20)

    = Chapter
    #lorem(10)

<div class="preview">

![Preview](/assets/f6b4eb2256c858de9f455dbe80ea228d.png)

</div>

</div>


### body: none, content | _positional_

The contents of the block.

