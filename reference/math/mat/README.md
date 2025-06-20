
# mat

```
math.mat(
    delim: none str array symbol
    align: alignment
    augment: none int dictionary
    gap: relative
    row-gap: relative
    column-gap: relative
    array
) -> content
```
A matrix.

The elements of a row should be separated by commas, while the rows
themselves should be separated by semicolons. The semicolon syntax
merges preceding arguments separated by commas into an array. You can
also use this special syntax of math function calls to define custom
functions that take 2D data.

Content in cells can be aligned with the
[`align`](/reference/math/mat/#parameters-align) parameter, or content
in cells that are in the same row can be aligned with the `&` symbol.

## Example

<div class="previewed-code">

    $ mat(
      1, 2, ..., 10;
      2, 2, ..., 10;
      dots.v, dots.v, dots.down, dots.v;
      10, 10, ..., 10;
    ) $

<div class="preview">

![Preview](/assets/ca24a2958190d70441a482b738ddf8f4.png)

</div>

</div>


### Parameters


### delim: none, str, array, symbol | _named_

The delimiter to use.

Can be a single character specifying the left delimiter, in which case
the right delimiter is inferred. Otherwise, can be an array containing a
left and a right delimiter.


#### Example

<div class="previewed-code">

    #set math.mat(delim: "[")
    $ mat(1, 2; 3, 4) $

<div class="preview">

![Preview](/assets/a90805f7e282235aafa3bde73f34aa1.png)

</div>

</div>


### align: alignment | _named_

The horizontal alignment that each cell should have.


#### Example

<div class="previewed-code">

    #set math.mat(align: right)
    $ mat(-1, 1, 1; 1, -1, 1; 1, 1, -1) $

<div class="preview">

![Preview](/assets/5f741736d817a8455441fbc945038f47.png)

</div>

</div>


### augment: none, int, dictionary | _named_

Draws augmentation lines in a matrix.

- <span class="typ-key">`none`</span>: No lines are drawn.
- A single number: A vertical augmentation line is drawn after the
  specified column number. Negative numbers start from the end.
- A dictionary: With a dictionary, multiple augmentation lines can be
  drawn both horizontally and vertically. Additionally, the style of the
  lines can be set. The dictionary can contain the following keys:
  - `hline`: The offsets at which horizontal lines should be drawn. For
    example, an offset of `2` would result in a horizontal line being
    drawn after the second row of the matrix. Accepts either an integer
    for a single line, or an array of integers for multiple lines. Like
    for a single number, negative numbers start from the end.
  - `vline`: The offsets at which vertical lines should be drawn. For
    example, an offset of `2` would result in a vertical line being
    drawn after the second column of the matrix. Accepts either an
    integer for a single line, or an array of integers for multiple
    lines. Like for a single number, negative numbers start from the
    end.
  - `stroke`: How to [stroke](/reference/visualize/stroke/) the line. If
    set to <span class="typ-key">`auto`</span>, takes on a thickness of
    0.05em and square line caps.


#### Example

<div class="previewed-code">

    $ mat(1, 0, 1; 0, 1, 2; augment: #2) $
    // Equivalent to:
    $ mat(1, 0, 1; 0, 1, 2; augment: #(-1)) $

<div class="preview">

![Preview](/assets/e228a9d19f69a430344b19c91c98a191.png)

</div>

</div>

<div class="previewed-code">

    $ mat(0, 0, 0; 1, 1, 1; augment: #(hline: 1, stroke: 2pt + green)) $

<div class="preview">

![Preview](/assets/dcf1c0269b2f89267e46ab5bdec05de0.png)

</div>

</div>


### gap: relative | _named_

The gap between rows and columns.

This is a shorthand to set `row-gap` and `column-gap` to the same value.


#### Example

<div class="previewed-code">

    #set math.mat(gap: 1em)
    $ mat(1, 2; 3, 4) $

<div class="preview">

![Preview](/assets/91aca9252744d4fd6539667e70c329c8.png)

</div>

</div>


### row-gap: relative | _named_

The gap between rows.


#### Example

<div class="previewed-code">

    #set math.mat(row-gap: 1em)
    $ mat(1, 2; 3, 4) $

<div class="preview">

![Preview](/assets/60d549f2e0a73efaecf1ed1891621016.png)

</div>

</div>


### column-gap: relative | _named_

The gap between columns.


#### Example

<div class="previewed-code">

    #set math.mat(column-gap: 1em)
    $ mat(1, 2; 3, 4) $

<div class="preview">

![Preview](/assets/b4a9ab4d1c58c1520bf31ecde2d9d1c9.png)

</div>

</div>


### rows: array | _required_ _positional_

An array of arrays with the rows of the matrix.


#### Example

<div class="previewed-code">

    #let data = ((1, 2, 3), (4, 5, 6))
    #let matrix = math.mat(..data)
    $ v := matrix $

<div class="preview">

![Preview](/assets/37eedc689e05b0f94e76556b52b364f6.png)

</div>

</div>

