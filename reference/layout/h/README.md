
# h

```
h(
    relative fraction
    weak: bool
) -> content
```
Inserts horizontal spacing into a paragraph.

The spacing can be absolute, relative, or fractional. In the last case,
the remaining space on the line is distributed among all fractional
spacings according to their relative fractions.

## Example

<div class="previewed-code">

    First #h(1cm) Second \
    First #h(30%) Second

<div class="preview">

![Preview](/assets/f302fec582d1e98ecc2e5a6822e5ffbc.png)

</div>

</div>

## Fractional spacing

With fractional spacing, you can align things within a line without
forcing a paragraph break (like
[`align`](/reference/layout/align/ "`align`") would). Each fractionally
sized element gets space based on the ratio of its fraction to the sum
of all fractions.

<div class="previewed-code">

    First #h(1fr) Second \
    First #h(1fr) Second #h(1fr) Third \
    First #h(2fr) Second #h(1fr) Third

<div class="preview">

![Preview](/assets/a410aa858f4085ebab8e7cf2d9580f06.png)

</div>

</div>

## Mathematical Spacing

In [mathematical formulas](/reference/math/), you can additionally use
these constants to add spacing between elements: `thin` (1/6 em), `med`
(2/9 em), `thick` (5/18 em), `quad` (1 em), `wide` (2 em).


### Parameters


### amount: relative, fraction | _required_ _positional_

How much spacing to insert.


### weak: bool | _named_

If <span class="typ-key">`true`</span>, the spacing collapses at the
start or end of a paragraph. Moreover, from multiple adjacent weak
spacings all but the largest one collapse.

Weak spacing in markup also causes all adjacent markup spaces to be
removed, regardless of the amount of spacing inserted. To force a space
next to weak spacing, you can explicitly write
<span class="typ-str">`#`</span><span class="typ-str">`" "`</span> (for
a normal space) or <span class="typ-escape">`~`</span> (for a
non-breaking space). The latter can be useful to create a construct that
always attaches to the preceding word with one non-breaking space,
independently of whether a markup space existed in front or not.


#### Example

<div class="previewed-code">

    #h(1cm, weak: true)
    We identified a group of _weak_
    specimens that fail to manifest
    in most cases. However, when
    #h(8pt, weak: true) supported
    #h(8pt, weak: true) on both sides,
    they do show up.

    Further #h(0pt, weak: true) more,
    even the smallest of them swallow
    adjacent markup spaces.

<div class="preview">

![Preview](/assets/73fedbffd595e924c21761117468697d.png)

</div>

</div>

