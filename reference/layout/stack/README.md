
# stack

```
stack(
    dir: direction
    spacing: none relative fraction
    relative fraction content
) -> content
```
Arranges content and spacing horizontally or vertically.

The stack places a list of items along an axis, with optional spacing
between each item.

## Example

<div class="previewed-code">

    #stack(
      dir: ttb,
      rect(width: 40pt),
      rect(width: 120pt),
      rect(width: 90pt),
    )

<div class="preview">

![Preview](/assets/adb95cfe03b8a39a9210f26d5c3d6a3e.png)

</div>

</div>


### Parameters


### dir: direction | _named_

The direction along which the items are stacked. Possible values are:

- `ltr`: Left to right.
- `rtl`: Right to left.
- `ttb`: Top to bottom.
- `btt`: Bottom to top.

You can use the `start` and `end` methods to obtain the initial and
final points (respectively) of a direction, as `alignment`. You can also
use the `axis` method to determine whether a direction is
<span class="typ-str">`"horizontal"`</span> or
<span class="typ-str">`"vertical"`</span>. The `inv` method returns a
direction's inverse direction.

For example,
`ttb`<span class="typ-punct">`.`</span><span class="typ-func">`start`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span>
is `top`,
`ttb`<span class="typ-punct">`.`</span><span class="typ-func">`end`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span>
is `bottom`,
`ttb`<span class="typ-punct">`.`</span><span class="typ-func">`axis`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span>
is <span class="typ-str">`"vertical"`</span> and
`ttb`<span class="typ-punct">`.`</span><span class="typ-func">`inv`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span>
is equal to `btt`.


### spacing: none, relative, fraction | _named_

Spacing to insert between items where no explicit spacing was provided.


### children: relative, fraction, content | _required_ _positional_

The children to stack along the axis.

