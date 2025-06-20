
# rotate

```
rotate(
    angle
    origin: alignment
    reflow: bool
    content
) -> content
```
Rotates content without affecting layout.

Rotates an element by a given angle. The layout will act as if the
element was not rotated unless you specify
`reflow: `<span class="typ-key">`true`</span>.

## Example

<div class="previewed-code">

    #stack(
      dir: ltr,
      spacing: 1fr,
      ..range(16)
        .map(i => rotate(24deg * i)[X]),
    )

<div class="preview">

![Preview](/assets/2913652711733d7c7032c2817b4bd215.png)

</div>

</div>


### Parameters


### angle: angle | _positional_

The amount of rotation.


#### Example

<div class="previewed-code">

    #rotate(-1.571rad)[Space!]

<div class="preview">

![Preview](/assets/fe4c7be5f5b5d6ef1363f663ea5bb2b7.png)

</div>

</div>


### origin: alignment | _named_

The origin of the rotation.

If, for instance, you wanted the bottom left corner of the rotated
element to stay aligned with the baseline, you would set it to
`bottom + left` instead.


#### Example

<div class="previewed-code">

    #set text(spacing: 8pt)
    #let square = square.with(width: 8pt)

    #box(square())
    #box(rotate(30deg, origin: center, square()))
    #box(rotate(30deg, origin: top + left, square()))
    #box(rotate(30deg, origin: bottom + right, square()))

<div class="preview">

![Preview](/assets/673042934ca6888793e71a385d773ef1.png)

</div>

</div>


### reflow: bool | _named_

Whether the rotation impacts the layout.

If set to <span class="typ-key">`false`</span>, the rotated content will
retain the bounding box of the original content. If set to
<span class="typ-key">`true`</span>, the bounding box will take the
rotation of the content into account and adjust the layout accordingly.


#### Example

<div class="previewed-code">

    Hello #rotate(90deg, reflow: true)[World]!

<div class="preview">

![Preview](/assets/8bc00ca76bf198a9f7367d30c00d59d3.png)

</div>

</div>


### body: content | _required_ _positional_

The content to rotate.

