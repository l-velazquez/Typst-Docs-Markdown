
# smallcaps

```
smallcaps(
    all: bool
    content
) -> content
```
Displays text in small capitals.

## Example

<div class="previewed-code">

    Hello \
    #smallcaps[Hello]

<div class="preview">

![Preview](/assets/d860d23f8025b71987581bf155766bc1.png)

</div>

</div>

## Smallcaps fonts

By default, this uses the `smcp` and `c2sc` OpenType features on the
font. Not all fonts support these features. Sometimes, smallcaps are
part of a dedicated font. This is, for example, the case for the *Latin
Modern* family of fonts. In those cases, you can use a show-set rule to
customize the appearance of the text in smallcaps:

    #show smallcaps: set text(font: "Latin Modern Roman Caps")

In the future, this function will support synthesizing smallcaps from
normal letters, but this is not yet implemented.

## Smallcaps headings

You can use a [show rule](/reference/styling/#show-rules) to apply
smallcaps formatting to all your headings. In the example below, we also
center-align our headings and disable the standard bold font.

<div class="previewed-code">

    #set par(justify: true)
    #set heading(numbering: "I.")

    #show heading: smallcaps
    #show heading: set align(center)
    #show heading: set text(
      weight: "regular"
    )

    = Introduction
    #lorem(40)

<div class="preview">

![Preview](/assets/7f47b81d5cd6ecd285a78baa93a2efaa.png)

</div>

</div>


### Parameters


### all: bool | _named_

Whether to turn uppercase letters into small capitals as well.

Unless overridden by a show rule, this enables the `c2sc` OpenType
feature.


#### Example

<div class="previewed-code">

    #smallcaps(all: true)[UNICEF] is an
    agency of #smallcaps(all: true)[UN].

<div class="preview">

![Preview](/assets/f26ae448d07a9e76c623cf95561882ad.png)

</div>

</div>


### body: content | _required_ _positional_

The content to display in small capitals.

