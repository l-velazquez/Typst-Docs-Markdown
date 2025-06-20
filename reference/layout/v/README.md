
# v

```
v(
    relative fraction
    weak: bool
) -> content
```
Inserts vertical spacing into a flow of blocks.

The spacing can be absolute, relative, or fractional. In the last case,
the remaining space on the page is distributed among all fractional
spacings according to their relative fractions.

## Example

<div class="previewed-code">

    #grid(
      rows: 3cm,
      columns: 6,
      gutter: 1fr,
      [A #parbreak() B],
      [A #v(0pt) B],
      [A #v(10pt) B],
      [A #v(0pt, weak: true) B],
      [A #v(40%, weak: true) B],
      [A #v(1fr) B],
    )

<div class="preview">

![Preview](/assets/cd0b69bfd17f6ce712e61cc001c42be.png)

</div>

</div>


### Parameters


### amount: relative, fraction | _required_ _positional_

How much spacing to insert.


### weak: bool | _named_

If <span class="typ-key">`true`</span>, the spacing collapses at the
start or end of a flow. Moreover, from multiple adjacent weak spacings
all but the largest one collapse. Weak spacings will always collapse
adjacent paragraph spacing, even if the paragraph spacing is larger.


#### Example

<div class="previewed-code">

    The following theorem is
    foundational to the field:
    #v(4pt, weak: true)
    $ x^2 + y^2 = r^2 $
    #v(4pt, weak: true)
    The proof is simple:

<div class="preview">

![Preview](/assets/ed76ba665ffecd67d6680ea0a2c33fd1.png)

</div>

</div>

