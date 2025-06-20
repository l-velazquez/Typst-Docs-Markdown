
# outline

```
outline(
    title: none auto content
    target: label selector location function
    depth: none int
    indent: auto relative function
) -> content
```
A table of contents, figures, or other elements.

This function generates a list of all occurrences of an element in the
document, up to a given
[`depth`](/reference/model/outline/#parameters-depth). The element's
numbering and page number will be displayed in the outline alongside its
title or caption.

## Example

<div class="previewed-code">

    #set heading(numbering: "1.")
    #outline()

    = Introduction
    #lorem(5)

    = Methods
    == Setup
    #lorem(10)

<div class="preview">

![Preview](/assets/2f8dbcfcc2a5c0869ffd07d1406ee6b0.png)

</div>

</div>

## Alternative outlines

In its default configuration, this function generates a table of
contents. By setting the `target` parameter, the outline can be used to
generate a list of other kinds of elements than headings.

In the example below, we list all figures containing images by setting
`target` to
`figure`<span class="typ-punct">`.`</span><span class="typ-func">`where`</span><span class="typ-punct">`(`</span>`kind`<span class="typ-punct">`:`</span>` image`<span class="typ-punct">`)`</span>.
Just the same, we could have set it to
`figure`<span class="typ-punct">`.`</span><span class="typ-func">`where`</span><span class="typ-punct">`(`</span>`kind`<span class="typ-punct">`:`</span>` table`<span class="typ-punct">`)`</span>
to generate a list of tables.

We could also set it to just `figure`, without using a
[`where`](/reference/foundations/function/#definitions-where) selector,
but then the list would contain *all* figures, be it ones containing
images, tables, or other material.

<div class="previewed-code">

    #outline(
      title: [List of Figures],
      target: figure.where(kind: image),
    )

    #figure(
      image("tiger.jpg"),
      caption: [A nice figure!],
    )

<div class="preview">

![Preview](/assets/2b41608abfcce886ce9e5c454e9468c8.png)

</div>

</div>

## Styling the outline

At the most basic level, you can style the outline by setting properties
on it and its entries. This way, you can customize the outline's
[title](/reference/model/outline/#parameters-title), how outline entries
are [indented](/reference/model/outline/#parameters-indent), and how the
space between an entry's text and its page number should be
[filled](/reference/model/outline/#definitions-entry-fill).

Richer customization is possible through configuration of the outline's
[entries](/reference/model/outline/#definitions-entry). The outline
generates one entry for each outlined element.

### Spacing the entries

Outline entries are [blocks](/reference/layout/block/), so you can
adjust the spacing between them with normal block-spacing rules:

<div class="previewed-code">

    #show outline.entry.where(
      level: 1
    ): set block(above: 1.2em)

    #outline()

    = About ACME Corp.
    == History
    === Origins
    = Products
    == ACME Tools

<div class="preview">

![Preview](/assets/e05b998d9a6ae5807b6352756f823b6c.png)

</div>

</div>

### Building an outline entry from its parts

For full control, you can also write a transformational show rule on
`outline.entry`. However, the logic for properly formatting and
indenting outline entries is quite complex and the outline entry itself
only contains two fields: The level and the outlined element.

For this reason, various helper functions are provided. You can mix and
match these to compose an entry from just the parts you like.

The default show rule for an outline entry looks like
this<sup>[1](#1)</sup>:

    #show outline.entry: it => link(
      it.element.location(),
      it.indented(it.prefix(), it.inner()),
    )

- The [`indented`](/reference/model/outline/#definitions-entry) function
  takes an optional prefix and inner content and automatically applies
  the proper indentation to it, such that different entries align nicely
  and long headings wrap properly.

- The [`prefix`](/reference/model/outline/#definitions-entry) function
  formats the element's numbering (if any). It also appends a supplement
  for certain elements.

- The [`inner`](/reference/model/outline/#definitions-entry) function
  combines the element's
  [`body`](/reference/model/outline/#definitions-entry), the filler, and
  the [`page` number](/reference/model/outline/#definitions-entry).

You can use these individual functions to format the outline entry in
different ways. Let's say, you'd like to fully remove the filler and
page numbers. To achieve this, you could write a show rule like this:

<div class="previewed-code">

    #show outline.entry: it => link(
      it.element.location(),
      // Keep just the body, dropping
      // the fill and the page.
      it.indented(it.prefix(), it.body()),
    )

    #outline()

    = About ACME Corp.
    == History

<div class="preview">

![Preview](/assets/1f3ff9aa7aff1ec866e0bc1e9ba7f289.png)

</div>

</div>

<div id="1" class="footnote-definition">

<sup>1</sup>

The outline of equations is the exception to this rule as it does not
have a body and thus does not use indented layout.

</div>


### Parameters


### title: none, auto, content | _named_

The title of the outline.

- When set to <span class="typ-key">`auto`</span>, an appropriate title
  for the [text language](/reference/text/text/#parameters-lang) will be
  used.
- When set to <span class="typ-key">`none`</span>, the outline will not
  have a title.
- A custom title can be set by passing content.

The outline's heading will not be numbered by default, but you can force
it to be with a show-set rule:
<span class="typ-key">`show`</span>` `<span class="typ-func">`outline`</span><span class="typ-punct">`:`</span>` `<span class="typ-key">`set`</span>` `<span class="typ-func">`heading`</span><span class="typ-punct">`(`</span>`numbering`<span class="typ-punct">`:`</span>` `<span class="typ-str">`"1."`</span><span class="typ-punct">`)`</span>


### target: label, selector, location, function | _named_

The type of element to include in the outline.

To list figures containing a specific kind of element, like an image or
a table, you can specify the desired kind in a
[`where`](/reference/foundations/function/#definitions-where) selector.
See the section on [alternative
outlines](/reference/model/outline/#alternative-outlines) for more
details.


#### Example

<div class="previewed-code">

    #outline(
      title: [List of Tables],
      target: figure.where(kind: table),
    )

    #figure(
      table(
        columns: 4,
        [t], [1], [2], [3],
        [y], [0.3], [0.7], [0.5],
      ),
      caption: [Experiment results],
    )

<div class="preview">

![Preview](/assets/f680ff60eff769a37ce5c022c5e04fda.png)

</div>

</div>


### depth: none, int | _named_

The maximum level up to which elements are included in the outline. When
this argument is <span class="typ-key">`none`</span>, all elements are
included.


#### Example

<div class="previewed-code">

    #set heading(numbering: "1.")
    #outline(depth: 2)

    = Yes
    Top-level section.

    == Still
    Subsection.

    === Nope
    Not included.

<div class="preview">

![Preview](/assets/7d811f81352691b1f4b246dc30a79217.png)

</div>

</div>


### indent: auto, relative, function | _named_

How to indent the outline's entries.

- <span class="typ-key">`auto`</span>: Indents the numbering/prefix of a
  nested entry with the title of its parent entry. If the entries are
  not numbered (e.g., via [heading
  numbering](/reference/model/heading/#parameters-numbering)), this
  instead simply inserts a fixed amount of
  <span class="typ-num">`1.2em`</span> indent per level.

- [Relative length](/reference/layout/relative/): Indents the entry by
  the specified length per nesting level. Specifying
  <span class="typ-num">`2em`</span>, for instance, would indent
  top-level headings by <span class="typ-num">`0em`</span> (not nested),
  second level headings by <span class="typ-num">`2em`</span> (nested
  once), third-level headings by <span class="typ-num">`4em`</span>
  (nested twice) and so on.

- [Function](/reference/foundations/function/): You can further
  customize this setting with a function. That function receives the
  nesting level as a parameter (starting at 0 for top-level
  headings/elements) and should return a (relative) length. For example,
  `n `<span class="typ-op">`=>`</span>` n `<span class="typ-op">`*`</span>` `<span class="typ-num">`2em`</span>
  would be equivalent to just specifying
  <span class="typ-num">`2em`</span>.


#### Example

<div class="previewed-code">

    #set heading(numbering: "1.a.")

    #outline(
      title: [Contents (Automatic)],
      indent: auto,
    )

    #outline(
      title: [Contents (Length)],
      indent: 2em,
    )

    = About ACME Corp.
    == History
    === Origins
    #lorem(10)

    == Products
    #lorem(10)

<div class="preview">

![Preview](/assets/4aed7c19e84eac0ece90e6e94123554a.png)

</div>

</div>


## Definitions


### entry

```
outline.entry(
    int
    content
    fill: none content
) -> content
```
Represents an entry line in an outline.

With show-set and show rules on outline entries, you can richly
customize the outline's appearance. See the [section on styling the
outline](/reference/model/outline/#styling-the-outline) for details.


##### Parameters


##### level: int | _required_ _positional_

The nesting level of this outline entry. Starts at
<span class="typ-num">`1`</span> for top-level entries.


##### element: content | _required_ _positional_

The element this entry refers to. Its location will be available through
the [`location`](/reference/foundations/content/#definitions-location)
method on the content and can be [linked](/reference/model/link/) to.


##### fill: none, content | _named_

Content to fill the space between the title and the page number. Can be
set to <span class="typ-key">`none`</span> to disable filling.

The `fill` will be placed into a fractionally sized box that spans the
space between the entry's body and the page number. When using show
rules to override outline entries, it is thus recommended to wrap the
fill in a [`box`](/reference/layout/box/ "`box`") with fractional width,
i.e.
<span class="typ-func">`box`</span><span class="typ-punct">`(`</span>`width`<span class="typ-punct">`:`</span>` `<span class="typ-num">`1fr`</span><span class="typ-punct">`,`</span>` it`<span class="typ-punct">`.`</span>`fill`<span class="typ-punct">`)`</span>.

When using [`repeat`](/reference/layout/repeat/ "`repeat`"), the
[`gap`](/reference/layout/repeat/#parameters-gap) property can be useful
to tweak the visual weight of the fill.


###### Example

<div class="previewed-code">

    #set outline.entry(fill: line(length: 100%))
    #outline()

    = A New Beginning

<div class="preview">

![Preview](/assets/ef524710c756d05f113284640dc3f53b.png)

</div>

</div>


#### Definitions


##### indented

```
entry.indented(
    none content
    content
    gap: length
) -> content
```
A helper function for producing an indented entry layout: Lays out a
prefix and the rest of the entry in an indent-aware way.

If the parent outline's
[`indent`](/reference/model/outline/#parameters-indent) is
<span class="typ-key">`auto`</span>, the inner content of all entries at
level `N` is aligned with the prefix of all entries at level `N + 1`,
leaving at least `gap` space between the prefix and inner parts.
Furthermore, the `inner` contents of all entries at the same level are
aligned.

If the outline's indent is a fixed value or a function, the prefixes are
indented, but the inner contents are simply inset from the prefix by the
specified `gap`, rather than aligning outline-wide.


####### Parameters


####### prefix: none, content | _required_ _positional_

The `prefix` is aligned with the `inner` content of entries that have
level one less.

In the default show rule, this is just `it.prefix()`, but it can be
freely customized.


####### inner: content | _required_ _positional_

The formatted inner content of the entry.

In the default show rule, this is just `it.inner()`, but it can be
freely customized.


####### gap: length | _named_

The gap between the prefix and the inner content.


##### prefix

```
entry.prefix(
) -> none content
```
Formats the element's numbering (if any).

This also appends the element's supplement in case of figures or
equations. For instance, it would output `1.1` for a heading, but
`Figure 1` for a figure, as is usual for outlines.


####### Parameters


##### inner

```
entry.inner(
) -> content
```
Creates the default inner content of the entry.

This includes the body, the fill, and page number.


####### Parameters


##### body

```
entry.body(
) -> content
```
The content which is displayed in place of the referred element at its
entry in the outline. For a heading, this is its
[`body`](/reference/model/heading/#parameters-body); for a figure a
caption and for equations, it is empty.


####### Parameters


##### page

```
entry.page(
) -> content
```
The page number of this entry's element, formatted with the numbering
set for the referenced page.


####### Parameters

