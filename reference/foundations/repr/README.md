
# repr

```
repr(
    any
) -> str
```
Returns the string representation of a value.

When inserted into content, most values are displayed as this
representation in monospace with syntax-highlighting. The exceptions are
<span class="typ-key">`none`</span>, integers, floats, strings, content,
and functions.

**Note:** This function is for debugging purposes. Its output should not
be considered stable and may change at any time!

## Example

<div class="previewed-code">

    #none vs #repr(none) \
    #"hello" vs #repr("hello") \
    #(1, 2) vs #repr((1, 2)) \
    #[*Hi*] vs #repr([*Hi*])

<div class="preview">

![Preview](/assets/84ebd00100d33ebdd6015bb8c7c1e483.png)

</div>

</div>


### Parameters


### value: any | _required_ _positional_

The value whose string representation to produce.

