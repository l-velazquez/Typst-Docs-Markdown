
# par

```
par(
    leading: length
    spacing: length
    justify: bool
    linebreaks: auto str
    first-line-indent: length dictionary
    hanging-indent: length
    content
) -> content
```
A logical subdivison of textual content.

Typst automatically collects *inline-level* elements into paragraphs.
Inline-level elements include [text](/reference/text/text/ "text"),
[horizontal spacing](/reference/layout/h/),
[boxes](/reference/layout/box/), and [inline
equations](/reference/math/equation/).

To separate paragraphs, use a blank line (or an explicit
[`parbreak`](/reference/model/parbreak/ "`parbreak`")). Paragraphs are
also automatically interrupted by any block-level element (like
[`block`](/reference/layout/block/ "`block`"),
[`place`](/reference/layout/place/ "`place`"), or anything that shows
itself as one of these).

The `par` element is primarily used in set rules to affect paragraph
properties, but it can also be used to explicitly display its argument
as a paragraph of its own. Then, the paragraph's body may not contain
any block-level content.

## Boxes and blocks

As explained above, usually paragraphs only contain inline-level
content. However, you can integrate any kind of block-level content into
a paragraph by wrapping it in a [`box`](/reference/layout/box/ "`box`").

Conversely, you can separate inline-level content from a paragraph by
wrapping it in a [`block`](/reference/layout/block/ "`block`"). In this
case, it will not become part of any paragraph at all. Read the
following section for an explanation of why that matters and how it
differs from just adding paragraph breaks around the content.

## What becomes a paragraph?

When you add inline-level content to your document, Typst will
automatically wrap it in paragraphs. However, a typical document also
contains some text that is not semantically part of a paragraph, for
example in a heading or caption.

The rules for when Typst wraps inline-level content in a paragraph are
as follows:

- All text at the root of a document is wrapped in paragraphs.

- Text in a container (like a `block`) is only wrapped in a paragraph if
  the container holds any block-level content. If all of the contents
  are inline-level, no paragraph is created.

In the laid-out document, it's not immediately visible whether text
became part of a paragraph. However, it is still important for various
reasons:

- Certain paragraph styling like `first-line-indent` will only apply to
  proper paragraphs, not any text. Similarly, `par` show rules of course
  only trigger on paragraphs.

- A proper distinction between paragraphs and other text helps people
  who rely on assistive technologies (such as screen readers) navigate
  and understand the document properly. Currently, this only applies to
  HTML export since Typst does not yet output accessible PDFs, but
  support for this is planned for the near future.

- HTML export will generate a `<p>` tag only for paragraphs.

When creating custom reusable components, you can and should take charge
over whether Typst creates paragraphs. By wrapping text in a
[`block`](/reference/layout/block/ "`block`") instead of just adding
paragraph breaks around it, you can force the absence of a paragraph.
Conversely, by adding a
[`parbreak`](/reference/model/parbreak/ "`parbreak`") after some content
in a container, you can force it to become a paragraph even if it's just
one word. This is, for example, what
[non-`tight`](/reference/model/list/#parameters-tight) lists do to force
their items to become paragraphs.

## Example

<div class="previewed-code">

    #set par(
      first-line-indent: 1em,
      spacing: 0.65em,
      justify: true,
    )

    We proceed by contradiction.
    Suppose that there exists a set
    of positive integers $a$, $b$, and
    $c$ that satisfies the equation
    $a^n + b^n = c^n$ for some
    integer value of $n > 2$.

    Without loss of generality,
    let $a$ be the smallest of the
    three integers. Then, we ...

<div class="preview">

![Preview](/assets/cab222a5bd10633b8312040d645e7baf.png)

</div>

</div>


### Parameters


### leading: length | _named_

The spacing between lines.

Leading defines the spacing between the [bottom
edge](/reference/text/text/#parameters-bottom-edge) of one line and the
[top edge](/reference/text/text/#parameters-top-edge) of the following
line. By default, these two properties are up to the font, but they can
also be configured manually with a text set rule.

By setting top edge, bottom edge, and leading, you can also configure a
consistent baseline-to-baseline distance. You could, for instance, set
the leading to <span class="typ-num">`1em`</span>, the top-edge to
<span class="typ-num">`0.8em`</span>, and the bottom-edge to
<span class="typ-op">`-`</span><span class="typ-num">`0.2em`</span> to
get a baseline gap of exactly <span class="typ-num">`2em`</span>. The
exact distribution of the top- and bottom-edge values affects the bounds
of the first and last line.


### spacing: length | _named_

The spacing between paragraphs.

Just like leading, this defines the spacing between the bottom edge of a
paragraph's last line and the top edge of the next paragraph's first
line.

When a paragraph is adjacent to a
[`block`](/reference/layout/block/ "`block`") that is not a paragraph,
that block's [`above`](/reference/layout/block/#parameters-above) or
[`below`](/reference/layout/block/#parameters-below) property takes
precedence over the paragraph spacing. Headings, for instance, reduce
the spacing below them by default for a better look.


### justify: bool | _named_

Whether to justify text in its line.

Hyphenation will be enabled for justified paragraphs if the [text
function's `hyphenate`
property](/reference/text/text/#parameters-hyphenate) is set to
<span class="typ-key">`auto`</span> and the current language is known.

Note that the current
[alignment](/reference/layout/align/#parameters-alignment) still has an
effect on the placement of the last line except if it ends with a
[justified line break](/reference/text/linebreak/#parameters-justify).


### linebreaks: auto, str | _named_

How to determine line breaks.

When this property is set to <span class="typ-key">`auto`</span>, its
default value, optimized line breaks will be used for justified
paragraphs. Enabling optimized line breaks for ragged paragraphs may
also be worthwhile to improve the appearance of the text.


#### Example

<div class="previewed-code">

    #set page(width: 207pt)
    #set par(linebreaks: "simple")
    Some texts feature many longer
    words. Those are often exceedingly
    challenging to break in a visually
    pleasing way.

    #set par(linebreaks: "optimized")
    Some texts feature many longer
    words. Those are often exceedingly
    challenging to break in a visually
    pleasing way.

<div class="preview">

![Preview](/assets/afe7dac249a627a4a78b08bcfbe89be6.png)

</div>

</div>


### first-line-indent: length, dictionary | _named_

The indent the first line of a paragraph should have.

By default, only the first line of a consecutive paragraph will be
indented (not the first one in the document or container, and not
paragraphs immediately following other block-level elements).

If you want to indent all paragraphs instead, you can pass a dictionary
containing the `amount` of indent as a length and the pair
`all: `<span class="typ-key">`true`</span>. When `all` is omitted from
the dictionary, it defaults to <span class="typ-key">`false`</span>.

By typographic convention, paragraph breaks are indicated either by some
space between paragraphs or by indented first lines. Consider

- reducing the [paragraph
  `spacing`](/reference/model/par/#parameters-spacing) to the
  [`leading`](/reference/model/par/#parameters-leading) using
  <span class="typ-key">`set`</span>` `<span class="typ-func">`par`</span><span class="typ-punct">`(`</span>`spacing`<span class="typ-punct">`:`</span>` `<span class="typ-num">`0.65em`</span><span class="typ-punct">`)`</span>
- increasing the [block
  `spacing`](/reference/layout/block/#parameters-spacing) (which
  inherits the paragraph spacing by default) to the original paragraph
  spacing using
  <span class="typ-key">`set`</span>` `<span class="typ-func">`block`</span><span class="typ-punct">`(`</span>`spacing`<span class="typ-punct">`:`</span>` `<span class="typ-num">`1.2em`</span><span class="typ-punct">`)`</span>


#### Example

<div class="previewed-code">

    #set block(spacing: 1.2em)
    #set par(
      first-line-indent: 1.5em,
      spacing: 0.65em,
    )

    The first paragraph is not affected
    by the indent.

    But the second paragraph is.

    #line(length: 100%)

    #set par(first-line-indent: (
      amount: 1.5em,
      all: true,
    ))

    Now all paragraphs are affected
    by the first line indent.

    Even the first one.

<div class="preview">

![Preview](/assets/8d7d84d566dc85bdc1bc0863bc851879.png)

</div>

</div>


### hanging-indent: length | _named_

The indent that all but the first line of a paragraph should have.


#### Example

<div class="previewed-code">

    #set par(hanging-indent: 1em)

    #lorem(15)

<div class="preview">

![Preview](/assets/7bde69f34692105af6720864a7d17480.png)

</div>

</div>


### body: content | _required_ _positional_

The contents of the paragraph.


## Definitions


### line

```
par.line(
    numbering: none str function
    number-align: auto alignment
    number-margin: alignment
    number-clearance: auto length
    numbering-scope: str
) -> content
```
A paragraph line.

This element is exclusively used for line number configuration through
set rules and cannot be placed.

The [`numbering`](/reference/model/par/#definitions-line-numbering)
option is used to enable line numbers by specifying a numbering format.


##### Parameters


##### numbering: none, str, function | _named_

How to number each line. Accepts a [numbering pattern or
function](/reference/model/numbering/).


###### Example

<div class="previewed-code">

    #set par.line(numbering: "I")

    Roses are red. \
    Violets are blue. \
    Typst is there for you.

<div class="preview">

![Preview](/assets/3bea09a9873e3b0128c5aa69c4ae0064.png)

</div>

</div>


##### number-align: auto, alignment | _named_

The alignment of line numbers associated with each line.

The default of <span class="typ-key">`auto`</span> indicates a smart
default where numbers grow horizontally away from the text, considering
the margin they're in and the current text direction.


###### Example

<div class="previewed-code">

    #set par.line(
      numbering: "I",
      number-align: left,
    )

    Hello world! \
    Today is a beautiful day \
    For exploring the world.

<div class="preview">

![Preview](/assets/5dfc01320623b767c6791805aff923e0.png)

</div>

</div>


##### number-margin: alignment | _named_

The margin at which line numbers appear.

*Note:* In a multi-column document, the line numbers for paragraphs
inside the last column will always appear on the `end` margin (right
margin for left-to-right text and left margin for right-to-left),
regardless of this configuration. That behavior cannot be changed at
this moment.


###### Example

<div class="previewed-code">

    #set par.line(
      numbering: "1",
      number-margin: right,
    )

    = Report
    - Brightness: Dark, yet darker
    - Readings: Negative

<div class="preview">

![Preview](/assets/bdfd1906b97281550007248cb244da29.png)

</div>

</div>


##### number-clearance: auto, length | _named_

The distance between line numbers and text.

The default value of <span class="typ-key">`auto`</span> results in a
clearance that is adaptive to the page width and yields reasonable
results in most cases.


###### Example

<div class="previewed-code">

    #set par.line(
      numbering: "1",
      number-clearance: 4pt,
    )

    Typesetting \
    Styling \
    Layout

<div class="preview">

![Preview](/assets/3208940772e8c44d0944e5a81c93ec96.png)

</div>

</div>


##### numbering-scope: str | _named_

Controls when to reset line numbering.

*Note:* The line numbering scope must be uniform across each page run (a
page run is a sequence of pages without an explicit pagebreak in
between). For this reason, set rules for it should be defined before any
page content, typically at the very start of the document.


###### Example

<div class="previewed-code">

    #set par.line(
      numbering: "1",
      numbering-scope: "page",
    )

    First line \
    Second line
    #pagebreak()
    First line again \
    Second line again

<div class="preview">

![Preview](/assets/3269883aef94076b02e0694e837a23f4.png)

</div>

</div>


#### Example

<div class="previewed-code">

    #set par.line(numbering: "1")

    Roses are red. \
    Violets are blue. \
    Typst is there for you.

<div class="preview">

![Preview](/assets/6f6e7b60b1d411a81b15694f783e2013.png)

</div>

</div>

The `numbering` option takes either a predefined [numbering
pattern](/reference/model/numbering/) or a function returning styled
content. You can disable line numbers for text inside certain elements
by setting the numbering to <span class="typ-key">`none`</span> using
show-set rules.

<div class="previewed-code">

    // Styled red line numbers.
    #set par.line(
      numbering: n => text(red)[#n]
    )

    // Disable numbers inside figures.
    #show figure: set par.line(
      numbering: none
    )

    Roses are red. \
    Violets are blue.

    #figure(
      caption: [Without line numbers.]
    )[
      Lorem ipsum \
      dolor sit amet
    ]

    The text above is a sample \
    originating from distant times.

<div class="preview">

![Preview](/assets/58937016f47739bbce0d3f8c6d6a9f94.png)

</div>

</div>

This element exposes further options which may be used to control other
aspects of line numbering, such as its
[alignment](/reference/model/par/#definitions-line-number-align) or
[margin](/reference/model/par/#definitions-line-number-margin). In
addition, you can control whether the numbering is reset on each page
through the
[`numbering-scope`](/reference/model/par/#definitions-line-numbering-scope)
option.

