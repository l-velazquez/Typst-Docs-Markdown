
# linebreak

```
linebreak(
    justify: bool
) -> content
```
Inserts a line break.

Advances the paragraph to the next line. A single trailing line break at
the end of a paragraph is ignored, but more than one creates additional
empty lines.

## Example

<div class="previewed-code">

    *Date:* 26.12.2022 \
    *Topic:* Infrastructure Test \
    *Severity:* High \

<div class="preview">

![Preview](/assets/384cb289bb242b86c8b1387b41ca7b38.png)

</div>

</div>

## Syntax

This function also has dedicated syntax: To insert a line break, simply
write a backslash followed by whitespace. This always creates an
unjustified break.


### Parameters


### justify: bool | _named_

Whether to justify the line before the break.

This is useful if you found a better line break opportunity in your
justified text than Typst did.


#### Example

<div class="previewed-code">

    #set par(justify: true)
    #let jb = linebreak(justify: true)

    I have manually tuned the #jb
    line breaks in this paragraph #jb
    for an _interesting_ result. #jb

<div class="preview">

![Preview](/assets/4652670040cf88f551099ee9a0e1d33b.png)

</div>

</div>

