
# heading

```
heading(
    level: auto int
    depth: int
    offset: int
    numbering: none str function
    supplement: none auto content function
    outlined: bool
    bookmarked: auto bool
    hanging-indent: auto length
    content
) -> content
```
A section heading.

With headings, you can structure your document into sections. Each
heading has a *level,* which starts at one and is unbounded upwards.
This level indicates the logical role of the following content (section,
subsection, etc.) A top-level heading indicates a top-level section of
the document (not the document's title).

Typst can automatically number your headings for you. To enable
numbering, specify how you want your headings to be numbered with a
[numbering pattern or function](/reference/model/numbering/).

Independently of the numbering, Typst can also automatically generate an
[outline](/reference/model/outline/ "outline") of all headings for you.
To exclude one or more headings from this outline, you can set the
`outlined` parameter to <span class="typ-key">`false`</span>.

## Example

<div class="previewed-code">

    #set heading(numbering: "1.a)")

    = Introduction
    In recent years, ...

    == Preliminaries
    To start, ...

<div class="preview">

![Preview](/assets/3da8ed6c330c3767836190a4021f5927.png)

</div>

</div>

## Syntax

Headings have dedicated syntax: They can be created by starting a line
with one or multiple equals signs, followed by a space. The number of
equals signs determines the heading's logical nesting depth. The
`offset` field can be set to configure the starting depth.


### Parameters


### level: auto, int | _named_

The absolute nesting depth of the heading, starting from one. If set to
<span class="typ-key">`auto`</span>, it is computed from
`offset `<span class="typ-op">`+`</span>` depth`.

This is primarily useful for usage in [show
rules](/reference/styling/#show-rules) (either with
[`where`](/reference/foundations/function/#definitions-where) selectors
or by accessing the level directly on a shown heading).


#### Example

<div class="previewed-code">

    #show heading.where(level: 2): set text(red)

    = Level 1
    == Level 2

    #set heading(offset: 1)
    = Also level 2
    == Level 3

<div class="preview">

![Preview](/assets/fe90e6f8fd396e0fe319b97dbaf1a394.png)

</div>

</div>


### depth: int | _named_

The relative nesting depth of the heading, starting from one. This is
combined with `offset` to compute the actual `level`.

This is set by the heading syntax, such that
<span class="typ-heading">`== Heading`</span> creates a heading with
logical depth of 2, but actual level
`offset `<span class="typ-op">`+`</span>` `<span class="typ-num">`2`</span>.
If you construct a heading manually, you should typically prefer this
over setting the absolute level.


### offset: int | _named_

The starting offset of each heading's `level`, used to turn its relative
`depth` into its absolute `level`.


#### Example

<div class="previewed-code">

    = Level 1

    #set heading(offset: 1, numbering: "1.1")
    = Level 2

    #heading(offset: 2, depth: 2)[
      I'm level 4
    ]

<div class="preview">

![Preview](/assets/84ab568a4e7e1f030c7a3a8ec0354a2c.png)

</div>

</div>


### numbering: none, str, function | _named_

How to number the heading. Accepts a [numbering pattern or
function](/reference/model/numbering/).


#### Example

<div class="previewed-code">

    #set heading(numbering: "1.a.")

    = A section
    == A subsection
    === A sub-subsection

<div class="preview">

![Preview](/assets/76d21794ff33145e127cdaac70f78b6c.png)

</div>

</div>


### supplement: none, auto, content, function | _named_

A supplement for the heading.

For references to headings, this is added before the referenced number.

If a function is specified, it is passed the referenced heading and
should return content.


#### Example

<div class="previewed-code">

    #set heading(numbering: "1.", supplement: [Chapter])

    = Introduction <intro>
    In @intro, we see how to turn
    Sections into Chapters. And
    in @intro[Part], it is done
    manually.

<div class="preview">

![Preview](/assets/3993144e7996642b7d2f45d44c369199.png)

</div>

</div>


### outlined: bool | _named_

Whether the heading should appear in the
[outline](/reference/model/outline/ "outline").

Note that this property, if set to <span class="typ-key">`true`</span>,
ensures the heading is also shown as a bookmark in the exported PDF's
outline (when exporting to PDF). To change that behavior, use the
`bookmarked` property.


#### Example

<div class="previewed-code">

    #outline()

    #heading[Normal]
    This is a normal heading.

    #heading(outlined: false)[Hidden]
    This heading does not appear
    in the outline.

<div class="preview">

![Preview](/assets/ab747af34dccbfd0fc8693f1e700f84e.png)

</div>

</div>


### bookmarked: auto, bool | _named_

Whether the heading should appear as a bookmark in the exported PDF's
outline. Doesn't affect other export formats, such as PNG.

The default value of <span class="typ-key">`auto`</span> indicates that
the heading will only appear in the exported PDF's outline if its
`outlined` property is set to <span class="typ-key">`true`</span>, that
is, if it would also be listed in Typst's
[outline](/reference/model/outline/ "outline"). Setting this property to
either <span class="typ-key">`true`</span> (bookmark) or
<span class="typ-key">`false`</span> (don't bookmark) bypasses that
behavior.


#### Example

<div class="previewed-code">

    #heading[Normal heading]
    This heading will be shown in
    the PDF's bookmark outline.

    #heading(bookmarked: false)[Not bookmarked]
    This heading won't be
    bookmarked in the resulting
    PDF.

<div class="preview">

![Preview](/assets/fd4bcc50364eb53747e22f371da7368b.png)

</div>

</div>


### hanging-indent: auto, length | _named_

The indent all but the first line of a heading should have.

The default value of <span class="typ-key">`auto`</span> indicates that
the subsequent heading lines will be indented based on the width of the
numbering.


#### Example

<div class="previewed-code">

    #set heading(numbering: "1.")
    #heading[A very, very, very, very, very, very long heading]

<div class="preview">

![Preview](/assets/df90e0df8906fbbae0d7e445a7c15a22.png)

</div>

</div>


### body: content | _required_ _positional_

The heading's title.

