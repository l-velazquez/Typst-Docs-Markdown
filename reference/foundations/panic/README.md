
# panic

```
panic(
    any
) -> 
```
Fails with an error.

Arguments are displayed to the user (not rendered in the document) as
strings, converting with `repr` if necessary.

## Example

The code below produces the error `panicked with: "this is wrong"`.

    #panic("this is wrong")


### Parameters


### values: any | _required_ _positional_

The values to panic with and display to the user.

