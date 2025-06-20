
# attach

Subscript, superscripts, and limits.

Attachments can be displayed either as sub/superscripts, or limits.
Typst automatically decides which is more suitable depending on the
base, but you can also control this manually with the `scripts` and
`limits` functions.

If you want the base to stretch to fit long top and bottom attachments
(for example, an arrow with text above it), use the
[`stretch`](/reference/math/stretch/) function.

## Example

<div class="previewed-code">

    $ sum_(i=0)^n a_i = 2^(1+i) $

<div class="preview">

![Preview](/assets/411437d70da7deb746bc3f0a67ecac51.png)

</div>

</div>

## Syntax

This function also has dedicated syntax for attachments after the base:
Use the underscore (`_`) to indicate a subscript i.e. bottom attachment
and the hat (`^`) to indicate a superscript i.e. top attachment.

## attach

```
math.attach(
    content
    t: none content
    b: none content
    tl: none content
    bl: none content
    tr: none content
    br: none content
) -> content
```
A base with optional attachments.


#### Parameters


#### base: content | _required_ _positional_

The base to which things are attached.


#### t: none, content | _named_

The top attachment, smartly positioned at top-right or above the base.

You can wrap the base in
<span class="typ-func">`limits`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span>
or
<span class="typ-func">`scripts`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span>
to override the smart positioning.


#### b: none, content | _named_

The bottom attachment, smartly positioned at the bottom-right or below
the base.

You can wrap the base in
<span class="typ-func">`limits`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span>
or
<span class="typ-func">`scripts`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span>
to override the smart positioning.


#### tl: none, content | _named_

The top-left attachment (before the base).


#### bl: none, content | _named_

The bottom-left attachment (before base).


#### tr: none, content | _named_

The top-right attachment (after the base).


#### br: none, content | _named_

The bottom-right attachment (after the base).


### Example

<div class="previewed-code">

    $ attach(
      Pi, t: alpha, b: beta,
      tl: 1, tr: 2+3, bl: 4+5, br: 6,
    ) $

<div class="preview">

![Preview](/assets/84fd52f8518c49b5d0c2154d3762e8c5.png)

</div>

</div>


## scripts

```
math.scripts(
    content
) -> content
```
Forces a base to display attachments as scripts.


#### Parameters


#### body: content | _required_ _positional_

The base to attach the scripts to.


### Example

<div class="previewed-code">

    $ scripts(sum)_1^2 != sum_1^2 $

<div class="preview">

![Preview](/assets/c9599c27cd86c13285b8d314e2c8528c.png)

</div>

</div>


## limits

```
math.limits(
    content
    inline: bool
) -> content
```
Forces a base to display attachments as limits.


#### Parameters


#### body: content | _required_ _positional_

The base to attach the limits to.


#### inline: bool | _named_

Whether to also force limits in inline equations.

When applying limits globally (e.g., through a show rule), it is
typically a good idea to disable this.


### Example

<div class="previewed-code">

    $ limits(A)_1^2 != A_1^2 $

<div class="preview">

![Preview](/assets/ffb91cddf4edf78f1af94d7ff70772ce.png)

</div>

</div>

