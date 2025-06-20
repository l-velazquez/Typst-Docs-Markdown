
# cbor

```
cbor(
    str bytes
) -> any
```
Reads structured data from a CBOR file.

The file must contain a valid CBOR serialization. Mappings will be
converted into Typst dictionaries, and sequences will be converted into
Typst arrays. Strings and booleans will be converted into the Typst
equivalents, null-values (`null`, `~` or empty \`\`) will be converted
into <span class="typ-key">`none`</span>, and numbers will be converted
to floats or integers depending on whether they are whole numbers.

Be aware that integers larger than 2<sup>63</sup>-1 will be converted to
floating point numbers, which may result in an approximative value.


### Parameters


### source: str, bytes | _required_ _positional_

A [path](/reference/syntax/#paths) to a CBOR file or raw CBOR bytes.


## Definitions


### decode

```
cbor.decode(
    bytes
) -> any
```
Reads structured data from CBOR bytes.


##### Parameters


##### data: bytes | _required_ _positional_

CBOR data.


### encode

```
cbor.encode(
    any
) -> bytes
```
Encode structured data into CBOR bytes.


##### Parameters


##### value: any | _required_ _positional_

Value to be encoded.

