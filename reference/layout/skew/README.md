
# skew

```
skew(
    ax: angle
    ay: angle
    origin: alignment
    reflow: bool
    content
) -> content
```
Skews content.

Skews an element in horizontal and/or vertical direction. The layout
will act as if the element was not skewed unless you specify
`reflow: `<span class="typ-key">`true`</span>.

## Example

<div class="previewed-code">

    #skew(ax: -12deg)[
      This is some fake italic text.
    ]

<div class="preview">

![Preview](/assets/154b52c95b3e31ae6bbd43fc074c397d.png)

</div>

</div>


### Parameters


### ax: angle | _named_

The horizontal skewing angle.


#### Example

<div class="previewed-code">

    #skew(ax: 30deg)[Skewed]

<div class="preview">

![Preview](/assets/1fd93686547f1d8c29e4c343e34cf7ae.png)

</div>

</div>


### ay: angle | _named_

The vertical skewing angle.


#### Example

<div class="previewed-code">

    #skew(ay: 30deg)[Skewed]

<div class="preview">

![Preview](/assets/c8b3992019d91ea57c698075add2fc4.png)

</div>

</div>


### origin: alignment | _named_

The origin of the skew transformation.

The origin will stay fixed during the operation.


#### Example

<div class="previewed-code">

    X #box(skew(ax: -30deg, origin: center + horizon)[X]) X \
    X #box(skew(ax: -30deg, origin: bottom + left)[X]) X \
    X #box(skew(ax: -30deg, origin: top + right)[X]) X

<div class="preview">

![Preview](/assets/d87ab8185612d6d4aa0a796ecf78db71.png)

</div>

</div>


### reflow: bool | _named_

Whether the skew transformation impacts the layout.

If set to <span class="typ-key">`false`</span>, the skewed content will
retain the bounding box of the original content. If set to
<span class="typ-key">`true`</span>, the bounding box will take the
transformation of the content into account and adjust the layout
accordingly.


#### Example

<div class="previewed-code">

    Hello #skew(ay: 30deg, reflow: true, "World")!

<div class="preview">

![Preview](/assets/fa4f8f52e45ecc3faaea3eef93ec5058.png)

</div>

</div>


### body: content | _required_ _positional_

The content to skew.

