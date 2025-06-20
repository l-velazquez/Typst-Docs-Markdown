
# repeat

```
repeat(
    content
    gap: length
    justify: bool
) -> content
```
Repeats content to the available space.

This can be useful when implementing a custom index, reference, or
outline.

Space may be inserted between the instances of the body parameter, so be
sure to adjust the
[`justify`](/reference/layout/repeat/#parameters-justify) parameter
accordingly.

Errors if there are no bounds on the available space, as it would create
infinite content.

## Example

<div class="previewed-code">

    Sign on the dotted line:
    #box(width: 1fr, repeat[.])

    #set text(10pt)
    #v(8pt, weak: true)
    #align(right)[
      Berlin, the 22nd of December, 2022
    ]

<div class="preview">

![Preview](/assets/2c620b6b8e39dd107ac681286f399070.png)

</div>

</div>


### Parameters


### body: content | _required_ _positional_

The content to repeat.


### gap: length | _named_

The gap between each instance of the body.


### justify: bool | _named_

Whether to increase the gap between instances to completely fill the
available space.

