
# Array

A sequence of values.

You can construct an array by enclosing a comma-separated sequence of
values in parentheses. The values do not have to be of the same type.

You can access and update array items with the `.at()` method. Indices
are zero-based and negative indices wrap around to the end of the array.
You can iterate over an array using a [for
loop](/reference/scripting/#loops). Arrays can be added together with
the `+` operator, [joined together](/reference/scripting/#blocks) and
multiplied with integers.

**Note:** An array of length one needs a trailing comma, as in
<span class="typ-punct">`(`</span><span class="typ-num">`1`</span><span class="typ-punct">`,`</span><span class="typ-punct">`)`</span>.
This is to disambiguate from a simple parenthesized expressions like
<span class="typ-punct">`(`</span><span class="typ-num">`1`</span>` `<span class="typ-op">`+`</span>` `<span class="typ-num">`2`</span><span class="typ-punct">`)`</span>` `<span class="typ-op">`*`</span>` `<span class="typ-num">`3`</span>.
An empty array is written as
<span class="typ-punct">`(`</span><span class="typ-punct">`)`</span>.

## Example

<div class="previewed-code">

    #let values = (1, 7, 4, -3, 2)

    #values.at(0) \
    #(values.at(0) = 3)
    #values.at(-1) \
    #values.find(calc.even) \
    #values.filter(calc.odd) \
    #values.map(calc.abs) \
    #values.rev() \
    #(1, (2, 3)).flatten() \
    #(("A", "B", "C")
        .join(", ", last: " and "))

<div class="preview">

![Preview](/assets/b82dcffb69c678f6966654cb6a9894a3.png)

</div>

</div>


## array

```
array(
    bytes array version
) -> array
```
Converts a value to an array.

Note that this function is only intended for conversion of a
collection-like value to an array, not for creation of an array from
individual items. Use the array syntax `(1, 2, 3)` (or `(1,)` for a
single-element array) instead.


#### Parameters


#### value: bytes, array, version | _required_ _positional_

The value that should be converted to an array.


### Example

<div class="previewed-code">

    #let hi = "Hello 😃"
    #array(bytes(hi))

<div class="preview">

![Preview](/assets/5f88747ad7a056745bb4d94b9e4440e4.png)

</div>

</div>


## Definitions


### len

```
array.len(
) -> int
```
The number of values in the array.


##### Parameters


### first

```
array.first(
    default: any
) -> any
```
Returns the first item in the array. May be used on the left-hand side
an assignment. Returns the default value if the array is empty or fails
with an error is no default value was specified.


##### Parameters


##### default: any | _named_

A default value to return if the array is empty.


### last

```
array.last(
    default: any
) -> any
```
Returns the last item in the array. May be used on the left-hand side of
an assignment. Returns the default value if the array is empty or fails
with an error is no default value was specified.


##### Parameters


##### default: any | _named_

A default value to return if the array is empty.


### at

```
array.at(
    int
    default: any
) -> any
```
Returns the item at the specified index in the array. May be used on the
left-hand side of an assignment. Returns the default value if the index
is out of bounds or fails with an error if no default value was
specified.


##### Parameters


##### index: int | _required_ _positional_

The index at which to retrieve the item. If negative, indexes from the
back.


##### default: any | _named_

A default value to return if the index is out of bounds.


### push

```
array.push(
    any
) -> 
```
Adds a value to the end of the array.


##### Parameters


##### value: any | _required_ _positional_

The value to insert at the end of the array.


### pop

```
array.pop(
) -> any
```
Removes the last item from the array and returns it. Fails with an error
if the array is empty.


##### Parameters


### insert

```
array.insert(
    int
    any
) -> 
```
Inserts a value into the array at the specified index, shifting all
subsequent elements to the right. Fails with an error if the index is
out of bounds.

To replace an element of an array, use
[`at`](/reference/foundations/array/#definitions-at).


##### Parameters


##### index: int | _required_ _positional_

The index at which to insert the item. If negative, indexes from the
back.


##### value: any | _required_ _positional_

The value to insert into the array.


### remove

```
array.remove(
    int
    default: any
) -> any
```
Removes the value at the specified index from the array and return it.


##### Parameters


##### index: int | _required_ _positional_

The index at which to remove the item. If negative, indexes from the
back.


##### default: any | _named_

A default value to return if the index is out of bounds.


### slice

```
array.slice(
    int
    none int
    count: int
) -> array
```
Extracts a subslice of the array. Fails with an error if the start or
end index is out of bounds.


##### Parameters


##### start: int | _required_ _positional_

The start index (inclusive). If negative, indexes from the back.


##### end: none, int | _positional_

The end index (exclusive). If omitted, the whole slice until the end of
the array is extracted. If negative, indexes from the back.


##### count: int | _named_

The number of items to extract. This is equivalent to passing
`start + count` as the `end` position. Mutually exclusive with `end`.


### contains

```
array.contains(
    any
) -> bool
```
Whether the array contains the specified value.

This method also has dedicated syntax: You can write
<span class="typ-num">`2`</span>` `<span class="typ-key">`in`</span>` `<span class="typ-punct">`(`</span><span class="typ-num">`1`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`2`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`3`</span><span class="typ-punct">`)`</span>
instead of
<span class="typ-punct">`(`</span><span class="typ-num">`1`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`2`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`3`</span><span class="typ-punct">`)`</span><span class="typ-punct">`.`</span><span class="typ-func">`contains`</span><span class="typ-punct">`(`</span><span class="typ-num">`2`</span><span class="typ-punct">`)`</span>.


##### Parameters


##### value: any | _required_ _positional_

The value to search for.


### find

```
array.find(
    function
) -> any none
```
Searches for an item for which the given function returns
<span class="typ-key">`true`</span> and returns the first match or
<span class="typ-key">`none`</span> if there is no match.


##### Parameters


##### searcher: function | _required_ _positional_

The function to apply to each item. Must return a boolean.


### position

```
array.position(
    function
) -> none int
```
Searches for an item for which the given function returns
<span class="typ-key">`true`</span> and returns the index of the first
match or <span class="typ-key">`none`</span> if there is no match.


##### Parameters


##### searcher: function | _required_ _positional_

The function to apply to each item. Must return a boolean.


### range

```
array.range(
    int
    int
    step: int
) -> array
```
Create an array consisting of a sequence of numbers.

If you pass just one positional parameter, it is interpreted as the
`end` of the range. If you pass two, they describe the `start` and `end`
of the range.

This function is available both in the array function's scope and
globally.


##### Parameters


##### start: int | _positional_

The start of the range (inclusive).


##### end: int | _required_ _positional_

The end of the range (exclusive).


##### step: int | _named_

The distance between the generated numbers.


#### Example

<div class="previewed-code">

    #range(5) \
    #range(2, 5) \
    #range(20, step: 4) \
    #range(21, step: 4) \
    #range(5, 2, step: -1)

<div class="preview">

![Preview](/assets/ceb87963d025cafe69d4f502bb2cf46c.png)

</div>

</div>


### filter

```
array.filter(
    function
) -> array
```
Produces a new array with only the items from the original one for which
the given function returns true.


##### Parameters


##### test: function | _required_ _positional_

The function to apply to each item. Must return a boolean.


### map

```
array.map(
    function
) -> array
```
Produces a new array in which all items from the original one were
transformed with the given function.


##### Parameters


##### mapper: function | _required_ _positional_

The function to apply to each item.


### enumerate

```
array.enumerate(
    start: int
) -> array
```
Returns a new array with the values alongside their indices.

The returned array consists of `(index, value)` pairs in the form of
length-2 arrays. These can be
[destructured](/reference/scripting/#bindings) with a let binding or for
loop.


##### Parameters


##### start: int | _named_

The index returned for the first pair of the returned list.


### zip

```
array.zip(
    exact: bool
    array
) -> array
```
Zips the array with other arrays.

Returns an array of arrays, where the `i`th inner array contains all the
`i`th elements from each original array.

If the arrays to be zipped have different lengths, they are zipped up to
the last element of the shortest array and all remaining elements are
ignored.

This function is variadic, meaning that you can zip multiple arrays
together at once:
<span class="typ-punct">`(`</span><span class="typ-num">`1`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`2`</span><span class="typ-punct">`)`</span><span class="typ-punct">`.`</span><span class="typ-func">`zip`</span><span class="typ-punct">`(`</span><span class="typ-punct">`(`</span><span class="typ-str">`"A"`</span><span class="typ-punct">`,`</span>` `<span class="typ-str">`"B"`</span><span class="typ-punct">`)`</span><span class="typ-punct">`,`</span>` `<span class="typ-punct">`(`</span><span class="typ-num">`10`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`20`</span><span class="typ-punct">`)`</span><span class="typ-punct">`)`</span>
yields
<span class="typ-punct">`(`</span><span class="typ-punct">`(`</span><span class="typ-num">`1`</span><span class="typ-punct">`,`</span>` `<span class="typ-str">`"A"`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`10`</span><span class="typ-punct">`)`</span><span class="typ-punct">`,`</span>` `<span class="typ-punct">`(`</span><span class="typ-num">`2`</span><span class="typ-punct">`,`</span>` `<span class="typ-str">`"B"`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`20`</span><span class="typ-punct">`)`</span><span class="typ-punct">`)`</span>.


##### Parameters


##### exact: bool | _named_

Whether all arrays have to have the same length. For example,
<span class="typ-punct">`(`</span><span class="typ-num">`1`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`2`</span><span class="typ-punct">`)`</span><span class="typ-punct">`.`</span><span class="typ-func">`zip`</span><span class="typ-punct">`(`</span><span class="typ-punct">`(`</span><span class="typ-num">`1`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`2`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`3`</span><span class="typ-punct">`)`</span><span class="typ-punct">`,`</span>` exact`<span class="typ-punct">`:`</span>` `<span class="typ-key">`true`</span><span class="typ-punct">`)`</span>
produces an error.


##### others: array | _required_ _positional_

The arrays to zip with.


### fold

```
array.fold(
    any
    function
) -> any
```
Folds all items into a single value using an accumulator function.


##### Parameters


##### init: any | _required_ _positional_

The initial value to start with.


##### folder: function | _required_ _positional_

The folding function. Must have two parameters: One for the accumulated
value and one for an item.


### sum

```
array.sum(
    default: any
) -> any
```
Sums all items (works for all types that can be added).


##### Parameters


##### default: any | _named_

What to return if the array is empty. Must be set if the array can be
empty.


### product

```
array.product(
    default: any
) -> any
```
Calculates the product all items (works for all types that can be
multiplied).


##### Parameters


##### default: any | _named_

What to return if the array is empty. Must be set if the array can be
empty.


### any

```
array.any(
    function
) -> bool
```
Whether the given function returns <span class="typ-key">`true`</span>
for any item in the array.


##### Parameters


##### test: function | _required_ _positional_

The function to apply to each item. Must return a boolean.


### all

```
array.all(
    function
) -> bool
```
Whether the given function returns <span class="typ-key">`true`</span>
for all items in the array.


##### Parameters


##### test: function | _required_ _positional_

The function to apply to each item. Must return a boolean.


### flatten

```
array.flatten(
) -> array
```
Combine all nested arrays into a single flat one.


##### Parameters


### rev

```
array.rev(
) -> array
```
Return a new array with the same items, but in reverse order.


##### Parameters


### split

```
array.split(
    any
) -> array
```
Split the array at occurrences of the specified value.


##### Parameters


##### at: any | _required_ _positional_

The value to split at.


### join

```
array.join(
    any none
    last: any
) -> any
```
Combine all items in the array into one.


##### Parameters


##### separator: any, none | _positional_

A value to insert between each item of the array.


##### last: any | _named_

An alternative separator between the last two items.


### intersperse

```
array.intersperse(
    any
) -> array
```
Returns an array with a copy of the separator value placed between
adjacent elements.


##### Parameters


##### separator: any | _required_ _positional_

The value that will be placed between each adjacent element.


### chunks

```
array.chunks(
    int
    exact: bool
) -> array
```
Splits an array into non-overlapping chunks, starting at the beginning,
ending with a single remainder chunk.

All chunks but the last have `chunk-size` elements. If `exact` is set to
<span class="typ-key">`true`</span>, the remainder is dropped if it
contains less than `chunk-size` elements.


##### Parameters


##### chunk-size: int | _required_ _positional_

How many elements each chunk may at most contain.


##### exact: bool | _named_

Whether to keep the remainder if its size is less than `chunk-size`.


#### Example

<div class="previewed-code">

    #let array = (1, 2, 3, 4, 5, 6, 7, 8)
    #array.chunks(3) \
    #array.chunks(3, exact: true)

<div class="preview">

![Preview](/assets/35c1baf0f7902b3b48cc164333d55b.png)

</div>

</div>


### windows

```
array.windows(
    int
) -> array
```
Returns sliding windows of `window-size` elements over an array.

If the array length is less than `window-size`, this will return an
empty array.


##### Parameters


##### window-size: int | _required_ _positional_

How many elements each window will contain.


#### Example

<div class="previewed-code">

    #let array = (1, 2, 3, 4, 5, 6, 7, 8)
    #array.windows(5)

<div class="preview">

![Preview](/assets/19a732fa351d05f71c5f8ddfc73c2a3e.png)

</div>

</div>


### sorted

```
array.sorted(
    key: function
    by: function
) -> array
```
Return a sorted version of this array, optionally by a given key
function. The sorting algorithm used is stable.

Returns an error if two values could not be compared or if the key or
comparison function (if given) yields an error.

To sort according to multiple criteria at once, e.g. in case of equality
between some criteria, the key function can return an array. The results
are in lexicographic order.


##### Parameters


##### key: function | _named_

If given, applies this function to the elements in the array to
determine the keys to sort by.


##### by: function | _named_

If given, uses this function to compare elements in the array.

This function should return a boolean:
<span class="typ-key">`true`</span> indicates that the elements are in
order, while <span class="typ-key">`false`</span> indicates that they
should be swapped. To keep the sort stable, if the two elements are
equal, the function should return <span class="typ-key">`true`</span>.

If this function does not order the elements properly (e.g., by
returning <span class="typ-key">`false`</span> for both
<span class="typ-punct">`(`</span>`x`<span class="typ-punct">`,`</span>` y`<span class="typ-punct">`)`</span>
and
<span class="typ-punct">`(`</span>`y`<span class="typ-punct">`,`</span>` x`<span class="typ-punct">`)`</span>,
or for
<span class="typ-punct">`(`</span>`x`<span class="typ-punct">`,`</span>` x`<span class="typ-punct">`)`</span>),
the resulting array will be in unspecified order.

When used together with `key`, `by` will be passed the keys instead of
the elements.


###### Example

<div class="previewed-code">

    #(
      "sorted",
      "by",
      "decreasing",
      "length",
    ).sorted(
      key: s => s.len(),
      by: (l, r) => l >= r,
    )

<div class="preview">

![Preview](/assets/7dde7fb47ef53c8d8b1aa9991abdf508.png)

</div>

</div>


#### Example

<div class="previewed-code">

    #let array = (
      (a: 2, b: 4),
      (a: 1, b: 5),
      (a: 2, b: 3),
    )
    #array.sorted(key: it => (it.a, it.b))

<div class="preview">

![Preview](/assets/fe903cbcc2093647a0fabae43aaaaf52.png)

</div>

</div>


### dedup

```
array.dedup(
    key: function
) -> array
```
Deduplicates all items in the array.

Returns a new array with all duplicate items removed. Only the first
element of each duplicate is kept.


##### Parameters


##### key: function | _named_

If given, applies this function to the elements in the array to
determine the keys to deduplicate by.


#### Example

<div class="previewed-code">

    #(1, 1, 2, 3, 1).dedup()

<div class="preview">

![Preview](/assets/37c0a9dbb361b1e7aef5584fddbfa0d2.png)

</div>

</div>


### to-dict

```
array.to-dict(
) -> dictionary
```
Converts an array of pairs into a dictionary. The first value of each
pair is the key, the second the value.

If the same key occurs multiple times, the last value is selected.


##### Parameters


#### Example

<div class="previewed-code">

    #(
      ("apples", 2),
      ("peaches", 3),
      ("apples", 5),
    ).to-dict()

<div class="preview">

![Preview](/assets/2e6b8e445cf77edd022ddf968946479e.png)

</div>

</div>


### reduce

```
array.reduce(
    function
) -> any
```
Reduces the elements to a single one, by repeatedly applying a reducing
operation.

If the array is empty, returns <span class="typ-key">`none`</span>,
otherwise, returns the result of the reduction.

The reducing function is a closure with two arguments: an "accumulator",
and an element.

For arrays with at least one element, this is the same as
[`array.fold`](/reference/foundations/array/#definitions-fold "`array.fold`")
with the first element of the array as the initial accumulator value,
folding every subsequent element into it.


##### Parameters


##### reducer: function | _required_ _positional_

The reducing function. Must have two parameters: One for the accumulated
value and one for an item.

