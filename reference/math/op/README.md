
# op

```
math.op(
    content
    limits: bool
) -> content
```
A text operator in an equation.

## Example

<div class="previewed-code">

    $ tan x = (sin x)/(cos x) $
    $ op("custom",
         limits: #true)_(n->oo) n $

<div class="preview">

![Preview](/assets/9fdc9e7c49667f04e2f767a37cbce167.png)

</div>

</div>

## Predefined Operators

Typst predefines the operators `arccos`, `arcsin`, `arctan`, `arg`,
`cos`, `cosh`, `cot`, `coth`, `csc`, `csch`, `ctg`, `deg`, `det`, `dim`,
`exp`, `gcd`, `lcm`, `hom`, `id`, `im`, `inf`, `ker`, `lg`, `lim`,
`liminf`, `limsup`, `ln`, `log`, `max`, `min`, `mod`, `Pr`, `sec`,
`sech`, `sin`, `sinc`, `sinh`, `sup`, `tan`, `tanh`, `tg` and `tr`.


### Parameters


### text: content | _required_ _positional_

The operator's text.


### limits: bool | _named_

Whether the operator should show attachments as limits in display mode.

