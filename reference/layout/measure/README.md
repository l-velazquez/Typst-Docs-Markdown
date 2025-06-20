
# measure

```
measure(
    width: auto length
    height: auto length
    content
) -> dictionary
```
Measures the layouted size of content.

The `measure` function lets you determine the layouted size of content.
By default an infinite space is assumed, so the measured dimensions may
not necessarily match the final dimensions of the content. If you want
to measure in the current layout dimensions, you can combine `measure`
and [`layout`](/reference/layout/layout/ "`layout`").

## Example

The same content can have a different size depending on the
[context](/reference/context/ "context") that it is placed into. In the
example below, the
<span class="typ-pol">`#`</span><span class="typ-pol">`content`</span>
is of course bigger when we increase the font size.

<div class="previewed-code">

    #let content = [Hello!]
    #content
    #set text(14pt)
    #content

<div class="preview">

![Preview](/assets/213f7d67a16c2b7124176f09e63be87.png)

</div>

</div>

For this reason, you can only measure when context is available.

<div class="previewed-code">

    #let thing(body) = context {
      let size = measure(body)
      [Width of "#body" is #size.width]
    }

    #thing[Hey] \
    #thing[Welcome]

<div class="preview">

![Preview](/assets/fb2e80b8ddc9deb97b1b3d71fd54638f.png)

</div>

</div>

The measure function returns a dictionary with the entries `width` and
`height`, both of type [`length`](/reference/layout/length/ "`length`").


### Parameters


### width: auto, length | _named_

The width available to layout the content.

Setting this to <span class="typ-key">`auto`</span> indicates infinite
available width.

Note that using the `width` and `height` parameters of this function is
different from measuring a sized
[`block`](/reference/layout/block/ "`block`") containing the content. In
the following example, the former will get the dimensions of the inner
content instead of the dimensions of the block.


#### Example

<div class="previewed-code">

    #context measure(lorem(100), width: 400pt)

    #context measure(block(lorem(100), width: 400pt))

<div class="preview">

![Preview](/assets/9063ce7197f1cd611fa96cca40225a16.png)

</div>

</div>


### height: auto, length | _named_

The height available to layout the content.

Setting this to <span class="typ-key">`auto`</span> indicates infinite
available height.


### content: content | _required_ _positional_

The content whose size to measure.

