
# emph

```
emph(
    content
) -> content
```
Emphasizes content by toggling italics.

- If the current [text style](/reference/text/text/#parameters-style) is
  <span class="typ-str">`"normal"`</span>, this turns it into
  <span class="typ-str">`"italic"`</span>.
- If it is already <span class="typ-str">`"italic"`</span> or
  <span class="typ-str">`"oblique"`</span>, it turns it back to
  <span class="typ-str">`"normal"`</span>.

## Example

<div class="previewed-code">

    This is _emphasized._ \
    This is #emph[too.]

    #show emph: it => {
      text(blue, it.body)
    }

    This is _emphasized_ differently.

<div class="preview">

![Preview](/assets/a777060a068976b92b49c3a2b5aed07e.png)

</div>

</div>

## Syntax

This function also has dedicated syntax: To emphasize content, simply
enclose it in underscores (`_`). Note that this only works at word
boundaries. To emphasize part of a word, you have to use the function.


### Parameters


### body: content | _required_ _positional_

The content to emphasize.

