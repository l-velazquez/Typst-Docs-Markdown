
# Symbol

A Unicode symbol.

Typst defines common symbols so that they can easily be written with
standard keyboards. The symbols are defined in modules, from which they
can be accessed using [field access
notation](/reference/scripting/#fields):

- General symbols are defined in the [`sym`
  module](/reference/symbols/sym/) and are accessible without the `sym.`
  prefix in math mode.
- Emoji are defined in the [`emoji` module](/reference/symbols/emoji/)

Moreover, you can define custom symbols with this type's constructor
function.

<div class="previewed-code">

    #sym.arrow.r \
    #sym.gt.eq.not \
    $gt.eq.not$ \
    #emoji.face.halo

<div class="preview">

![Preview](/assets/554ec909334ebd767463138a7c508786.png)

</div>

</div>

Many symbols have different variants, which can be selected by appending
the modifiers with dot notation. The order of the modifiers is not
relevant. Visit the documentation pages of the symbol modules and click
on a symbol to see its available variants.

<div class="previewed-code">

    $arrow.l$ \
    $arrow.r$ \
    $arrow.t.quad$

<div class="preview">

![Preview](/assets/e9ba4ee331e9848b80743d649bfa9b0c.png)

</div>

</div>


## symbol

```
symbol(
    str array
) -> symbol
```
Create a custom symbol with modifiers.


#### Parameters


#### variants: str, array | _required_ _positional_

The variants of the symbol.

Can be a just a string consisting of a single character for the
modifierless variant or an array with two strings specifying the
modifiers and the symbol. Individual modifiers should be separated by
dots. When displaying a symbol, Typst selects the first from the
variants that have all attached modifiers and the minimum number of
other modifiers.


### Example

<div class="previewed-code">

    #let envelope = symbol(
      "🖂",
      ("stamped", "🖃"),
      ("stamped.pen", "🖆"),
      ("lightning", "🖄"),
      ("fly", "🖅"),
    )

    #envelope
    #envelope.stamped
    #envelope.stamped.pen
    #envelope.lightning
    #envelope.fly

<div class="preview">

![Preview](/assets/29b63ba2df6949dcc2f06e985ef13f54.png)

</div>

</div>


## Definitions

