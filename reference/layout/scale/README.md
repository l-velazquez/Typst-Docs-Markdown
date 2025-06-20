
# scale

```
scale(
    auto length ratio
    x: auto length ratio
    y: auto length ratio
    origin: alignment
    reflow: bool
    content
) -> content
```
Scales content without affecting layout.

Lets you mirror content by specifying a negative scale on a single axis.

## Example

<div class="previewed-code">

    #set align(center)
    #scale(x: -100%)[This is mirrored.]
    #scale(x: -100%, reflow: true)[This is mirrored.]

<div class="preview">

![Preview](/assets/4a11fc3689aa86e118aeb7546c0a6368.png)

</div>

</div>


### Parameters


### factor: auto, length, ratio | _positional_

The scaling factor for both axes, as a positional argument. This is just
an optional shorthand notation for setting `x` and `y` to the same
value.


### x: auto, length, ratio | _named_

The horizontal scaling factor.

The body will be mirrored horizontally if the parameter is negative.


### y: auto, length, ratio | _named_

The vertical scaling factor.

The body will be mirrored vertically if the parameter is negative.


### origin: alignment | _named_

The origin of the transformation.


#### Example

<div class="previewed-code">

    A#box(scale(75%)[A])A \
    B#box(scale(75%, origin: bottom + left)[B])B

<div class="preview">

![Preview](/assets/753e3d1a1bca7e3f8a8ff37f29db41a9.png)

</div>

</div>


### reflow: bool | _named_

Whether the scaling impacts the layout.

If set to <span class="typ-key">`false`</span>, the scaled content will
be allowed to overlap other content. If set to
<span class="typ-key">`true`</span>, it will compute the new size of the
scaled content and adjust the layout accordingly.


#### Example

<div class="previewed-code">

    Hello #scale(x: 20%, y: 40%, reflow: true)[World]!

<div class="preview">

![Preview](/assets/f2a115827e2953ff282e69617b8717d9.png)

</div>

</div>


### body: content | _required_ _positional_

The content to scale.

