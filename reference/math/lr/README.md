
# lr

Delimiter matching.

The `lr` function allows you to match two delimiters and scale them with
the content they contain. While this also happens automatically for
delimiters that match syntactically, `lr` allows you to match two
arbitrary delimiters and control their size exactly. Apart from the `lr`
function, Typst provides a few more functions that create delimiter
pairings for absolute, ceiled, and floored values as well as norms.

To prevent a delimiter from being matched by Typst, and thus
auto-scaled, escape it with a backslash. To instead disable auto-scaling
completely, use
<span class="typ-key">`set`</span>` math`<span class="typ-punct">`.`</span><span class="typ-func">`lr`</span><span class="typ-punct">`(`</span>`size`<span class="typ-punct">`:`</span>` `<span class="typ-num">`1em`</span><span class="typ-punct">`)`</span>.

## Example

<div class="previewed-code">

    $ [a, b/2] $
    $ lr(]sum_(x=1)^n], size: #50%) x $
    $ abs((x + y) / 2) $
    $ \{ (x / y) \} $
    #set math.lr(size: 1em)
    $ { (a / b), a, b in (0; 1/2] } $

<div class="preview">

![Preview](/assets/63330327318f138d9440594430988bbb.png)

</div>

</div>

## lr

```
math.lr(
    size: relative
    content
) -> content
```
Scales delimiters.

While matched delimiters scale by default, this can be used to scale
unmatched delimiters and to control the delimiter scaling more
precisely.


#### Parameters


#### size: relative | _named_

The size of the brackets, relative to the height of the wrapped content.


#### body: content | _required_ _positional_

The delimited content, including the delimiters.


## mid

```
math.mid(
    content
) -> content
```
Scales delimiters vertically to the nearest surrounding
<span class="typ-func">`lr`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span>
group.


#### Parameters


#### body: content | _required_ _positional_

The content to be scaled.


### Example

<div class="previewed-code">

    $ { x mid(|) sum_(i=1)^n w_i|f_i (x)| < 1 } $

<div class="preview">

![Preview](/assets/a29f9290887cdd1f41b9003f982e3560.png)

</div>

</div>


## abs

```
math.abs(
    size: relative
    content
) -> content
```
Takes the absolute value of an expression.


#### Parameters


#### size: relative | _named_

The size of the brackets, relative to the height of the wrapped content.


#### body: content | _required_ _positional_

The expression to take the absolute value of.


### Example

<div class="previewed-code">

    $ abs(x/2) $

<div class="preview">

![Preview](/assets/5892ee44ad18813000297eeafd1b6e78.png)

</div>

</div>


## norm

```
math.norm(
    size: relative
    content
) -> content
```
Takes the norm of an expression.


#### Parameters


#### size: relative | _named_

The size of the brackets, relative to the height of the wrapped content.


#### body: content | _required_ _positional_

The expression to take the norm of.


### Example

<div class="previewed-code">

    $ norm(x/2) $

<div class="preview">

![Preview](/assets/602e918d9e4207139477dfb451df53cd.png)

</div>

</div>


## floor

```
math.floor(
    size: relative
    content
) -> content
```
Floors an expression.


#### Parameters


#### size: relative | _named_

The size of the brackets, relative to the height of the wrapped content.


#### body: content | _required_ _positional_

The expression to floor.


### Example

<div class="previewed-code">

    $ floor(x/2) $

<div class="preview">

![Preview](/assets/3c3107954755188561218b3da59b9b88.png)

</div>

</div>


## ceil

```
math.ceil(
    size: relative
    content
) -> content
```
Ceils an expression.


#### Parameters


#### size: relative | _named_

The size of the brackets, relative to the height of the wrapped content.


#### body: content | _required_ _positional_

The expression to ceil.


### Example

<div class="previewed-code">

    $ ceil(x/2) $

<div class="preview">

![Preview](/assets/f0cd1c0e8d2655688398c799bc806a38.png)

</div>

</div>


## round

```
math.round(
    size: relative
    content
) -> content
```
Rounds an expression.


#### Parameters


#### size: relative | _named_

The size of the brackets, relative to the height of the wrapped content.


#### body: content | _required_ _positional_

The expression to round.


### Example

<div class="previewed-code">

    $ round(x/2) $

<div class="preview">

![Preview](/assets/b45f33012980296a7361d593384f333c.png)

</div>

</div>

