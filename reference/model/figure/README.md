
# figure

```
figure(
    content
    placement: none auto alignment
    scope: str
    caption: none content
    kind: auto str function
    supplement: none auto content function
    numbering: none str function
    gap: length
    outlined: bool
) -> content
```
A figure with an optional caption.

Automatically detects its kind to select the correct counting track. For
example, figures containing images will be numbered separately from
figures containing tables.

## Examples

The example below shows a basic figure with an image:

<div class="previewed-code">

    @glacier shows a glacier. Glaciers
    are complex systems.

    #figure(
      image("glacier.jpg", width: 80%),
      caption: [A curious figure.],
    ) <glacier>

<div class="preview">

![Preview](/assets/b9dc3c275cd6f020dfa180755d3cdd2e.png)

</div>

</div>

You can also insert [tables](/reference/model/table/) into figures to
give them a caption. The figure will detect this and automatically use a
separate counter.

<div class="previewed-code">

    #figure(
      table(
        columns: 4,
        [t], [1], [2], [3],
        [y], [0.3s], [0.4s], [0.8s],
      ),
      caption: [Timing results],
    )

<div class="preview">

![Preview](/assets/fd168e26293d3b952840ef04aba38cf6.png)

</div>

</div>

This behaviour can be overridden by explicitly specifying the figure's
`kind`. All figures of the same kind share a common counter.

## Figure behaviour

By default, figures are placed within the flow of content. To make them
float to the top or bottom of the page, you can use the
[`placement`](/reference/model/figure/#parameters-placement) argument.

If your figure is too large and its contents are breakable across pages
(e.g. if it contains a large table), then you can make the figure itself
breakable across pages as well with this show rule:

    #show figure: set block(breakable: true)

See the [block](/reference/layout/block/#parameters-breakable)
documentation for more information about breakable and non-breakable
blocks.

## Caption customization

You can modify the appearance of the figure's caption with its
associated [`caption`](/reference/model/figure/#definitions-caption)
function. In the example below, we emphasize all captions:

<div class="previewed-code">

    #show figure.caption: emph

    #figure(
      rect[Hello],
      caption: [I am emphasized!],
    )

<div class="preview">

![Preview](/assets/fd76214814edd5d9a3611f40e27fda0a.png)

</div>

</div>

By using a [`where`](/reference/foundations/function/#definitions-where)
selector, we can scope such rules to specific kinds of figures. For
example, to position the caption above tables, but keep it below for all
other kinds of figures, we could write the following show-set rule:

<div class="previewed-code">

    #show figure.where(
      kind: table
    ): set figure.caption(position: top)

    #figure(
      table(columns: 2)[A][B][C][D],
      caption: [I'm up here],
    )

<div class="preview">

![Preview](/assets/e455d8faf40a203e10d4562c478231f4.png)

</div>

</div>


### Parameters


### body: content | _required_ _positional_

The content of the figure. Often, an
[image](/reference/visualize/image/ "image").


### placement: none, auto, alignment | _named_

The figure's placement on the page.

- <span class="typ-key">`none`</span>: The figure stays in-flow exactly
  where it was specified like other content.
- <span class="typ-key">`auto`</span>: The figure picks `top` or
  `bottom` depending on which is closer.
- `top`: The figure floats to the top of the page.
- `bottom`: The figure floats to the bottom of the page.

The gap between the main flow content and the floating figure is
controlled by the
[`clearance`](/reference/layout/place/#parameters-clearance) argument on
the `place` function.


#### Example

<div class="previewed-code">

    #set page(height: 200pt)
    #show figure: set place(
      clearance: 1em,
    )

    = Introduction
    #figure(
      placement: bottom,
      caption: [A glacier],
      image("glacier.jpg", width: 60%),
    )
    #lorem(60)

<div class="preview">

![Preview](/assets/836b68045cf729130a332f4422de1824.png)

</div>

</div>


### scope: str | _named_

Relative to which containing scope the figure is placed.

Set this to <span class="typ-str">`"parent"`</span> to create a
full-width figure in a two-column document.

Has no effect if `placement` is <span class="typ-key">`none`</span>.


#### Example

<div class="previewed-code">

    #set page(height: 250pt, columns: 2)

    = Introduction
    #figure(
      placement: bottom,
      scope: "parent",
      caption: [A glacier],
      image("glacier.jpg", width: 60%),
    )
    #lorem(60)

<div class="preview">

![Preview](/assets/ff35f92bd3477ddda661809e2666a0ef.png)

</div>

</div>


### caption: none, content | _named_

The figure's caption.


### kind: auto, str, function | _named_

The kind of figure this is.

All figures of the same kind share a common counter.

If set to <span class="typ-key">`auto`</span>, the figure will try to
automatically determine its kind based on the type of its body.
Automatically detected kinds are [tables](/reference/model/table/) and
[code](/reference/text/raw/). In other cases, the inferred kind is that
of an [image](/reference/visualize/image/ "image").

Setting this to something other than <span class="typ-key">`auto`</span>
will override the automatic detection. This can be useful if

- you wish to create a custom figure type that is not an
  [image](/reference/visualize/image/ "image"), a
  [table](/reference/model/table/ "table") or
  [code](/reference/text/raw/),
- you want to force the figure to use a specific counter regardless of
  its content.

You can set the kind to be an element function or a string. If you set
it to an element function other than [`table`](/reference/model/table/),
[`raw`](/reference/text/raw/) or [`image`](/reference/visualize/image/),
you will need to manually specify the figure's supplement.


#### Example

<div class="previewed-code">

    #figure(
      circle(radius: 10pt),
      caption: [A curious atom.],
      kind: "atom",
      supplement: [Atom],
    )

<div class="preview">

![Preview](/assets/82712152d3e540b0bd0e61dfb58e2fcd.png)

</div>

</div>


### supplement: none, auto, content, function | _named_

The figure's supplement.

If set to <span class="typ-key">`auto`</span>, the figure will try to
automatically determine the correct supplement based on the `kind` and
the active [text language](/reference/text/text/#parameters-lang). If
you are using a custom figure type, you will need to manually specify
the supplement.

If a function is specified, it is passed the first descendant of the
specified `kind` (typically, the figure's body) and should return
content.


#### Example

<div class="previewed-code">

    #figure(
      [The contents of my figure!],
      caption: [My custom figure],
      supplement: [Bar],
      kind: "foo",
    )

<div class="preview">

![Preview](/assets/fe8c37b3e778c5204de955fe9d51d5cd.png)

</div>

</div>


### numbering: none, str, function | _named_

How to number the figure. Accepts a [numbering pattern or
function](/reference/model/numbering/).


### gap: length | _named_

The vertical gap between the body and caption.


### outlined: bool | _named_

Whether the figure should appear in an
[`outline`](/reference/model/outline/ "`outline`") of figures.


## Definitions


### caption

```
figure.caption(
    position: alignment
    separator: auto content
    content
) -> content
```
The caption of a figure. This element can be used in set and show rules
to customize the appearance of captions for all figures or figures of a
specific kind.

In addition to its `position` and `body`, the `caption` also provides
the figure's `kind`, `supplement`, `counter`, and `numbering` as fields.
These parts can be used in
[`where`](/reference/foundations/function/#definitions-where) selectors
and show rules to build a completely custom caption.


##### Parameters


##### position: alignment | _named_

The caption's position in the figure. Either `top` or `bottom`.


###### Example

<div class="previewed-code">

    #show figure.where(
      kind: table
    ): set figure.caption(position: top)

    #figure(
      table(columns: 2)[A][B],
      caption: [I'm up here],
    )

    #figure(
      rect[Hi],
      caption: [I'm down here],
    )

    #figure(
      table(columns: 2)[A][B],
      caption: figure.caption(
        position: bottom,
        [I'm down here too!]
      )
    )

<div class="preview">

![Preview](/assets/21d14a9a26af4aa31312a9fcc145ee52.png)

</div>

</div>


##### separator: auto, content | _named_

The separator which will appear between the number and body.

If set to <span class="typ-key">`auto`</span>, the separator will be
adapted to the current [language](/reference/text/text/#parameters-lang)
and [region](/reference/text/text/#parameters-region).


###### Example

<div class="previewed-code">

    #set figure.caption(separator: [ --- ])

    #figure(
      rect[Hello],
      caption: [A rectangle],
    )

<div class="preview">

![Preview](/assets/178ec0814a619978959f5da809bfc408.png)

</div>

</div>


##### body: content | _required_ _positional_

The caption's body.

Can be used alongside `kind`, `supplement`, `counter`, `numbering`, and
`location` to completely customize the caption.


###### Example

<div class="previewed-code">

    #show figure.caption: it => [
      #underline(it.body) |
      #it.supplement
      #context it.counter.display(it.numbering)
    ]

    #figure(
      rect[Hello],
      caption: [A rectangle],
    )

<div class="preview">

![Preview](/assets/271203fbe1409c884010228b31516257.png)

</div>

</div>


#### Example

<div class="previewed-code">

    #show figure.caption: emph

    #figure(
      rect[Hello],
      caption: [A rectangle],
    )

<div class="preview">

![Preview](/assets/ffd45a7b793ed7875c6f4d1b596e1c88.png)

</div>

</div>

