
# Bytes

A sequence of bytes.

This is conceptually similar to an array of
[integers](/reference/foundations/int/) between
<span class="typ-num">`0`</span> and <span class="typ-num">`255`</span>,
but represented much more efficiently. You can iterate over it using a
[for loop](/reference/scripting/#loops).

You can convert

- a [string](/reference/foundations/str/) or an
  [array](/reference/foundations/array/ "array") of integers to bytes
  with the [`bytes`](/reference/foundations/bytes/ "`bytes`")
  constructor
- bytes to a string with the
  [`str`](/reference/foundations/str/ "`str`") constructor, with UTF-8
  encoding
- bytes to an array of integers with the
  [`array`](/reference/foundations/array/ "`array`") constructor

When [reading](/reference/data-loading/read/) data from a file, you can
decide whether to load it as a string or as raw bytes.

<div class="previewed-code">

    #bytes((123, 160, 22, 0)) \
    #bytes("Hello 😃")

    #let data = read(
      "rhino.png",
      encoding: none,
    )

    // Magic bytes.
    #array(data.slice(0, 4)) \
    #str(data.slice(1, 4))

<div class="preview">

![Preview](/assets/b09b581605724240d910b1078dee72c3.png)

</div>

</div>


## bytes

```
bytes(
    str bytes array
) -> bytes
```
Converts a value to bytes.

- Strings are encoded in UTF-8.
- Arrays of integers between <span class="typ-num">`0`</span> and
  <span class="typ-num">`255`</span> are converted directly. The
  dedicated byte representation is much more efficient than the array
  representation and thus typically used for large byte buffers (e.g.
  image data).


#### Parameters


#### value: str, bytes, array | _required_ _positional_

The value that should be converted to bytes.


### Example

<div class="previewed-code">

    #bytes("Hello 😃") \
    #bytes((123, 160, 22, 0))

<div class="preview">

![Preview](/assets/3e57d56a31a67c32cc63aa7c5f84b707.png)

</div>

</div>


## Definitions


### len

```
bytes.len(
) -> int
```
The length in bytes.


##### Parameters


### at

```
bytes.at(
    int
    default: any
) -> any
```
Returns the byte at the specified index. Returns the default value if
the index is out of bounds or fails with an error if no default value
was specified.


##### Parameters


##### index: int | _required_ _positional_

The index at which to retrieve the byte.


##### default: any | _named_

A default value to return if the index is out of bounds.


### slice

```
bytes.slice(
    int
    none int
    count: int
) -> bytes
```
Extracts a subslice of the bytes. Fails with an error if the start or
end index is out of bounds.


##### Parameters


##### start: int | _required_ _positional_

The start index (inclusive).


##### end: none, int | _positional_

The end index (exclusive). If omitted, the whole slice until the end is
extracted.


##### count: int | _named_

The number of items to extract. This is equivalent to passing
`start + count` as the `end` position. Mutually exclusive with `end`.

