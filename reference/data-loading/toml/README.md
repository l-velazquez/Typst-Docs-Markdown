
# toml

```
toml(
    str bytes
) -> any
```
Reads structured data from a TOML file.

The file must contain a valid TOML table. TOML tables will be converted
into Typst dictionaries, and TOML arrays will be converted into Typst
arrays. Strings, booleans and datetimes will be converted into the Typst
equivalents and numbers will be converted to floats or integers
depending on whether they are whole numbers.

The TOML file in the example consists of a table with the keys `title`,
`version`, and `authors`.

## Example

<div class="previewed-code">

    #let details = toml("details.toml")

    Title: #details.title \
    Version: #details.version \
    Authors: #(details.authors
      .join(", ", last: " and "))

<div class="preview">

![Preview](/assets/7f6e9fac705651fafb6c8a26435ab058.png)

</div>

</div>


### Parameters


### source: str, bytes | _required_ _positional_

A [path](/reference/syntax/#paths) to a TOML file or raw TOML bytes.


## Definitions


### decode

```
toml.decode(
    str bytes
) -> any
```
Reads structured data from a TOML string/bytes.


##### Parameters


##### data: str, bytes | _required_ _positional_

TOML data.


### encode

```
toml.encode(
    any
    pretty: bool
) -> str
```
Encodes structured data into a TOML string.


##### Parameters


##### value: any | _required_ _positional_

Value to be encoded.


##### pretty: bool | _named_

Whether to pretty-print the resulting TOML.

