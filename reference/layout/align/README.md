
# align

```
align(
    alignment
    content
) -> content
```
Aligns content horizontally and vertically.

## Example

Let's start with centering our content horizontally:

<div class="previewed-code">

    #set page(height: 120pt)
    #set align(center)

    Centered text, a sight to see \
    In perfect balance, visually \
    Not left nor right, it stands alone \
    A work of art, a visual throne

<div class="preview">

![Preview](/assets/91c3481be6d803c4fd0540e78c25091a.png)

</div>

</div>

To center something vertically, use *horizon* alignment:

<div class="previewed-code">

    #set page(height: 120pt)
    #set align(horizon)

    Vertically centered, \
    the stage had entered, \
    a new paragraph.

<div class="preview">

![Preview](/assets/cbd38ef8c4834081d6b063dcffaa4d9c.png)

</div>

</div>

## Combining alignments

You can combine two alignments with the `+` operator. Let's also only
apply this to one piece of content by using the function form instead of
a set rule:

<div class="previewed-code">

    #set page(height: 120pt)
    Though left in the beginning ...

    #align(right + bottom)[
      ... they were right in the end, \
      and with addition had gotten, \
      the paragraph to the bottom!
    ]

<div class="preview">

![Preview](/assets/8176aa00c602f0b89c8ff5022b425216.png)

</div>

</div>

## Nested alignment

You can use varying alignments for layout containers and the elements
within them. This way, you can create intricate layouts:

<div class="previewed-code">

    #align(center, block[
      #set align(left)
      Though centered together \
      alone \
      we \
      are \
      left.
    ])

<div class="preview">

![Preview](/assets/7a63e59616d8948c21cd27d07c47cbd.png)

</div>

</div>

## Alignment within the same line

The `align` function performs block-level alignment and thus always
interrupts the current paragraph. To have different alignment for parts
of the same line, you should use [fractional
spacing](/reference/layout/h/) instead:

<div class="previewed-code">

    Start #h(1fr) End

<div class="preview">

![Preview](/assets/8e569fc1b13666e212c093d0351cc0de.png)

</div>

</div>


### Parameters


### alignment: alignment | _positional_

The [alignment](/reference/layout/alignment/ "alignment") along both
axes.


#### Example

<div class="previewed-code">

    #set page(height: 6cm)
    #set text(lang: "ar")

    مثال
    #align(
      end + horizon,
      rect(inset: 12pt)[ركن]
    )

<div class="preview">

![Preview](/assets/df5efabe6e8813f04d7d9ad5a5cf7fc4.png)

</div>

</div>


### body: content | _required_ _positional_

The content to align.

