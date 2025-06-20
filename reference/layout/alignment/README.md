
# Alignment

Where to align something along an axis.

Possible values are:

- `start`: Aligns at the
  [start](/reference/layout/direction/#definitions-start) of the [text
  direction](/reference/text/text/#parameters-dir).
- `end`: Aligns at the
  [end](/reference/layout/direction/#definitions-end) of the [text
  direction](/reference/text/text/#parameters-dir).
- `left`: Align at the left.
- `center`: Aligns in the middle, horizontally.
- `right`: Aligns at the right.
- `top`: Aligns at the top.
- `horizon`: Aligns in the middle, vertically.
- `bottom`: Align at the bottom.

These values are available globally and also in the alignment type's
scope, so you can write either of the following two:

<div class="previewed-code">

    #align(center)[Hi]
    #align(alignment.center)[Hi]

<div class="preview">

![Preview](/assets/669ac68cb04f4942797f66b87e297c20.png)

</div>

</div>

## 2D alignments

To align along both axes at the same time, add the two alignments using
the `+` operator. For example, `top + right` aligns the content to the
top right corner.

<div class="previewed-code">

    #set page(height: 3cm)
    #align(center + bottom)[Hi]

<div class="preview">

![Preview](/assets/5f766b5749e7d5181e3d6b4854c0785e.png)

</div>

</div>

## Fields

The `x` and `y` fields hold the alignment's horizontal and vertical
components, respectively (as yet another `alignment`). They may be
<span class="typ-key">`none`</span>.

<div class="previewed-code">

    #(top + right).x \
    #left.x \
    #left.y (none)

<div class="preview">

![Preview](/assets/79cafc257ee34674474ab3a53a1c3047.png)

</div>

</div>


## Definitions


### axis

```
alignment.axis(
) -> none str
```
The axis this alignment belongs to.

- <span class="typ-str">`"horizontal"`</span> for `start`, `left`,
  `center`, `right`, and `end`
- <span class="typ-str">`"vertical"`</span> for `top`, `horizon`, and
  `bottom`
- <span class="typ-key">`none`</span> for 2-dimensional alignments


##### Parameters


#### Example

<div class="previewed-code">

    #left.axis() \
    #bottom.axis()

<div class="preview">

![Preview](/assets/387aae8b6112fd14679b1c8e65d15622.png)

</div>

</div>


### inv

```
alignment.inv(
) -> alignment
```
The inverse alignment.


##### Parameters


#### Example

<div class="previewed-code">

    #top.inv() \
    #left.inv() \
    #center.inv() \
    #(left + bottom).inv()

<div class="preview">

![Preview](/assets/b41031486714772a203469f697c3e6fd.png)

</div>

</div>

