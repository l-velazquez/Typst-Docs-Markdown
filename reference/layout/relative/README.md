
# Relative Length

A length in relation to some known length.

This type is a combination of a
[length](/reference/layout/length/ "length") with a
[ratio](/reference/layout/ratio/ "ratio"). It results from addition and
subtraction of a length and a ratio. Wherever a relative length is
expected, you can also use a bare length or ratio.

## Relative to the page

A common use case is setting the width or height of a layout element
(e.g., [block](/reference/layout/block/ "block"),
[rect](/reference/visualize/rect/ "rect"), etc.) as a certain percentage
of the width of the page. Here, the rectangle's width is set to
<span class="typ-num">`25%`</span>, so it takes up one fourth of the
page's *inner* width (the width minus margins).

<div class="previewed-code">

    #rect(width: 25%)

<div class="preview">

![Preview](/assets/4d00e48a14d2fa6bbfde5bd85623a199.png)

</div>

</div>

Bare lengths or ratios are always valid where relative lengths are
expected, but the two can also be freely mixed:

<div class="previewed-code">

    #rect(width: 25% + 1cm)

<div class="preview">

![Preview](/assets/9dd66f878a23031069f8f03df39872fa.png)

</div>

</div>

If you're trying to size an element so that it takes up the page's
*full* width, you have a few options (this highly depends on your exact
use case):

1.  Set page margins to <span class="typ-num">`0pt`</span>
    (<span class="typ-key">`#`</span><span class="typ-key">`set`</span>` `<span class="typ-func">`page`</span><span class="typ-punct">`(`</span>`margin`<span class="typ-punct">`:`</span>` `<span class="typ-num">`0pt`</span><span class="typ-punct">`)`</span>)
2.  Multiply the ratio by the known full page width
    (<span class="typ-num">`21cm`</span>` `<span class="typ-op">`*`</span>` `<span class="typ-num">`69%`</span>)
3.  Use padding which will negate the margins
    (<span class="typ-func">`#`</span><span class="typ-func">`pad`</span><span class="typ-punct">`(`</span>`x`<span class="typ-punct">`:`</span>` `<span class="typ-op">`-`</span><span class="typ-num">`2.5cm`</span><span class="typ-punct">`,`</span>` `<span class="typ-op">`..`</span><span class="typ-punct">`.`</span><span class="typ-punct">`)`</span>)
4.  Use the page
    [background](/reference/layout/page/#parameters-background) or
    [foreground](/reference/layout/page/#parameters-foreground) field as
    those don't take margins into account (note that it will render the
    content outside of the document flow, see
    [place](/reference/layout/place/ "place") to control the content
    position)

## Relative to a container

When a layout element (e.g. a [rect](/reference/visualize/rect/ "rect"))
is nested in another layout container (e.g. a
[block](/reference/layout/block/ "block")) instead of being a direct
descendant of the page, relative widths become relative to the
container:

<div class="previewed-code">

    #block(
      width: 100pt,
      fill: aqua,
      rect(width: 50%),
    )

<div class="preview">

![Preview](/assets/402d58027e654e20b23526448886fb40.png)

</div>

</div>

## Scripting

You can multiply relative lengths by [ratios](/reference/layout/ratio/),
[integers](/reference/foundations/int/), and
[floats](/reference/foundations/float/).

A relative length has the following fields:

- `length`: Its length component.
- `ratio`: Its ratio component.

<div class="previewed-code">

    #(100% - 50pt).length \
    #(100% - 50pt).ratio

<div class="preview">

![Preview](/assets/d770a260705b27902b61e33e8c0a5f28.png)

</div>

</div>


## Definitions

