
# parbreak

```
parbreak(
) -> content
```
A paragraph break.

This starts a new paragraph. Especially useful when used within code
like [for loops](/reference/scripting/#loops). Multiple consecutive
paragraph breaks collapse into a single one.

## Example

<div class="previewed-code">

    #for i in range(3) {
      [Blind text #i: ]
      lorem(5)
      parbreak()
    }

<div class="preview">

![Preview](/assets/5209f40a97b9d041dd878b57ae66f860.png)

</div>

</div>

## Syntax

Instead of calling this function, you can insert a blank line into your
markup to create a paragraph break.


### Parameters

