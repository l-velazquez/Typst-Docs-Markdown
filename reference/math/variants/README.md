
# variants

Alternate typefaces within formulas.

These functions are distinct from the
[`text`](/reference/text/text/ "`text`") function because math fonts
contain multiple variants of each letter.

## serif

```
math.serif(
    content
) -> content
```
Serif (roman) font style in math.

This is already the default.


#### Parameters


#### body: content | _required_ _positional_

The content to style.


## sans

```
math.sans(
    content
) -> content
```
Sans-serif font style in math.


#### Parameters


#### body: content | _required_ _positional_

The content to style.


### Example

<div class="previewed-code">

    $ sans(A B C) $

<div class="preview">

![Preview](/assets/407ec97977e50acfb00a33fc9e4056ad.png)

</div>

</div>


## frak

```
math.frak(
    content
) -> content
```
Fraktur font style in math.


#### Parameters


#### body: content | _required_ _positional_

The content to style.


### Example

<div class="previewed-code">

    $ frak(P) $

<div class="preview">

![Preview](/assets/7bc5e4240760597643a9b5acf7819e79.png)

</div>

</div>


## mono

```
math.mono(
    content
) -> content
```
Monospace font style in math.


#### Parameters


#### body: content | _required_ _positional_

The content to style.


### Example

<div class="previewed-code">

    $ mono(x + y = z) $

<div class="preview">

![Preview](/assets/55d904edd40fbf32537bb0710d91dc9f.png)

</div>

</div>


## bb

```
math.bb(
    content
) -> content
```
Blackboard bold (double-struck) font style in math.

For uppercase latin letters, blackboard bold is additionally available
through [symbols](/reference/symbols/sym/) of the form `NN` and `RR`.


#### Parameters


#### body: content | _required_ _positional_

The content to style.


### Example

<div class="previewed-code">

    $ bb(b) $
    $ bb(N) = NN $
    $ f: NN -> RR $

<div class="preview">

![Preview](/assets/eeab38b02d476b4bcefc48bf7678c7b9.png)

</div>

</div>


## cal

```
math.cal(
    content
) -> content
```
Calligraphic font style in math.


#### Parameters


#### body: content | _required_ _positional_

The content to style.


### Example

<div class="previewed-code">

    Let $cal(P)$ be the set of ...

<div class="preview">

![Preview](/assets/92ac6bdff36119c06add06619087c88f.png)

</div>

</div>

This corresponds both to LaTeX's `\mathcal` and `\mathscr` as both of
these styles share the same Unicode codepoints. Switching between the
styles is thus only possible if supported by the font via [font
features](/reference/text/text/#parameters-features).

For the default math font, the roundhand style is available through the
`ss01` feature. Therefore, you could define your own version of
`\mathscr` like this:

<div class="previewed-code">

    #let scr(it) = text(
      features: ("ss01",),
      box($cal(it)$),
    )

    We establish $cal(P) != scr(P)$.

<div class="preview">

![Preview](/assets/3cb10e42a618f6a8962f0095bfc8ff1c.png)

</div>

</div>

(The box is not conceptually necessary, but unfortunately currently
needed due to limitations in Typst's text style handling in math.)

