
# Dictionary

A map from string keys to values.

You can construct a dictionary by enclosing comma-separated `key: value`
pairs in parentheses. The values do not have to be of the same type.
Since empty parentheses already yield an empty array, you have to use
the special `(:)` syntax to create an empty dictionary.

A dictionary is conceptually similar to an array, but it is indexed by
strings instead of integers. You can access and create dictionary
entries with the `.at()` method. If you know the key statically, you can
alternatively use [field access notation](/reference/scripting/#fields)
(`.key`) to access the value. Dictionaries can be added with the `+`
operator and [joined together](/reference/scripting/#blocks). To check
whether a key is present in the dictionary, use the `in` keyword.

You can iterate over the pairs in a dictionary using a [for
loop](/reference/scripting/#loops). This will iterate in the order the
pairs were inserted / declared.

## Example

<div class="previewed-code">

    #let dict = (
      name: "Typst",
      born: 2019,
    )

    #dict.name \
    #(dict.launch = 20)
    #dict.len() \
    #dict.keys() \
    #dict.values() \
    #dict.at("born") \
    #dict.insert("city", "Berlin ")
    #("name" in dict)

<div class="preview">

![Preview](/assets/d41c8842a0cf678555c4f98536841783.png)

</div>

</div>


## dictionary

```
dictionary(
    module
) -> dictionary
```
Converts a value into a dictionary.

Note that this function is only intended for conversion of a
dictionary-like value to a dictionary, not for creation of a dictionary
from individual pairs. Use the dictionary syntax `(key: value)` instead.


#### Parameters


#### value: module | _required_ _positional_

The value that should be converted to a dictionary.


### Example

<div class="previewed-code">

    #dictionary(sys).at("version")

<div class="preview">

![Preview](/assets/bebc0d67925f97a933ee062710eb0cd0.png)

</div>

</div>


## Definitions


### len

```
dictionary.len(
) -> int
```
The number of pairs in the dictionary.


##### Parameters


### at

```
dictionary.at(
    str
    default: any
) -> any
```
Returns the value associated with the specified key in the dictionary.
May be used on the left-hand side of an assignment if the key is already
present in the dictionary. Returns the default value if the key is not
part of the dictionary or fails with an error if no default value was
specified.


##### Parameters


##### key: str | _required_ _positional_

The key at which to retrieve the item.


##### default: any | _named_

A default value to return if the key is not part of the dictionary.


### insert

```
dictionary.insert(
    str
    any
) -> 
```
Inserts a new pair into the dictionary. If the dictionary already
contains this key, the value is updated.


##### Parameters


##### key: str | _required_ _positional_

The key of the pair that should be inserted.


##### value: any | _required_ _positional_

The value of the pair that should be inserted.


### remove

```
dictionary.remove(
    str
    default: any
) -> any
```
Removes a pair from the dictionary by key and return the value.


##### Parameters


##### key: str | _required_ _positional_

The key of the pair to remove.


##### default: any | _named_

A default value to return if the key does not exist.


### keys

```
dictionary.keys(
) -> array
```
Returns the keys of the dictionary as an array in insertion order.


##### Parameters


### values

```
dictionary.values(
) -> array
```
Returns the values of the dictionary as an array in insertion order.


##### Parameters


### pairs

```
dictionary.pairs(
) -> array
```
Returns the keys and values of the dictionary as an array of pairs. Each
pair is represented as an array of length two.


##### Parameters

