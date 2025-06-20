
# sub

```
sub(
    typographic: bool
    baseline: length
    size: length
    content
) -> content
```
Renders text in subscript.

The text is rendered smaller and its baseline is lowered.

## Example

<div class="previewed-code">

    Revenue#sub[yearly]

<div class="preview">

![Preview](/assets/aba9b70776d538b28fb89148a20a8833.png)

</div>

</div>


### Parameters


### typographic: bool | _named_

Whether to prefer the dedicated subscript characters of the font.

If this is enabled, Typst first tries to transform the text to subscript
codepoints. If that fails, it falls back to rendering lowered and shrunk
normal letters.


#### Example

<div class="previewed-code">

    N#sub(typographic: true)[1]
    N#sub(typographic: false)[1]

<div class="preview">

![Preview](/assets/786b89e1ca0f1dc21ba334ef18abd42c.png)

</div>

</div>


### baseline: length | _named_

The baseline shift for synthetic subscripts. Does not apply if
`typographic` is true and the font has subscript codepoints for the
given `body`.


### size: length | _named_

The font size for synthetic subscripts. Does not apply if `typographic`
is true and the font has subscript codepoints for the given `body`.


### body: content | _required_ _positional_

The text to display in subscript.

