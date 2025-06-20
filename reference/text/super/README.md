
# super

```
super(
    typographic: bool
    baseline: length
    size: length
    content
) -> content
```
Renders text in superscript.

The text is rendered smaller and its baseline is raised.

## Example

<div class="previewed-code">

    1#super[st] try!

<div class="preview">

![Preview](/assets/d39db3c0aae4bd51ed655cd6eb958575.png)

</div>

</div>


### Parameters


### typographic: bool | _named_

Whether to prefer the dedicated superscript characters of the font.

If this is enabled, Typst first tries to transform the text to
superscript codepoints. If that fails, it falls back to rendering raised
and shrunk normal letters.


#### Example

<div class="previewed-code">

    N#super(typographic: true)[1]
    N#super(typographic: false)[1]

<div class="preview">

![Preview](/assets/d7fcca4246d939b0d654b4f893ed8b29.png)

</div>

</div>


### baseline: length | _named_

The baseline shift for synthetic superscripts. Does not apply if
`typographic` is true and the font has superscript codepoints for the
given `body`.


### size: length | _named_

The font size for synthetic superscripts. Does not apply if
`typographic` is true and the font has superscript codepoints for the
given `body`.


### body: content | _required_ _positional_

The text to display in superscript.

