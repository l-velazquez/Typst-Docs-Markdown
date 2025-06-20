
# equation

```
math.equation(
    block: bool
    numbering: none str function
    number-align: alignment
    supplement: none auto content function
    content
) -> content
```
A mathematical equation.

Can be displayed inline with text or as a separate block. An equation
becomes block-level through the presence of at least one space after the
opening dollar sign and one space before the closing dollar sign.

## Example

<div class="previewed-code">

    #set text(font: "New Computer Modern")

    Let $a$, $b$, and $c$ be the side
    lengths of right-angled triangle.
    Then, we know that:
    $ a^2 + b^2 = c^2 $

    Prove by induction:
    $ sum_(k=1)^n k = (n(n+1)) / 2 $

<div class="preview">

![Preview](/assets/26dc4e81002bbeca5f9a64ad97cfb7fe.png)

</div>

</div>

By default, block-level equations will not break across pages. This can
be changed through
<span class="typ-key">`show`</span>` math`<span class="typ-punct">`.`</span><span class="typ-func">`equation`</span><span class="typ-punct">`:`</span>` `<span class="typ-key">`set`</span>` `<span class="typ-func">`block`</span><span class="typ-punct">`(`</span>`breakable`<span class="typ-punct">`:`</span>` `<span class="typ-key">`true`</span><span class="typ-punct">`)`</span>.

## Syntax

This function also has dedicated syntax: Write mathematical markup
within dollar signs to create an equation. Starting and ending the
equation with at least one space lifts it into a separate block that is
centered horizontally. For more details about math syntax, see the [main
math page](/reference/math/).


### Parameters


### block: bool | _named_

Whether the equation is displayed as a separate block.


### numbering: none, str, function | _named_

How to [number](/reference/model/numbering/) block-level equations.


#### Example

<div class="previewed-code">

    #set math.equation(numbering: "(1)")

    We define:
    $ phi.alt := (1 + sqrt(5)) / 2 $ <ratio>

    With @ratio, we get:
    $ F_n = floor(1 / sqrt(5) phi.alt^n) $

<div class="preview">

![Preview](/assets/202911378a85036c27dd557f74625c28.png)

</div>

</div>


### number-align: alignment | _named_

The alignment of the equation numbering.

By default, the alignment is
`end `<span class="typ-op">`+`</span>` horizon`. For the horizontal
component, you can use `right`, `left`, or `start` and `end` of the text
direction; for the vertical component, you can use `top`, `horizon`, or
`bottom`.


#### Example

<div class="previewed-code">

    #set math.equation(numbering: "(1)", number-align: bottom)

    We can calculate:
    $ E &= sqrt(m_0^2 + p^2) \
        &approx 125 "GeV" $

<div class="preview">

![Preview](/assets/12340ab301fe38101ce51c2197eed635.png)

</div>

</div>


### supplement: none, auto, content, function | _named_

A supplement for the equation.

For references to equations, this is added before the referenced number.

If a function is specified, it is passed the referenced equation and
should return content.


#### Example

<div class="previewed-code">

    #set math.equation(numbering: "(1)", supplement: [Eq.])

    We define:
    $ phi.alt := (1 + sqrt(5)) / 2 $ <ratio>

    With @ratio, we get:
    $ F_n = floor(1 / sqrt(5) phi.alt^n) $

<div class="preview">

![Preview](/assets/2ecbd21a7ecd72183675d76fdf30c1b4.png)

</div>

</div>


### body: content | _required_ _positional_

The contents of the equation.

