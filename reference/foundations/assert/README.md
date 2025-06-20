
# assert

```
assert(
    bool
    message: str
) -> 
```
Ensures that a condition is fulfilled.

Fails with an error if the condition is not fulfilled. Does not produce
any output in the document.

If you wish to test equality between two values, see
[`assert.eq`](/reference/foundations/assert/#definitions-eq) and
[`assert.ne`](/reference/foundations/assert/#definitions-ne).

## Example

    #assert(1 < 2, message: "math broke")


### Parameters


### condition: bool | _required_ _positional_

The condition that must be true for the assertion to pass.


### message: str | _named_

The error message when the assertion fails.


## Definitions


### eq

```
assert.eq(
    any
    any
    message: str
) -> 
```
Ensures that two values are equal.

Fails with an error if the first value is not equal to the second. Does
not produce any output in the document.


##### Parameters


##### left: any | _required_ _positional_

The first value to compare.


##### right: any | _required_ _positional_

The second value to compare.


##### message: str | _named_

An optional message to display on error instead of the representations
of the compared values.


#### Example

    #assert.eq(10, 10)


### ne

```
assert.ne(
    any
    any
    message: str
) -> 
```
Ensures that two values are not equal.

Fails with an error if the first value is equal to the second. Does not
produce any output in the document.


##### Parameters


##### left: any | _required_ _positional_

The first value to compare.


##### right: any | _required_ _positional_

The second value to compare.


##### message: str | _named_

An optional message to display on error instead of the representations
of the compared values.


#### Example

    #assert.ne(3, 4)

