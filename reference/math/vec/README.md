
# vec

```
math.vec(
    delim: none str array symbol
    align: alignment
    gap: relative
    content
) -> content
```
A column vector.

Content in the vector's elements can be aligned with the
[`align`](/reference/math/vec/#parameters-align) parameter, or the `&`
symbol.

## Example

<div class="previewed-code">

    $ vec(a, b, c) dot vec(1, 2, 3)
        = a + 2b + 3c $

<div class="preview">

![Preview](/assets/2e7466d3a94b320803f1f09065d03ae9.png)

</div>

</div>


### Parameters


### delim: none, str, array, symbol | _named_

The delimiter to use.

Can be a single character specifying the left delimiter, in which case
the right delimiter is inferred. Otherwise, can be an array containing a
left and a right delimiter.


#### Example

<div class="previewed-code">

    #set math.vec(delim: "[")
    $ vec(1, 2) $

<div class="preview">

![Preview](/assets/e4b15927d776e5b9635c5a7a90044772.png)

</div>

</div>


### align: alignment | _named_

The horizontal alignment that each element should have.


#### Example

<div class="previewed-code">

    #set math.vec(align: right)
    $ vec(-1, 1, -1) $

<div class="preview">

![Preview](/assets/66d1e5a7d638cc4b73e7761d7f9ba72c.png)

</div>

</div>


### gap: relative | _named_

The gap between elements.


#### Example

<div class="previewed-code">

    #set math.vec(gap: 1em)
    $ vec(1, 2) $

<div class="preview">

![Preview](/assets/ba22b66d050a8c8cdc3b7206a7b4593f.png)

</div>

</div>


### children: content | _required_ _positional_

The elements of the vector.

