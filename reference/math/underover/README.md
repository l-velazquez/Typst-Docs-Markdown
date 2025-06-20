
# underover

Delimiters above or below parts of an equation.

The braces and brackets further allow you to add an optional annotation
below or above themselves.

## underline

```
math.underline(
    content
) -> content
```
A horizontal line under content.


#### Parameters


#### body: content | _required_ _positional_

The content above the line.


### Example

<div class="previewed-code">

    $ underline(1 + 2 + ... + 5) $

<div class="preview">

![Preview](/assets/90fbf6ae4b8e62a139c6b4bd8329f2ab.png)

</div>

</div>


## overline

```
math.overline(
    content
) -> content
```
A horizontal line over content.


#### Parameters


#### body: content | _required_ _positional_

The content below the line.


### Example

<div class="previewed-code">

    $ overline(1 + 2 + ... + 5) $

<div class="preview">

![Preview](/assets/6eb6edcdeea961c6dd0c7657a98b57e1.png)

</div>

</div>


## underbrace

```
math.underbrace(
    content
    none content
) -> content
```
A horizontal brace under content, with an optional annotation below.


#### Parameters


#### body: content | _required_ _positional_

The content above the brace.


#### annotation: none, content | _positional_

The optional content below the brace.


### Example

<div class="previewed-code">

    $ underbrace(1 + 2 + ... + 5, "numbers") $

<div class="preview">

![Preview](/assets/903eb82e0d7a4bd8aaaa179d2ba2834.png)

</div>

</div>


## overbrace

```
math.overbrace(
    content
    none content
) -> content
```
A horizontal brace over content, with an optional annotation above.


#### Parameters


#### body: content | _required_ _positional_

The content below the brace.


#### annotation: none, content | _positional_

The optional content above the brace.


### Example

<div class="previewed-code">

    $ overbrace(1 + 2 + ... + 5, "numbers") $

<div class="preview">

![Preview](/assets/924046495c724e4e7f2f593f106f08de.png)

</div>

</div>


## underbracket

```
math.underbracket(
    content
    none content
) -> content
```
A horizontal bracket under content, with an optional annotation below.


#### Parameters


#### body: content | _required_ _positional_

The content above the bracket.


#### annotation: none, content | _positional_

The optional content below the bracket.


### Example

<div class="previewed-code">

    $ underbracket(1 + 2 + ... + 5, "numbers") $

<div class="preview">

![Preview](/assets/80e269d7914a9b870e10e1db5b81fe3b.png)

</div>

</div>


## overbracket

```
math.overbracket(
    content
    none content
) -> content
```
A horizontal bracket over content, with an optional annotation above.


#### Parameters


#### body: content | _required_ _positional_

The content below the bracket.


#### annotation: none, content | _positional_

The optional content above the bracket.


### Example

<div class="previewed-code">

    $ overbracket(1 + 2 + ... + 5, "numbers") $

<div class="preview">

![Preview](/assets/d450da709982d29facd0739d468afb5a.png)

</div>

</div>


## underparen

```
math.underparen(
    content
    none content
) -> content
```
A horizontal parenthesis under content, with an optional annotation
below.


#### Parameters


#### body: content | _required_ _positional_

The content above the parenthesis.


#### annotation: none, content | _positional_

The optional content below the parenthesis.


### Example

<div class="previewed-code">

    $ underparen(1 + 2 + ... + 5, "numbers") $

<div class="preview">

![Preview](/assets/2fd6fccafb542e0079aaa96262a2e56c.png)

</div>

</div>


## overparen

```
math.overparen(
    content
    none content
) -> content
```
A horizontal parenthesis over content, with an optional annotation
above.


#### Parameters


#### body: content | _required_ _positional_

The content below the parenthesis.


#### annotation: none, content | _positional_

The optional content above the parenthesis.


### Example

<div class="previewed-code">

    $ overparen(1 + 2 + ... + 5, "numbers") $

<div class="preview">

![Preview](/assets/d0efcf75e3fd683e0875b88014f2c773.png)

</div>

</div>


## undershell

```
math.undershell(
    content
    none content
) -> content
```
A horizontal tortoise shell bracket under content, with an optional
annotation below.


#### Parameters


#### body: content | _required_ _positional_

The content above the tortoise shell bracket.


#### annotation: none, content | _positional_

The optional content below the tortoise shell bracket.


### Example

<div class="previewed-code">

    $ undershell(1 + 2 + ... + 5, "numbers") $

<div class="preview">

![Preview](/assets/a89478cda198b446c24a0c23d2407356.png)

</div>

</div>


## overshell

```
math.overshell(
    content
    none content
) -> content
```
A horizontal tortoise shell bracket over content, with an optional
annotation above.


#### Parameters


#### body: content | _required_ _positional_

The content below the tortoise shell bracket.


#### annotation: none, content | _positional_

The optional content above the tortoise shell bracket.


### Example

<div class="previewed-code">

    $ overshell(1 + 2 + ... + 5, "numbers") $

<div class="preview">

![Preview](/assets/bcf034bf413f257c2c0b506968295c12.png)

</div>

</div>

