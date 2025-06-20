
# styles

Alternate letterforms within formulas.

These functions are distinct from the
[`text`](/reference/text/text/ "`text`") function because math fonts
contain multiple variants of each letter.

## upright

```
math.upright(
    content
) -> content
```
Upright (non-italic) font style in math.


#### Parameters


#### body: content | _required_ _positional_

The content to style.


### Example

<div class="previewed-code">

    $ upright(A) != A $

<div class="preview">

![Preview](/assets/2375f3944b651050f90b0f7ab2b4b59e.png)

</div>

</div>


## italic

```
math.italic(
    content
) -> content
```
Italic font style in math.

For roman letters and greek lowercase letters, this is already the
default.


#### Parameters


#### body: content | _required_ _positional_

The content to style.


## bold

```
math.bold(
    content
) -> content
```
Bold font style in math.


#### Parameters


#### body: content | _required_ _positional_

The content to style.


### Example

<div class="previewed-code">

    $ bold(A) := B^+ $

<div class="preview">

![Preview](/assets/f3ef64e42845d8f3b5dffc758a93e400.png)

</div>

</div>

