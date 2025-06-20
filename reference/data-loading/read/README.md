
# read

```
read(
    str
    encoding: none str
) -> str bytes
```
Reads plain text or data from a file.

By default, the file will be read as UTF-8 and returned as a
[string](/reference/foundations/str/).

If you specify `encoding: `<span class="typ-key">`none`</span>, this
returns raw [bytes](/reference/foundations/bytes/ "bytes") instead.

## Example

<div class="previewed-code">

    An example for a HTML file: \
    #let text = read("example.html")
    #raw(text, lang: "html")

    Raw bytes:
    #read("tiger.jpg", encoding: none)

<div class="preview">

![Preview](/assets/b92e43ad9c335363c8a8efef74973b19.png)

</div>

</div>


### Parameters


### path: str | _required_ _positional_

Path to a file.

For more details, see the [Paths section](/reference/syntax/#paths).


### encoding: none, str | _named_

The encoding to read the file with.

If set to <span class="typ-key">`none`</span>, this function returns raw
bytes.

