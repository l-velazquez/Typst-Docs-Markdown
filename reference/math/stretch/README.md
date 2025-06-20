
# stretch

```
math.stretch(
    content
    size: relative
) -> content
```
Stretches a glyph.

This function can also be used to automatically stretch the base of an
attachment, so that it fits the top and bottom attachments.

Note that only some glyphs can be stretched, and which ones can depend
on the math font being used. However, most math fonts are the same in
this regard.

<div class="previewed-code">

    $ H stretch(=)^"define" U + p V $
    $ f : X stretch(->>, size: #150%)_"surjective" Y $
    $ x stretch(harpoons.ltrb, size: #3em) y
        stretch(\[, size: #150%) z $

<div class="preview">

![Preview](/assets/b3aef8dd0847dfe7ad675cbf416f9b2c.png)

</div>

</div>


### Parameters


### body: content | _required_ _positional_

The glyph to stretch.


### size: relative | _named_

The size to stretch to, relative to the maximum size of the glyph and
its attachments.

