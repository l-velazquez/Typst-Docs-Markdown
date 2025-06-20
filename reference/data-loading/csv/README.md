
# csv

```
csv(
    str bytes
    delimiter: str
    row-type: type
) -> array
```
Reads structured data from a CSV file.

The CSV file will be read and parsed into a 2-dimensional array of
strings: Each row in the CSV file will be represented as an array of
strings, and all rows will be collected into a single array. Header rows
will not be stripped.

## Example

<div class="previewed-code">

    #let results = csv("example.csv")

    #table(
      columns: 2,
      [*Condition*], [*Result*],
      ..results.flatten(),
    )

<div class="preview">

![Preview](/assets/c192b88f7dd7e11a0cbe1419b109e999.png)

</div>

</div>


### Parameters


### source: str, bytes | _required_ _positional_

A [path](/reference/syntax/#paths) to a CSV file or raw CSV bytes.


### delimiter: str | _named_

The delimiter that separates columns in the CSV file. Must be a single
ASCII character.


### row-type: type | _named_

How to represent the file's rows.

- If set to `array`, each row is represented as a plain array of
  strings.
- If set to `dictionary`, each row is represented as a dictionary
  mapping from header keys to strings. This option only makes sense when
  a header row is present in the CSV file.


## Definitions


### decode

```
csv.decode(
    str bytes
    delimiter: str
    row-type: type
) -> array
```
Reads structured data from a CSV string/bytes.


##### Parameters


##### data: str, bytes | _required_ _positional_

CSV data.


##### delimiter: str | _named_

The delimiter that separates columns in the CSV file. Must be a single
ASCII character.


##### row-type: type | _named_

How to represent the file's rows.

- If set to `array`, each row is represented as a plain array of
  strings.
- If set to `dictionary`, each row is represented as a dictionary
  mapping from header keys to strings. This option only makes sense when
  a header row is present in the CSV file.

