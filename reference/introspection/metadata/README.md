
# metadata

```
metadata(
    any
) -> content
```
Exposes a value to the query system without producing visible content.

This element can be retrieved with the
[`query`](/reference/introspection/query/ "`query`") function and from
the command line with
[`typst query`](/reference/introspection/query/#command-line-queries).
Its purpose is to expose an arbitrary value to the introspection system.
To identify a metadata value among others, you can attach a
[`label`](/reference/foundations/label/ "`label`") to it and query for
that label.

The `metadata` element is especially useful for command line queries
because it allows you to expose arbitrary values to the outside world.

<div class="previewed-code">

    // Put metadata somewhere.
    #metadata("This is a note") <note>

    // And find it from anywhere else.
    #context {
      query(<note>).first().value
    }

<div class="preview">

![Preview](/assets/b1b17f01cf3adfe808d66deaa0bf5abf.png)

</div>

</div>


### Parameters


### value: any | _required_ _positional_

The value to embed into the document.

