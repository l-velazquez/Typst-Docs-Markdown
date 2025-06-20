
# page

```
page(
    paper: str
    width: auto length
    height: auto length
    flipped: bool
    margin: auto relative dictionary
    binding: auto alignment
    columns: int
    fill: none auto color gradient tiling
    numbering: none str function
    supplement: none auto content
    number-align: alignment
    header: none auto content
    header-ascent: relative
    footer: none auto content
    footer-descent: relative
    background: none content
    foreground: none content
    content
) -> content
```
Layouts its child onto one or multiple pages.

Although this function is primarily used in set rules to affect page
properties, it can also be used to explicitly render its argument onto a
set of pages of its own.

Pages can be set to use <span class="typ-key">`auto`</span> as their
width or height. In this case, the pages will grow to fit their content
on the respective axis.

The [Guide for Page Setup](/guides/page-setup-guide/) explains how to
use this and related functions to set up a document with many examples.

## Example

<div class="previewed-code">

    #set page("us-letter")

    There you go, US friends!

<div class="preview">

![Preview](/assets/1ac9f7bf119f609244d0315ae70eada1.png)

</div>

</div>


### Parameters


### paper: str | _named_

A standard paper size to set width and height.

This is just a shorthand for setting `width` and `height` and, as such,
cannot be retrieved in a context expression.


### width: auto, length | _named_

The width of the page.


#### Example

<div class="previewed-code">

    #set page(
      width: 3cm,
      margin: (x: 0cm),
    )

    #for i in range(3) {
      box(square(width: 1cm))
    }

<div class="preview">

![Preview](/assets/c5c0cb479bae932e5a12726ba0fdc97d.png)

</div>

</div>


### height: auto, length | _named_

The height of the page.

If this is set to <span class="typ-key">`auto`</span>, page breaks can
only be triggered manually by inserting a [page
break](/reference/layout/pagebreak/) or by adding another non-empty page
set rule. Most examples throughout this documentation use
<span class="typ-key">`auto`</span> for the height of the page to
dynamically grow and shrink to fit their content.


### flipped: bool | _named_

Whether the page is flipped into landscape orientation.


#### Example

<div class="previewed-code">

    #set page(
      "us-business-card",
      flipped: true,
      fill: rgb("f2e5dd"),
    )

    #set align(bottom + end)
    #text(14pt)[*Sam H. Richards*] \
    _Procurement Manager_

    #set text(10pt)
    17 Main Street \
    New York, NY 10001 \
    +1 555 555 5555

<div class="preview">

![Preview](/assets/3443cc2c62d432e0b05c7641ea2bb708.png)

</div>

</div>


### margin: auto, relative, dictionary | _named_

The page's margins.

- <span class="typ-key">`auto`</span>: The margins are set automatically
  to 2.5/21 times the smaller dimension of the page. This results in
  2.5cm margins for an A4 page.
- A single length: The same margin on all sides.
- A dictionary: With a dictionary, the margins can be set individually.
  The dictionary can contain the following keys in order of precedence:
  - `top`: The top margin.
  - `right`: The right margin.
  - `bottom`: The bottom margin.
  - `left`: The left margin.
  - `inside`: The margin at the inner side of the page (where the
    [binding](/reference/layout/page/#parameters-binding) is).
  - `outside`: The margin at the outer side of the page (opposite to the
    [binding](/reference/layout/page/#parameters-binding)).
  - `x`: The horizontal margins.
  - `y`: The vertical margins.
  - `rest`: The margins on all sides except those for which the
    dictionary explicitly sets a size.

The values for `left` and `right` are mutually exclusive with the values
for `inside` and `outside`.


#### Example

<div class="previewed-code">

    #set page(
     width: 3cm,
     height: 4cm,
     margin: (x: 8pt, y: 4pt),
    )

    #rect(
      width: 100%,
      height: 100%,
      fill: aqua,
    )

<div class="preview">

![Preview](/assets/38cab24c8c7bc83c32353d035059e214.png)

</div>

</div>


### binding: auto, alignment | _named_

On which side the pages will be bound.

- <span class="typ-key">`auto`</span>: Equivalent to `left` if the [text
  direction](/reference/text/text/#parameters-dir) is left-to-right and
  `right` if it is right-to-left.
- `left`: Bound on the left side.
- `right`: Bound on the right side.

This affects the meaning of the `inside` and `outside` options for
margins.


### columns: int | _named_

How many columns the page has.

If you need to insert columns into a page or other container, you can
also use the [`columns` function](/reference/layout/columns/).


#### Example

<div class="previewed-code">

    #set page(columns: 2, height: 4.8cm)
    Climate change is one of the most
    pressing issues of our time, with
    the potential to devastate
    communities, ecosystems, and
    economies around the world. It's
    clear that we need to take urgent
    action to reduce our carbon
    emissions and mitigate the impacts
    of a rapidly changing climate.

<div class="preview">

![Preview](/assets/41e9bf3601743b2a7f2d8f0945514159.png)

</div>

</div>


### fill: none, auto, color, gradient, tiling | _named_

The page's background fill.

Setting this to something non-transparent instructs the printer to color
the complete page. If you are considering larger production runs, it may
be more environmentally friendly and cost-effective to source pre-dyed
pages and not set this property.

When set to <span class="typ-key">`none`</span>, the background becomes
transparent. Note that PDF pages will still appear with a (usually
white) background in viewers, but they are actually transparent. (If you
print them, no color is used for the background.)

The default of <span class="typ-key">`auto`</span> results in
<span class="typ-key">`none`</span> for PDF output, and `white` for PNG
and SVG.


#### Example

<div class="previewed-code">

    #set page(fill: rgb("444352"))
    #set text(fill: rgb("fdfdfd"))
    *Dark mode enabled.*

<div class="preview">

![Preview](/assets/3cb12cf6356d48cdc5c6ca004dae9200.png)

</div>

</div>


### numbering: none, str, function | _named_

How to [number](/reference/model/numbering/) the pages.

If an explicit `footer` (or `header` for top-aligned numbering) is
given, the numbering is ignored.


#### Example

<div class="previewed-code">

    #set page(
      height: 100pt,
      margin: (top: 16pt, bottom: 24pt),
      numbering: "1 / 1",
    )

    #lorem(48)

<div class="preview">

![Preview](/assets/458f1ff4e33685bdecfd0ded4b77d583.png)

</div>

</div>


### supplement: none, auto, content | _named_

A supplement for the pages.

For page references, this is added before the page number.


#### Example

<div class="previewed-code">

    #set page(numbering: "1.", supplement: [p.])

    = Introduction <intro>
    We are on #ref(<intro>, form: "page")!

<div class="preview">

![Preview](/assets/c75fa03fff6bfa8d16ee76ca5b278cbe.png)

</div>

</div>


### number-align: alignment | _named_

The alignment of the page numbering.

If the vertical component is `top`, the numbering is placed into the
header and if it is `bottom`, it is placed in the footer. Horizon
alignment is forbidden. If an explicit matching `header` or `footer` is
given, the numbering is ignored.


#### Example

<div class="previewed-code">

    #set page(
      margin: (top: 16pt, bottom: 24pt),
      numbering: "1",
      number-align: right,
    )

    #lorem(30)

<div class="preview">

![Preview](/assets/12bbe38d48e502ec6a76dce9bada9640.png)

</div>

</div>


### header: none, auto, content | _named_

The page's header. Fills the top margin of each page.

- Content: Shows the content as the header.
- <span class="typ-key">`auto`</span>: Shows the page number if a
  `numbering` is set and `number-align` is `top`.
- <span class="typ-key">`none`</span>: Suppresses the header.


#### Example

<div class="previewed-code">

    #set par(justify: true)
    #set page(
      margin: (top: 32pt, bottom: 20pt),
      header: [
        #set text(8pt)
        #smallcaps[Typst Academy]
        #h(1fr) _Exercise Sheet 3_
      ],
    )

    #lorem(19)

<div class="preview">

![Preview](/assets/b18fb365dc45c64d948757c6cca11852.png)

</div>

</div>


### header-ascent: relative | _named_

The amount the header is raised into the top margin.


### footer: none, auto, content | _named_

The page's footer. Fills the bottom margin of each page.

- Content: Shows the content as the footer.
- <span class="typ-key">`auto`</span>: Shows the page number if a
  `numbering` is set and `number-align` is `bottom`.
- <span class="typ-key">`none`</span>: Suppresses the footer.

For just a page number, the `numbering` property typically suffices. If
you want to create a custom footer but still display the page number,
you can directly access the [page
counter](/reference/introspection/counter/).


#### Example

<div class="previewed-code">

    #set par(justify: true)
    #set page(
      height: 100pt,
      margin: 20pt,
      footer: context [
        #set align(right)
        #set text(8pt)
        #counter(page).display(
          "1 of I",
          both: true,
        )
      ]
    )

    #lorem(48)

<div class="preview">

![Preview](/assets/18ae21d9e7d7e037a98c61a2523cde8d.png)

</div>

</div>


### footer-descent: relative | _named_

The amount the footer is lowered into the bottom margin.


### background: none, content | _named_

Content in the page's background.

This content will be placed behind the page's body. It can be used to
place a background image or a watermark.


#### Example

<div class="previewed-code">

    #set page(background: rotate(24deg,
      text(18pt, fill: rgb("FFCBC4"))[
        *CONFIDENTIAL*
      ]
    ))

    = Typst's secret plans
    In the year 2023, we plan to take
    over the world (of typesetting).

<div class="preview">

![Preview](/assets/79d32183be70b3e18882ae4824d25bad.png)

</div>

</div>


### foreground: none, content | _named_

Content in the page's foreground.

This content will overlay the page's body.


#### Example

<div class="previewed-code">

    #set page(foreground: text(24pt)[🥸])

    Reviewer 2 has marked our paper
    "Weak Reject" because they did
    not understand our approach...

<div class="preview">

![Preview](/assets/5310764e3bb4ce0e2787ce6130564d3b.png)

</div>

</div>


### body: content | _required_ _positional_

The contents of the page(s).

Multiple pages will be created if the content does not fit on a single
page. A new page with the page properties prior to the function
invocation will be created after the body has been typeset.

