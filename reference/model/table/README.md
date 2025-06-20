
# table

```
table(
    columns: auto int relative fraction array
    rows: auto int relative fraction array
    gutter: auto int relative fraction array
    column-gutter: auto int relative fraction array
    row-gutter: auto int relative fraction array
    fill: none color gradient array tiling function
    align: auto array alignment function
    stroke: none length color gradient array stroke tiling dictionary function
    inset: relative array dictionary function
    content
) -> content
```
A table of items.

Tables are used to arrange content in cells. Cells can contain arbitrary
content, including multiple paragraphs and are specified in row-major
order. For a hands-on explanation of all the ways you can use and
customize tables in Typst, check out the [table
guide](/guides/table-guide/).

Because tables are just grids with different defaults for some cell
properties (notably `stroke` and `inset`), refer to the [grid
documentation](/reference/layout/grid/) for more information on how to
size the table tracks and specify the cell appearance properties.

If you are unsure whether you should be using a table or a grid,
consider whether the content you are arranging semantically belongs
together as a set of related data points or similar or whether you are
just want to enhance your presentation by arranging unrelated content in
a grid. In the former case, a table is the right choice, while in the
latter case, a grid is more appropriate. Furthermore, Typst will
annotate its output in the future such that screenreaders will announce
content in `table` as tabular while a grid's content will be announced
no different than multiple content blocks in the document flow.

Note that, to override a particular cell's properties or apply show
rules on table cells, you can use the
[`table.cell`](/reference/model/table/#definitions-cell) element. See
its documentation for more information.

Although the `table` and the `grid` share most properties, set and show
rules on one of them do not affect the other.

To give a table a caption and make it
[referenceable](/reference/model/ref/), put it into a
[figure](/reference/model/figure/ "figure").

## Example

The example below demonstrates some of the most common table options.

<div class="previewed-code">

    #table(
      columns: (1fr, auto, auto),
      inset: 10pt,
      align: horizon,
      table.header(
        [], [*Volume*], [*Parameters*],
      ),
      image("cylinder.svg"),
      $ pi h (D^2 - d^2) / 4 $,
      [
        $h$: height \
        $D$: outer radius \
        $d$: inner radius
      ],
      image("tetrahedron.svg"),
      $ sqrt(2) / 12 a^3 $,
      [$a$: edge length]
    )

<div class="preview">

![Preview](/assets/292ce306c3aab6e773c2f2ba66fa7dbb.png)

</div>

</div>

Much like with grids, you can use
[`table.cell`](/reference/model/table/#definitions-cell) to customize
the appearance and the position of each cell.

<div class="previewed-code">

    #set table(
      stroke: none,
      gutter: 0.2em,
      fill: (x, y) =>
        if x == 0 or y == 0 { gray },
      inset: (right: 1.5em),
    )

    #show table.cell: it => {
      if it.x == 0 or it.y == 0 {
        set text(white)
        strong(it)
      } else if it.body == [] {
        // Replace empty cells with 'N/A'
        pad(..it.inset)[_N/A_]
      } else {
        it
      }
    }

    #let a = table.cell(
      fill: green.lighten(60%),
    )[A]
    #let b = table.cell(
      fill: aqua.lighten(60%),
    )[B]

    #table(
      columns: 4,
      [], [Exam 1], [Exam 2], [Exam 3],

      [John], [], a, [],
      [Mary], [], a, a,
      [Robert], b, a, b,
    )

<div class="preview">

![Preview](/assets/ffc1843d36a9bc64fabab2c809c2265.png)

</div>

</div>


### Parameters


### columns: auto, int, relative, fraction, array | _named_

The column sizes. See the [grid documentation](/reference/layout/grid/)
for more information on track sizing.


### rows: auto, int, relative, fraction, array | _named_

The row sizes. See the [grid documentation](/reference/layout/grid/) for
more information on track sizing.


### gutter: auto, int, relative, fraction, array | _named_

The gaps between rows and columns. This is a shorthand for setting
`column-gutter` and `row-gutter` to the same value. See the [grid
documentation](/reference/layout/grid/) for more information on gutters.


### column-gutter: auto, int, relative, fraction, array | _named_

The gaps between columns. Takes precedence over `gutter`. See the [grid
documentation](/reference/layout/grid/) for more information on gutters.


### row-gutter: auto, int, relative, fraction, array | _named_

The gaps between rows. Takes precedence over `gutter`. See the [grid
documentation](/reference/layout/grid/) for more information on gutters.


### fill: none, color, gradient, array, tiling, function | _named_

How to fill the cells.

This can be a color or a function that returns a color. The function
receives the cells' column and row indices, starting from zero. This can
be used to implement striped tables.


#### Example

<div class="previewed-code">

    #table(
      fill: (x, _) =>
        if calc.odd(x) { luma(240) }
        else { white },
      align: (x, y) =>
        if y == 0 { center }
        else if x == 0 { left }
        else { right },
      columns: 4,
      [], [*Q1*], [*Q2*], [*Q3*],
      [Revenue:], [1000 €], [2000 €], [3000 €],
      [Expenses:], [500 €], [1000 €], [1500 €],
      [Profit:], [500 €], [1000 €], [1500 €],
    )

<div class="preview">

![Preview](/assets/1ce6e13c91ef624898a870a344ad491f.png)

</div>

</div>


### align: auto, array, alignment, function | _named_

How to align the cells' content.

This can either be a single alignment, an array of alignments
(corresponding to each column) or a function that returns an alignment.
The function receives the cells' column and row indices, starting from
zero. If set to <span class="typ-key">`auto`</span>, the outer alignment
is used.


#### Example

<div class="previewed-code">

    #table(
      columns: 3,
      align: (left, center, right),
      [Hello], [Hello], [Hello],
      [A], [B], [C],
    )

<div class="preview">

![Preview](/assets/fdf060a2d0a5f8bb558ef194e322452d.png)

</div>

</div>


### stroke: none, length, color, gradient, array, stroke, tiling, dictionary, function | _named_

How to [stroke](/reference/visualize/stroke/ "stroke") the cells.

Strokes can be disabled by setting this to
<span class="typ-key">`none`</span>.

If it is necessary to place lines which can cross spacing between cells
produced by the `gutter` option, or to override the stroke between
multiple specific cells, consider specifying one or more of
[`table.hline`](/reference/model/table/#definitions-hline) and
[`table.vline`](/reference/model/table/#definitions-vline) alongside
your table cells.

See the [grid documentation](/reference/layout/grid/#parameters-stroke)
for more information on strokes.


### inset: relative, array, dictionary, function | _named_

How much to pad the cells' content.


#### Example

<div class="previewed-code">

    #table(
      inset: 10pt,
      [Hello],
      [World],
    )

    #table(
      columns: 2,
      inset: (
        x: 20pt,
        y: 10pt,
      ),
      [Hello],
      [World],
    )

<div class="preview">

![Preview](/assets/7f5904d443534c1d3689928a3e857f5f.png)

</div>

</div>


### children: content | _required_ _positional_

The contents of the table cells, plus any extra table lines specified
with the [`table.hline`](/reference/model/table/#definitions-hline) and
[`table.vline`](/reference/model/table/#definitions-vline) elements.


## Definitions


### cell

```
table.cell(
    content
    x: auto int
    y: auto int
    colspan: int
    rowspan: int
    fill: none auto color gradient tiling
    align: auto alignment
    inset: auto relative dictionary
    stroke: none length color gradient stroke tiling dictionary
    breakable: auto bool
) -> content
```
A cell in the table. Use this to position a cell manually or to apply
styling. To do the latter, you can either use the function to override
the properties for a particular cell, or use it in show rules to apply
certain styles to multiple cells at once.

Perhaps the most important use case of
`table`<span class="typ-punct">`.`</span>`cell` is to make a cell span
multiple columns and/or rows with the `colspan` and `rowspan` fields.


##### Parameters


##### body: content | _required_ _positional_

The cell's body.


##### x: auto, int | _named_

The cell's column (zero-indexed). Functions identically to the `x` field
in [`grid.cell`](/reference/layout/grid/#definitions-cell).


##### y: auto, int | _named_

The cell's row (zero-indexed). Functions identically to the `y` field in
[`grid.cell`](/reference/layout/grid/#definitions-cell).


##### colspan: int | _named_

The amount of columns spanned by this cell.


##### rowspan: int | _named_

The amount of rows spanned by this cell.


##### fill: none, auto, color, gradient, tiling | _named_

The cell's [fill](/reference/model/table/#parameters-fill) override.


##### align: auto, alignment | _named_

The cell's [alignment](/reference/model/table/#parameters-align)
override.


##### inset: auto, relative, dictionary | _named_

The cell's [inset](/reference/model/table/#parameters-inset) override.


##### stroke: none, length, color, gradient, stroke, tiling, dictionary | _named_

The cell's [stroke](/reference/model/table/#parameters-stroke) override.


##### breakable: auto, bool | _named_

Whether rows spanned by this cell can be placed in different pages. When
equal to <span class="typ-key">`auto`</span>, a cell spanning only
fixed-size rows is unbreakable, while a cell spanning at least one
<span class="typ-key">`auto`</span>-sized row is breakable.


#### Example

<div class="previewed-code">

    #show table.cell.where(y: 0): strong
    #set table(
      stroke: (x, y) => if y == 0 {
        (bottom: 0.7pt + black)
      },
      align: (x, y) => (
        if x > 0 { center }
        else { left }
      )
    )

    #table(
      columns: 3,
      table.header(
        [Substance],
        [Subcritical °C],
        [Supercritical °C],
      ),
      [Hydrochloric Acid],
      [12.0], [92.1],
      [Sodium Myreth Sulfate],
      [16.6], [104],
      [Potassium Hydroxide],
      table.cell(colspan: 2)[24.7],
    )

<div class="preview">

![Preview](/assets/dab40f9bc81b4706c5aa22132650faa0.png)

</div>

</div>

For example, you can override the fill, alignment or inset for a single
cell:

<div class="previewed-code">

    // You can also import those.
    #import table: cell, header

    #table(
      columns: 2,
      align: center,
      header(
        [*Trip progress*],
        [*Itinerary*],
      ),
      cell(
        align: right,
        fill: fuchsia.lighten(80%),
        [🚗],
      ),
      [Get in, folks!],
      [🚗], [Eat curbside hotdog],
      cell(align: left)[🌴🚗],
      cell(
        inset: 0.06em,
        text(1.62em)[🛖🌅🌊],
      ),
    )

<div class="preview">

![Preview](/assets/56d6b266584cad45b33a6040c84a2b0d.png)

</div>

</div>

You may also apply a show rule on `table.cell` to style all cells at
once. Combined with selectors, this allows you to apply styles based on
a cell's position:

<div class="previewed-code">

    #show table.cell.where(x: 0): strong

    #table(
      columns: 3,
      gutter: 3pt,
      [Name], [Age], [Strength],
      [Hannes], [36], [Grace],
      [Irma], [50], [Resourcefulness],
      [Vikram], [49], [Perseverance],
    )

<div class="preview">

![Preview](/assets/73648fd3af6abcc0737856eb8d5b3ca7.png)

</div>

</div>


### hline

```
table.hline(
    y: auto int
    start: int
    end: none int
    stroke: none length color gradient stroke tiling dictionary
    position: alignment
) -> content
```
A horizontal line in the table.

Overrides any per-cell stroke, including stroke specified through the
table's `stroke` field. Can cross spacing between cells created through
the table's
[`column-gutter`](/reference/model/table/#parameters-column-gutter)
option.

Use this function instead of the table's `stroke` field if you want to
manually place a horizontal line at a specific position in a single
table. Consider using [table's
`stroke`](/reference/model/table/#parameters-stroke) field or
[`table.cell`'s
`stroke`](/reference/model/table/#definitions-cell-stroke) field instead
if the line you want to place is part of all your tables' designs.


##### Parameters


##### y: auto, int | _named_

The row above which the horizontal line is placed (zero-indexed).
Functions identically to the `y` field in
[`grid.hline`](/reference/layout/grid/#definitions-hline-y).


##### start: int | _named_

The column at which the horizontal line starts (zero-indexed,
inclusive).


##### end: none, int | _named_

The column before which the horizontal line ends (zero-indexed,
exclusive).


##### stroke: none, length, color, gradient, stroke, tiling, dictionary | _named_

The line's stroke.

Specifying <span class="typ-key">`none`</span> removes any lines
previously placed across this line's range, including hlines or per-cell
stroke below it.


##### position: alignment | _named_

The position at which the line is placed, given its row (`y`) - either
`top` to draw above it or `bottom` to draw below it.

This setting is only relevant when row gutter is enabled (and shouldn't
be used otherwise - prefer just increasing the `y` field by one
instead), since then the position below a row becomes different from the
position above the next row due to the spacing between both.


#### Example

<div class="previewed-code">

    #set table.hline(stroke: .6pt)

    #table(
      stroke: none,
      columns: (auto, 1fr),
      [09:00], [Badge pick up],
      [09:45], [Opening Keynote],
      [10:30], [Talk: Typst's Future],
      [11:15], [Session: Good PRs],
      table.hline(start: 1),
      [Noon], [_Lunch break_],
      table.hline(start: 1),
      [14:00], [Talk: Tracked Layout],
      [15:00], [Talk: Automations],
      [16:00], [Workshop: Tables],
      table.hline(),
      [19:00], [Day 1 Attendee Mixer],
    )

<div class="preview">

![Preview](/assets/165f96ef6c21f2194a6fbd988e52743e.png)

</div>

</div>


### vline

```
table.vline(
    x: auto int
    start: int
    end: none int
    stroke: none length color gradient stroke tiling dictionary
    position: alignment
) -> content
```
A vertical line in the table. See the docs for
[`grid.vline`](/reference/layout/grid/#definitions-vline) for more
information regarding how to use this element's fields.

Overrides any per-cell stroke, including stroke specified through the
table's `stroke` field. Can cross spacing between cells created through
the table's
[`row-gutter`](/reference/model/table/#parameters-row-gutter) option.

Similar to [`table.hline`](/reference/model/table/#definitions-hline),
use this function if you want to manually place a vertical line at a
specific position in a single table and use the [table's
`stroke`](/reference/model/table/#parameters-stroke) field or
[`table.cell`'s
`stroke`](/reference/model/table/#definitions-cell-stroke) field instead
if the line you want to place is part of all your tables' designs.


##### Parameters


##### x: auto, int | _named_

The column before which the horizontal line is placed (zero-indexed).
Functions identically to the `x` field in
[`grid.vline`](/reference/layout/grid/#definitions-vline).


##### start: int | _named_

The row at which the vertical line starts (zero-indexed, inclusive).


##### end: none, int | _named_

The row on top of which the vertical line ends (zero-indexed,
exclusive).


##### stroke: none, length, color, gradient, stroke, tiling, dictionary | _named_

The line's stroke.

Specifying <span class="typ-key">`none`</span> removes any lines
previously placed across this line's range, including vlines or per-cell
stroke below it.


##### position: alignment | _named_

The position at which the line is placed, given its column (`x`) -
either `start` to draw before it or `end` to draw after it.

The values `left` and `right` are also accepted, but discouraged as they
cause your table to be inconsistent between left-to-right and
right-to-left documents.

This setting is only relevant when column gutter is enabled (and
shouldn't be used otherwise - prefer just increasing the `x` field by
one instead), since then the position after a column becomes different
from the position before the next column due to the spacing between
both.


### header

```
table.header(
    repeat: bool
    level: int
    content
) -> content
```
A repeatable table header.

You should wrap your tables' heading rows in this function even if you
do not plan to wrap your table across pages because Typst will use this
function to attach accessibility metadata to tables in the future and
ensure universal access to your document.

You can use the `repeat` parameter to control whether your table's
header will be repeated across pages.


##### Parameters


##### repeat: bool | _named_

Whether this header should be repeated across pages.


##### level: int | _named_

The level of the header. Must not be zero.

This allows repeating multiple headers at once. Headers with different
levels can repeat together, as long as they have ascending levels.

Notably, when a header with a lower level starts repeating, all higher
or equal level headers stop repeating (they are "replaced" by the new
header).


##### children: content | _required_ _positional_

The cells and lines within the header.


#### Example

<div class="previewed-code">

    #set page(height: 11.5em)
    #set table(
      fill: (x, y) =>
        if x == 0 or y == 0 {
          gray.lighten(40%)
        },
      align: right,
    )

    #show table.cell.where(x: 0): strong
    #show table.cell.where(y: 0): strong

    #table(
      columns: 4,
      table.header(
        [], [Blue chip],
        [Fresh IPO], [Penny st'k],
      ),
      table.cell(
        rowspan: 6,
        align: horizon,
        rotate(-90deg, reflow: true)[
          *USD / day*
        ],
      ),
      [0.20], [104], [5],
      [3.17], [108], [4],
      [1.59], [84],  [1],
      [0.26], [98],  [15],
      [0.01], [195], [4],
      [7.34], [57],  [2],
    )

<div class="preview">

![Preview](/assets/207a73a7e6fb990edcb409654b11167d.png)

</div>

</div>


### footer

```
table.footer(
    repeat: bool
    content
) -> content
```
A repeatable table footer.

Just like the
[`table.header`](/reference/model/table/#definitions-header) element,
the footer can repeat itself on every page of the table. This is useful
for improving legibility by adding the column labels in both the header
and footer of a large table, totals, or other information that should be
visible on every page.

No other table cells may be placed after the footer.


##### Parameters


##### repeat: bool | _named_

Whether this footer should be repeated across pages.


##### children: content | _required_ _positional_

The cells and lines within the footer.

