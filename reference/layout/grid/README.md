
# grid

```
grid(
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
Arranges content in a grid.

The grid element allows you to arrange content in a grid. You can define
the number of rows and columns, as well as the size of the gutters
between them. There are multiple sizing modes for columns and rows that
can be used to create complex layouts.

While the grid and table elements work very similarly, they are intended
for different use cases and carry different semantics. The grid element
is intended for presentational and layout purposes, while the
[`table`](/reference/model/table/) element is intended for, in broad
terms, presenting multiple related data points. In the future, Typst
will annotate its output such that screenreaders will announce content
in `table` as tabular while a grid's content will be announced no
different than multiple content blocks in the document flow. Set and
show rules on one of these elements do not affect the other.

A grid's sizing is determined by the track sizes specified in the
arguments. Because each of the sizing parameters accepts the same
values, we will explain them just once, here. Each sizing argument
accepts an array of individual track sizes. A track size is either:

- <span class="typ-key">`auto`</span>: The track will be sized to fit
  its contents. It will be at most as large as the remaining space. If
  there is more than one <span class="typ-key">`auto`</span> track
  width, and together they claim more than the available space, the
  <span class="typ-key">`auto`</span> tracks will fairly distribute the
  available space among themselves.

- A fixed or relative length (e.g. <span class="typ-num">`10pt`</span>
  or
  <span class="typ-num">`20%`</span>` `<span class="typ-op">`-`</span>` `<span class="typ-num">`1cm`</span>):
  The track will be exactly of this size.

- A fractional length (e.g. <span class="typ-num">`1fr`</span>): Once
  all other tracks have been sized, the remaining space will be divided
  among the fractional tracks according to their fractions. For example,
  if there are two fractional tracks, each with a fraction of
  <span class="typ-num">`1fr`</span>, they will each take up half of the
  remaining space.

To specify a single track, the array can be omitted in favor of a single
value. To specify multiple <span class="typ-key">`auto`</span> tracks,
enter the number of tracks instead of an array. For example, `columns:`
<span class="typ-num">`3`</span> is equivalent to `columns:`
<span class="typ-punct">`(`</span><span class="typ-key">`auto`</span><span class="typ-punct">`,`</span>` `<span class="typ-key">`auto`</span><span class="typ-punct">`,`</span>` `<span class="typ-key">`auto`</span><span class="typ-punct">`)`</span>.

## Examples

The example below demonstrates the different track sizing options. It
also shows how you can use
[`grid.cell`](/reference/layout/grid/#definitions-cell) to make an
individual cell span two grid tracks.

<div class="previewed-code">

    // We use `rect` to emphasize the
    // area of cells.
    #set rect(
      inset: 8pt,
      fill: rgb("e4e5ea"),
      width: 100%,
    )

    #grid(
      columns: (60pt, 1fr, 2fr),
      rows: (auto, 60pt),
      gutter: 3pt,
      rect[Fixed width, auto height],
      rect[1/3 of the remains],
      rect[2/3 of the remains],
      rect(height: 100%)[Fixed height],
      grid.cell(
        colspan: 2,
        image("tiger.jpg", width: 100%),
      ),
    )

<div class="preview">

![Preview](/assets/9d4e8714750ff00270cb0fc4f0bc09ae.png)

</div>

</div>

You can also [spread](/reference/foundations/arguments/#spreading) an
array of strings or content into a grid to populate its cells.

<div class="previewed-code">

    #grid(
      columns: 5,
      gutter: 5pt,
      ..range(25).map(str)
    )

<div class="preview">

![Preview](/assets/aad11723d596b2524d0d3d305af58082.png)

</div>

</div>

## Styling the grid

The grid's appearance can be customized through different parameters.
These are the most important ones:

- [`fill`](/reference/layout/grid/#parameters-fill) to give all cells a
  background
- [`align`](/reference/layout/grid/#parameters-align) to change how
  cells are aligned
- [`inset`](/reference/layout/grid/#parameters-inset) to optionally add
  internal padding to each cell
- [`stroke`](/reference/layout/grid/#parameters-stroke) to optionally
  enable grid lines with a certain stroke

If you need to override one of the above options for a single cell, you
can use the [`grid.cell`](/reference/layout/grid/#definitions-cell)
element. Likewise, you can override individual grid lines with the
[`grid.hline`](/reference/layout/grid/#definitions-hline) and
[`grid.vline`](/reference/layout/grid/#definitions-vline) elements.

Alternatively, if you need the appearance options to depend on a cell's
position (column and row), you may specify a function to `fill` or
`align` of the form `(column, row) => value`. You may also use a show
rule on [`grid.cell`](/reference/layout/grid/#definitions-cell) - see
that element's examples or the examples below for more information.

Locating most of your styling in set and show rules is recommended, as
it keeps the grid's or table's actual usages clean and easy to read. It
also allows you to easily change the grid's appearance in one place.

### Stroke styling precedence

There are three ways to set the stroke of a grid cell: through
[`grid`<span class="typ-punct">`.`</span>`cell`'s `stroke`
field](/reference/layout/grid/#definitions-cell-stroke), by using
[`grid`<span class="typ-punct">`.`</span>`hline`](/reference/layout/grid/#definitions-hline)
and
[`grid`<span class="typ-punct">`.`</span>`vline`](/reference/layout/grid/#definitions-vline),
or by setting the [`grid`'s `stroke`
field](/reference/layout/grid/#parameters-stroke). When multiple of
these settings are present and conflict, the `hline` and `vline`
settings take the highest precedence, followed by the `cell` settings,
and finally the `grid` settings.

Furthermore, strokes of a repeated grid header or footer will take
precedence over regular cell strokes.


### Parameters


### columns: auto, int, relative, fraction, array | _named_

The column sizes.

Either specify a track size array or provide an integer to create a grid
with that many <span class="typ-key">`auto`</span>-sized columns. Note
that opposed to rows and gutters, providing a single track size will
only ever create a single column.


### rows: auto, int, relative, fraction, array | _named_

The row sizes.

If there are more cells than fit the defined rows, the last row is
repeated until there are no more cells.


### gutter: auto, int, relative, fraction, array | _named_

The gaps between rows and columns.

If there are more gutters than defined sizes, the last gutter is
repeated.

This is a shorthand to set `column-gutter` and `row-gutter` to the same
value.


### column-gutter: auto, int, relative, fraction, array | _named_

The gaps between columns.


### row-gutter: auto, int, relative, fraction, array | _named_

The gaps between rows.


### fill: none, color, gradient, array, tiling, function | _named_

How to fill the cells.

This can be a color or a function that returns a color. The function
receives the cells' column and row indices, starting from zero. This can
be used to implement striped grids.


#### Example

<div class="previewed-code">

    #grid(
      fill: (x, y) =>
        if calc.even(x + y) { luma(230) }
        else { white },
      align: center + horizon,
      columns: 4,
      inset: 2pt,
      [X], [O], [X], [O],
      [O], [X], [O], [X],
      [X], [O], [X], [O],
      [O], [X], [O], [X],
    )

<div class="preview">

![Preview](/assets/616a52b479521e50994e6526049b3d5d.png)

</div>

</div>


### align: auto, array, alignment, function | _named_

How to align the cells' content.

This can either be a single alignment, an array of alignments
(corresponding to each column) or a function that returns an alignment.
The function receives the cells' column and row indices, starting from
zero. If set to <span class="typ-key">`auto`</span>, the outer alignment
is used.

You can find an example for this argument at the
[`table.align`](/reference/model/table/#parameters-align) parameter.


### stroke: none, length, color, gradient, array, stroke, tiling, dictionary, function | _named_

How to [stroke](/reference/visualize/stroke/) the cells.

Grids have no strokes by default, which can be changed by setting this
option to the desired stroke.

If it is necessary to place lines which can cross spacing between cells
produced by the `gutter` option, or to override the stroke between
multiple specific cells, consider specifying one or more of
[`grid.hline`](/reference/layout/grid/#definitions-hline) and
[`grid.vline`](/reference/layout/grid/#definitions-vline) alongside your
grid cells.


#### Example

<div class="previewed-code">

    #set page(height: 13em, width: 26em)

    #let cv(..jobs) = grid(
      columns: 2,
      inset: 5pt,
      stroke: (x, y) => if x == 0 and y > 0 {
        (right: (
          paint: luma(180),
          thickness: 1.5pt,
          dash: "dotted"
        ))
      },
      grid.header(grid.cell(colspan: 2)[
        *Professional Experience*
        #box(width: 1fr, line(length: 100%, stroke: luma(180)))
      ]),
      ..{
        let last = none
        for job in jobs.pos() {
          (
            if job.year != last [*#job.year*],
            [
              *#job.company* - #job.role _(#job.timeframe)_ \
              #job.details
            ]
          )
          last = job.year
        }
      }
    )

    #cv(
      (
        year: 2012,
        company: [Pear Seed & Co.],
        role: [Lead Engineer],
        timeframe: [Jul - Dec],
        details: [
          - Raised engineers from 3x to 10x
          - Did a great job
        ],
      ),
      (
        year: 2012,
        company: [Mega Corp.],
        role: [VP of Sales],
        timeframe: [Mar - Jun],
        details: [- Closed tons of customers],
      ),
      (
        year: 2013,
        company: [Tiny Co.],
        role: [CEO],
        timeframe: [Jan - Dec],
        details: [- Delivered 4x more shareholder value],
      ),
      (
        year: 2014,
        company: [Glorbocorp Ltd],
        role: [CTO],
        timeframe: [Jan - Mar],
        details: [- Drove containerization forward],
      ),
    )

<div class="preview">

![Preview](/assets/d2b36ee1992a9899d60d6b5bb36c9993.png)

</div>

</div>


### inset: relative, array, dictionary, function | _named_

How much to pad the cells' content.

You can find an example for this argument at the
[`table.inset`](/reference/model/table/#parameters-inset) parameter.


### children: content | _required_ _positional_

The contents of the grid cells, plus any extra grid lines specified with
the [`grid.hline`](/reference/layout/grid/#definitions-hline) and
[`grid.vline`](/reference/layout/grid/#definitions-vline) elements.

The cells are populated in row-major order.


## Definitions


### cell

```
grid.cell(
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
A cell in the grid. You can use this function in the argument list of a
grid to override grid style properties for an individual cell or
manually positioning it within the grid. You can also use this function
in show rules to apply certain styles to multiple cells at once.

For example, you can override the position and stroke for a single cell:


##### Parameters


##### body: content | _required_ _positional_

The cell's body.


##### x: auto, int | _named_

The cell's column (zero-indexed). This field may be used in show rules
to style a cell depending on its column.

You may override this field to pick in which column the cell must be
placed. If no row (`y`) is chosen, the cell will be placed in the first
row (starting at row 0) with that column available (or a new row if
none). If both `x` and `y` are chosen, however, the cell will be placed
in that exact position. An error is raised if that position is not
available (thus, it is usually wise to specify cells with a custom
position before cells with automatic positions).


###### Example

<div class="previewed-code">

    #let circ(c) = circle(
        fill: c, width: 5mm
    )

    #grid(
      columns: 4,
      rows: 7mm,
      stroke: .5pt + blue,
      align: center + horizon,
      inset: 1mm,

      grid.cell(x: 2, y: 2, circ(aqua)),
      circ(yellow),
      grid.cell(x: 3, circ(green)),
      circ(black),
    )

<div class="preview">

![Preview](/assets/d4295624ceed58586c2323592650f5a3.png)

</div>

</div>


##### y: auto, int | _named_

The cell's row (zero-indexed). This field may be used in show rules to
style a cell depending on its row.

You may override this field to pick in which row the cell must be
placed. If no column (`x`) is chosen, the cell will be placed in the
first column (starting at column 0) available in the chosen row. If all
columns in the chosen row are already occupied, an error is raised.


###### Example

<div class="previewed-code">

    #let tri(c) = polygon.regular(
      fill: c,
      size: 5mm,
      vertices: 3,
    )

    #grid(
      columns: 2,
      stroke: blue,
      inset: 1mm,

      tri(black),
      grid.cell(y: 1, tri(teal)),
      grid.cell(y: 1, tri(red)),
      grid.cell(y: 2, tri(orange))
    )

<div class="preview">

![Preview](/assets/2aa1128c7723558f82b243152265c648.png)

</div>

</div>


##### colspan: int | _named_

The amount of columns spanned by this cell.


##### rowspan: int | _named_

The amount of rows spanned by this cell.


##### fill: none, auto, color, gradient, tiling | _named_

The cell's [fill](/reference/layout/grid/#parameters-fill) override.


##### align: auto, alignment | _named_

The cell's [alignment](/reference/layout/grid/#parameters-align)
override.


##### inset: auto, relative, dictionary | _named_

The cell's [inset](/reference/layout/grid/#parameters-inset) override.


##### stroke: none, length, color, gradient, stroke, tiling, dictionary | _named_

The cell's [stroke](/reference/layout/grid/#parameters-stroke) override.


##### breakable: auto, bool | _named_

Whether rows spanned by this cell can be placed in different pages. When
equal to <span class="typ-key">`auto`</span>, a cell spanning only
fixed-size rows is unbreakable, while a cell spanning at least one
<span class="typ-key">`auto`</span>-sized row is breakable.


#### Example

<div class="previewed-code">

    #set text(15pt, font: "Noto Sans Symbols 2")
    #show regex("[♚-♟︎]"): set text(fill: rgb("21212A"))
    #show regex("[♔-♙]"): set text(fill: rgb("111015"))

    #grid(
      fill: (x, y) => rgb(
        if calc.odd(x + y) { "7F8396" }
        else { "EFF0F3" }
      ),
      columns: (1em,) * 8,
      rows: 1em,
      align: center + horizon,

      [♖], [♘], [♗], [♕], [♔], [♗], [♘], [♖],
      [♙], [♙], [♙], [♙], [],  [♙], [♙], [♙],
      grid.cell(
        x: 4, y: 3,
        stroke: blue.transparentize(60%)
      )[♙],

      ..(grid.cell(y: 6)[♟],) * 8,
      ..([♜], [♞], [♝], [♛], [♚], [♝], [♞], [♜])
        .map(grid.cell.with(y: 7)),
    )

<div class="preview">

![Preview](/assets/85a80ca20c73818a35cfef42a986e689.png)

</div>

</div>

You may also apply a show rule on `grid.cell` to style all cells at
once, which allows you, for example, to apply styles based on a cell's
position. Refer to the examples of the
[`table.cell`](/reference/model/table/#definitions-cell) element to
learn more about this.


### hline

```
grid.hline(
    y: auto int
    start: int
    end: none int
    stroke: none length color gradient stroke tiling dictionary
    position: alignment
) -> content
```
A horizontal line in the grid.

Overrides any per-cell stroke, including stroke specified through the
grid's `stroke` field. Can cross spacing between cells created through
the grid's `column-gutter` option.

An example for this function can be found at the
[`table.hline`](/reference/model/table/#definitions-hline) element.


##### Parameters


##### y: auto, int | _named_

The row above which the horizontal line is placed (zero-indexed). If the
`position` field is set to `bottom`, the line is placed below the row
with the given index instead (see that field's docs for details).

Specifying <span class="typ-key">`auto`</span> causes the line to be
placed at the row below the last automatically positioned cell (that is,
cell without coordinate overrides) before the line among the grid's
children. If there is no such cell before the line, it is placed at the
top of the grid (row 0). Note that specifying for this option exactly
the total amount of rows in the grid causes this horizontal line to
override the bottom border of the grid, while a value of 0 overrides the
top border.


##### start: int | _named_

The column at which the horizontal line starts (zero-indexed,
inclusive).


##### end: none, int | _named_

The column before which the horizontal line ends (zero-indexed,
exclusive). Therefore, the horizontal line will be drawn up to and
across column `end - 1`.

A value equal to <span class="typ-key">`none`</span> or to the amount of
columns causes it to extend all the way towards the end of the grid.


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


### vline

```
grid.vline(
    x: auto int
    start: int
    end: none int
    stroke: none length color gradient stroke tiling dictionary
    position: alignment
) -> content
```
A vertical line in the grid.

Overrides any per-cell stroke, including stroke specified through the
grid's `stroke` field. Can cross spacing between cells created through
the grid's `row-gutter` option.


##### Parameters


##### x: auto, int | _named_

The column before which the horizontal line is placed (zero-indexed). If
the `position` field is set to `end`, the line is placed after the
column with the given index instead (see that field's docs for details).

Specifying <span class="typ-key">`auto`</span> causes the line to be
placed at the column after the last automatically positioned cell (that
is, cell without coordinate overrides) before the line among the grid's
children. If there is no such cell before the line, it is placed before
the grid's first column (column 0). Note that specifying for this option
exactly the total amount of columns in the grid causes this vertical
line to override the end border of the grid (right in LTR, left in RTL),
while a value of 0 overrides the start border (left in LTR, right in
RTL).


##### start: int | _named_

The row at which the vertical line starts (zero-indexed, inclusive).


##### end: none, int | _named_

The row on top of which the vertical line ends (zero-indexed,
exclusive). Therefore, the vertical line will be drawn up to and across
row `end - 1`.

A value equal to <span class="typ-key">`none`</span> or to the amount of
rows causes it to extend all the way towards the bottom of the grid.


##### stroke: none, length, color, gradient, stroke, tiling, dictionary | _named_

The line's stroke.

Specifying <span class="typ-key">`none`</span> removes any lines
previously placed across this line's range, including vlines or per-cell
stroke below it.


##### position: alignment | _named_

The position at which the line is placed, given its column (`x`) -
either `start` to draw before it or `end` to draw after it.

The values `left` and `right` are also accepted, but discouraged as they
cause your grid to be inconsistent between left-to-right and
right-to-left documents.

This setting is only relevant when column gutter is enabled (and
shouldn't be used otherwise - prefer just increasing the `x` field by
one instead), since then the position after a column becomes different
from the position before the next column due to the spacing between
both.


### header

```
grid.header(
    repeat: bool
    level: int
    content
) -> content
```
A repeatable grid header.

If `repeat` is set to `true`, the header will be repeated across pages.
For an example, refer to the
[`table.header`](/reference/model/table/#definitions-header) element and
the [`grid.stroke`](/reference/layout/grid/#parameters-stroke)
parameter.


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


### footer

```
grid.footer(
    repeat: bool
    content
) -> content
```
A repeatable grid footer.

Just like the
[`grid.header`](/reference/layout/grid/#definitions-header) element, the
footer can repeat itself on every page of the table.

No other grid cells may be placed after the footer.


##### Parameters


##### repeat: bool | _named_

Whether this footer should be repeated across pages.


##### children: content | _required_ _positional_

The cells and lines within the footer.

