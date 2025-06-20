
# class

```
math.class(
    str
    content
) -> content
```
Forced use of a certain math class.

This is useful to treat certain symbols as if they were of a different
class, e.g. to make a symbol behave like a relation. The class of a
symbol defines the way it is laid out, including spacing around it, and
how its scripts are attached by default. Note that the latter can always
be overridden using [`limits`](/reference/math/attach/#functions-limits)
and [`scripts`](/reference/math/attach/#functions-scripts).

## Example

<div class="previewed-code">

    #let loves = math.class(
      "relation",
      sym.suit.heart,
    )

    $x loves y and y loves 5$

<div class="preview">

![Preview](/assets/e3ed6eac7ab33197c87fb7cb4f0ff530.png)

</div>

</div>


### Parameters


### class: str | _required_ _positional_

The class to apply to the content.


### body: content | _required_ _positional_

The content to which the class is applied.

