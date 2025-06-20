
# move

```
move(
    dx: relative
    dy: relative
    content
) -> content
```
Moves content without affecting layout.

The `move` function allows you to move content while the layout still
'sees' it at the original positions. Containers will still be sized as
if the content was not moved.

## Example

<div class="previewed-code">

    #rect(inset: 0pt, move(
      dx: 6pt, dy: 6pt,
      rect(
        inset: 8pt,
        fill: white,
        stroke: black,
        [Abra cadabra]
      )
    ))

<div class="preview">

![Preview](/assets/d4c74187eb971ba906446e8361d95c24.png)

</div>

</div>


### Parameters


### dx: relative | _named_

The horizontal displacement of the content.


### dy: relative | _named_

The vertical displacement of the content.


### body: content | _required_ _positional_

The content to move.

