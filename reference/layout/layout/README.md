
# layout

```
layout(
    function
) -> content
```
Provides access to the current outer container's (or page's, if none)
dimensions (width and height).

Accepts a function that receives a single parameter, which is a
dictionary with keys `width` and `height`, both of type
[`length`](/reference/layout/length/ "`length`"). The function is
provided [context](/reference/context/ "context"), meaning you don't
need to use it in combination with the `context` keyword. This is why
[`measure`](/reference/layout/measure/ "`measure`") can be called in the
example below.

<div class="previewed-code">

    #let text = lorem(30)
    #layout(size => [
      #let (height,) = measure(
        width: size.width,
        text,
      )
      This text is #height high with
      the current page width: \
      #text
    ])

<div class="preview">

![Preview](/assets/cc7bcca62e697ffb30df3438570db1ab.png)

</div>

</div>

Note that the `layout` function forces its contents into a
[block](/reference/layout/block/ "block")-level container, so placement
relative to the page or pagebreaks are not possible within it.

If the `layout` call is placed inside a box with a width of
<span class="typ-num">`800pt`</span> and a height of
<span class="typ-num">`400pt`</span>, then the specified function will
be given the argument
<span class="typ-punct">`(`</span>`width`<span class="typ-punct">`:`</span>` `<span class="typ-num">`800pt`</span><span class="typ-punct">`,`</span>` height`<span class="typ-punct">`:`</span>` `<span class="typ-num">`400pt`</span><span class="typ-punct">`)`</span>.
If it is placed directly into the page, it receives the page's
dimensions minus its margins. This is mostly useful in combination with
[measurement](/reference/layout/measure/).

To retrieve the *remaining* height of the page rather than its full
size, you can wrap your `layout` call in a
<span class="typ-func">`block`</span><span class="typ-punct">`(`</span>`height`<span class="typ-punct">`:`</span>` `<span class="typ-num">`1fr`</span><span class="typ-punct">`)`</span>.
This works because the block automatically grows to fill the remaining
space (see the [fraction](/reference/layout/fraction/ "fraction")
documentation for more details).

<div class="previewed-code">

    #set page(height: 150pt)

    #lorem(20)

    #block(height: 1fr, layout(size => [
      Remaining height: #size.height
    ]))

<div class="preview">

![Preview](/assets/287861b8e3129cb301b74afa92ff7a07.png)

</div>

</div>

You can also use this function to resolve a
[`ratio`](/reference/layout/ratio/ "`ratio`") to a fixed length. This
might come in handy if you're building your own layout abstractions.

<div class="previewed-code">

    #layout(size => {
      let half = 50% * size.width
      [Half a page is #half wide.]
    })

<div class="preview">

![Preview](/assets/d40a0e3eb100447da2f5971d71a9a270.png)

</div>

</div>

Note that the width or height provided by `layout` will be infinite if
the corresponding page dimension is set to
<span class="typ-key">`auto`</span>.


### Parameters


### func: function | _required_ _positional_

A function to call with the outer container's size. Its return value is
displayed in the document.

The container's size is given as a
[dictionary](/reference/foundations/dictionary/ "dictionary") with the
keys `width` and `height`.

This function is called once for each time the content returned by
`layout` appears in the document. This makes it possible to generate
content that depends on the dimensions of its container.

