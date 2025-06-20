
# Arguments

Captured arguments to a function.

## Argument Sinks

Like built-in functions, custom functions can also take a variable
number of arguments. You can specify an *argument sink* which collects
all excess arguments as `..sink`. The resulting `sink` value is of the
`arguments` type. It exposes methods to access the positional and named
arguments.

<div class="previewed-code">

    #let format(title, ..authors) = {
      let by = authors
        .pos()
        .join(", ", last: " and ")

      [*#title* \ _Written by #by;_]
    }

    #format("ArtosFlow", "Jane", "Joe")

<div class="preview">

![Preview](/assets/d6ce7ebd806b82775abf2d566f8c412.png)

</div>

</div>

## Spreading

Inversely to an argument sink, you can *spread* arguments, arrays and
dictionaries into a function call with the `..spread` operator:

<div class="previewed-code">

    #let array = (2, 3, 5)
    #calc.min(..array)
    #let dict = (fill: blue)
    #text(..dict)[Hello]

<div class="preview">

![Preview](/assets/91c9aab47f6ac6ae8183c670c0a9cc09.png)

</div>

</div>


## arguments

```
arguments(
    any
) -> arguments
```
Construct spreadable arguments in place.

This function behaves like
<span class="typ-key">`let`</span>` `<span class="typ-func">`args`</span><span class="typ-punct">`(`</span><span class="typ-op">`..`</span>`sink`<span class="typ-punct">`)`</span>` `<span class="typ-op">`=`</span>` sink`.


#### Parameters


#### arguments: any | _required_ _positional_

The arguments to construct.


### Example

<div class="previewed-code">

    #let args = arguments(stroke: red, inset: 1em, [Body])
    #box(..args)

<div class="preview">

![Preview](/assets/25bccad3df7eaeaab4a645bea07090b2.png)

</div>

</div>


## Definitions


### at

```
arguments.at(
    int str
    default: any
) -> any
```
Returns the positional argument at the specified index, or the named
argument with the specified name.

If the key is an [integer](/reference/foundations/int/), this is
equivalent to first calling
[`pos`](/reference/foundations/arguments/#definitions-pos) and then
[`array.at`](/reference/foundations/array/#definitions-at "`array.at`").
If it is a [string](/reference/foundations/str/), this is equivalent to
first calling
[`named`](/reference/foundations/arguments/#definitions-named) and then
[`dictionary.at`](/reference/foundations/dictionary/#definitions-at "`dictionary.at`").


##### Parameters


##### key: int, str | _required_ _positional_

The index or name of the argument to get.


##### default: any | _named_

A default value to return if the key is invalid.


### pos

```
arguments.pos(
) -> array
```
Returns the captured positional arguments as an array.


##### Parameters


### named

```
arguments.named(
) -> dictionary
```
Returns the captured named arguments as a dictionary.


##### Parameters

