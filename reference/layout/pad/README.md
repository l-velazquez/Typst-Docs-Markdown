
# pad

```
pad(
    left: relative
    top: relative
    right: relative
    bottom: relative
    x: relative
    y: relative
    rest: relative
    content
) -> content
```
Adds spacing around content.

The spacing can be specified for each side individually, or for all
sides at once by specifying a positional argument.

## Example

<div class="previewed-code">

    #set align(center)

    #pad(x: 16pt, image("typing.jpg"))
    _Typing speeds can be
     measured in words per minute._

<div class="preview">

![Preview](/assets/627bf363796cd87adc3e0a240ccc55ab.png)

</div>

</div>


### Parameters


### left: relative | _named_

The padding at the left side.


### top: relative | _named_

The padding at the top side.


### right: relative | _named_

The padding at the right side.


### bottom: relative | _named_

The padding at the bottom side.


### x: relative | _named_

A shorthand to set `left` and `right` to the same value.


### y: relative | _named_

A shorthand to set `top` and `bottom` to the same value.


### rest: relative | _named_

A shorthand to set all four sides to the same value.


### body: content | _required_ _positional_

The content to pad at the sides.

