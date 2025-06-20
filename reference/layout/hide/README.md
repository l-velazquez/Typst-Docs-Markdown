
# hide

```
hide(
    content
) -> content
```
Hides content without affecting layout.

The `hide` function allows you to hide content while the layout still
'sees' it. This is useful to create whitespace that is exactly as large
as some content. It may also be useful to redact content because its
arguments are not included in the output.

## Example

<div class="previewed-code">

    Hello Jane \
    #hide[Hello] Joe

<div class="preview">

![Preview](/assets/c348a83fa35ef3b84e31782980f262ae.png)

</div>

</div>


### Parameters


### body: content | _required_ _positional_

The content to hide.

