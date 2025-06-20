
# highlight

```
highlight(
    fill: none color gradient tiling
    stroke: none length color gradient stroke tiling dictionary
    top-edge: length str
    bottom-edge: length str
    extent: length
    radius: relative dictionary
    content
) -> content
```
Highlights text with a background color.

## Example

<div class="previewed-code">

    This is #highlight[important].

<div class="preview">

![Preview](/assets/42da40ea2afd5161477973d1af6803f4.png)

</div>

</div>


### Parameters


### fill: none, color, gradient, tiling | _named_

The color to highlight the text with.


#### Example

<div class="previewed-code">

    This is #highlight(
      fill: blue
    )[highlighted with blue].

<div class="preview">

![Preview](/assets/a16fbe0f26297ecde73ff95938897ae6.png)

</div>

</div>


### stroke: none, length, color, gradient, stroke, tiling, dictionary | _named_

The highlight's border color. See the [rectangle's
documentation](/reference/visualize/rect/#parameters-stroke) for more
details.


#### Example

<div class="previewed-code">

    This is a #highlight(
      stroke: fuchsia
    )[stroked highlighting].

<div class="preview">

![Preview](/assets/55d6650499e446077347fe0beb9ccacd.png)

</div>

</div>


### top-edge: length, str | _named_

The top end of the background rectangle.


#### Example

<div class="previewed-code">

    #set highlight(top-edge: "ascender")
    #highlight[a] #highlight[aib]

    #set highlight(top-edge: "x-height")
    #highlight[a] #highlight[aib]

<div class="preview">

![Preview](/assets/df7c3a2968aabd2accab8d62139a1bfd.png)

</div>

</div>


### bottom-edge: length, str | _named_

The bottom end of the background rectangle.


#### Example

<div class="previewed-code">

    #set highlight(bottom-edge: "descender")
    #highlight[a] #highlight[ap]

    #set highlight(bottom-edge: "baseline")
    #highlight[a] #highlight[ap]

<div class="preview">

![Preview](/assets/b594de9ba44041727c385cc8acbe809c.png)

</div>

</div>


### extent: length | _named_

The amount by which to extend the background to the sides beyond (or
within if negative) the content.


#### Example

<div class="previewed-code">

    A long #highlight(extent: 4pt)[background].

<div class="preview">

![Preview](/assets/2f6c1fda8ce0be0320da2237151f4b75.png)

</div>

</div>


### radius: relative, dictionary | _named_

How much to round the highlight's corners. See the [rectangle's
documentation](/reference/visualize/rect/#parameters-radius) for more
details.


#### Example

<div class="previewed-code">

    Listen #highlight(
      radius: 5pt, extent: 2pt
    )[carefully], it will be on the test.

<div class="preview">

![Preview](/assets/31d0f4700eee1a1ee9db3df6dfcd3f90.png)

</div>

</div>


### body: content | _required_ _positional_

The content that should be highlighted.

