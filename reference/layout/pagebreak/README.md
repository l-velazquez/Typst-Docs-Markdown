
# pagebreak

```
pagebreak(
    weak: bool
    to: none str
) -> content
```
A manual page break.

Must not be used inside any containers.

## Example

<div class="previewed-code">

    The next page contains
    more details on compound theory.
    #pagebreak()

    == Compound Theory
    In 1984, the first ...

<div class="preview">

![Preview](/assets/3098eee9a9bf195060b49592b4463703.png)

</div>

</div>


### Parameters


### weak: bool | _named_

If <span class="typ-key">`true`</span>, the page break is skipped if the
current page is already empty.


### to: none, str | _named_

If given, ensures that the next page will be an even/odd page, with an
empty page in between if necessary.


#### Example

<div class="previewed-code">

    #set page(height: 30pt)

    First.
    #pagebreak(to: "odd")
    Third.

<div class="preview">

![Preview](/assets/ff80837b479a5387b266d55477502b8a.png)

</div>

</div>

