
# accent

```
math.accent(
    content
    str content
    size: relative
    dotless: bool
) -> content
```
Attaches an accent to a base.

## Example

<div class="previewed-code">

    $grave(a) = accent(a, `)$ \
    $arrow(a) = accent(a, arrow)$ \
    $tilde(a) = accent(a, \u{0303})$

<div class="preview">

![Preview](/assets/c1d2d9103d9cbed5ca014ef9bcab402b.png)

</div>

</div>


### Parameters


### base: content | _required_ _positional_

The base to which the accent is applied. May consist of multiple
letters.


#### Example

<div class="previewed-code">

    $arrow(A B C)$

<div class="preview">

![Preview](/assets/695a59b99713825042bc5f246e3c4dec.png)

</div>

</div>


### accent: str, content | _required_ _positional_

The accent to apply to the base.

Supported accents include:

| Accent                | Name                  | Codepoint |
|-----------------------|-----------------------|-----------|
| Grave                 | `grave`               | `` ` ``   |
| Acute                 | `acute`               | `´`       |
| Circumflex            | `hat`                 | `^`       |
| Tilde                 | `tilde`               | `~`       |
| Macron                | `macron`              | `¯`       |
| Dash                  | `dash`                | `‾`       |
| Breve                 | `breve`               | `˘`       |
| Dot                   | `dot`                 | `.`       |
| Double dot, Diaeresis | `dot.double`, `diaer` | `¨`       |
| Triple dot            | `dot.triple`          | `⃛`        |
| Quadruple dot         | `dot.quad`            | `⃜`        |
| Circle                | `circle`              | `∘`       |
| Double acute          | `acute.double`        | `˝`       |
| Caron                 | `caron`               | `ˇ`       |
| Right arrow           | `arrow`, `->`         | `→`       |
| Left arrow            | `arrow.l`, `<-`       | `←`       |
| Left/Right arrow      | `arrow.l.r`           | `↔`       |
| Right harpoon         | `harpoon`             | `⇀`       |
| Left harpoon          | `harpoon.lt`          | `↼`       |


### size: relative | _named_

The size of the accent, relative to the width of the base.


#### Example

<div class="previewed-code">

    $dash(A, size: #150%)$

<div class="preview">

![Preview](/assets/86ae8b36db880e0350036e149fff5a22.png)

</div>

</div>


### dotless: bool | _named_

Whether to remove the dot on top of lowercase i and j when adding a top
accent.

This enables the `dtls` OpenType feature.


#### Example

<div class="previewed-code">

    $hat(dotless: #false, i)$

<div class="preview">

![Preview](/assets/739dfe1b39a87e4783e3d11d043a9fb6.png)

</div>

</div>

