
# strong

```
strong(
    delta: int
    content
) -> content
```
Strongly emphasizes content by increasing the font weight.

Increases the current font weight by a given `delta`.

## Example

<div class="previewed-code">

    This is *strong.* \
    This is #strong[too.] \

    #show strong: set text(red)
    And this is *evermore.*

<div class="preview">

![Preview](/assets/f0f155e1250d5cd6db61ef6e1d6d484c.png)

</div>

</div>

## Syntax

This function also has dedicated syntax: To strongly emphasize content,
simply enclose it in stars/asterisks (`*`). Note that this only works at
word boundaries. To strongly emphasize part of a word, you have to use
the function.


### Parameters


### delta: int | _named_

The delta to apply on the font weight.


#### Example

<div class="previewed-code">

    #set strong(delta: 0)
    No *effect!*

<div class="preview">

![Preview](/assets/482ecb9a7454c6daefc502f7df57e97c.png)

</div>

</div>


### body: content | _required_ _positional_

The content to strongly emphasize.

