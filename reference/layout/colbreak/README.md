
# colbreak

```
colbreak(
    weak: bool
) -> content
```
Forces a column break.

The function will behave like a [page
break](/reference/layout/pagebreak/) when used in a single column layout
or the last column on a page. Otherwise, content after the column break
will be placed in the next column.

## Example

<div class="previewed-code">

    #set page(columns: 2)
    Preliminary findings from our
    ongoing research project have
    revealed a hitherto unknown
    phenomenon of extraordinary
    significance.

    #colbreak()
    Through rigorous experimentation
    and analysis, we have discovered
    a hitherto uncharacterized process
    that defies our current
    understanding of the fundamental
    laws of nature.

<div class="preview">

![Preview](/assets/317ca576aa5033b3292e2f600bab0f18.png)

</div>

</div>


### Parameters


### weak: bool | _named_

If <span class="typ-key">`true`</span>, the column break is skipped if
the current column is already empty.

