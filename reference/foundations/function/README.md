
# Function

A mapping from argument values to a return value.

You can call a function by writing a comma-separated list of function
*arguments* enclosed in parentheses directly after the function name.
Additionally, you can pass any number of trailing content blocks
arguments to a function *after* the normal argument list. If the normal
argument list would become empty, it can be omitted. Typst supports
positional and named arguments. The former are identified by position
and type, while the latter are written as `name: value`.

Within math mode, function calls have special behaviour. See the [math
documentation](/reference/math/) for more details.

## Example

<div class="previewed-code">

    // Call a function.
    #list([A], [B])

    // Named arguments and trailing
    // content blocks.
    #enum(start: 2)[A][B]

    // Version without parentheses.
    #list[A][B]

<div class="preview">

![Preview](/assets/87cba5b2546c4d8134e4fbb8ab2e42e8.png)

</div>

</div>

Functions are a fundamental building block of Typst. Typst provides
functions for a variety of typesetting tasks. Moreover, the markup you
write is backed by functions and all styling happens through functions.
This reference lists all available functions and how you can use them.
Please also refer to the documentation about
[set](/reference/styling/#set-rules) and
[show](/reference/styling/#show-rules) rules to learn about additional
ways you can work with functions in Typst.

## Element functions

Some functions are associated with *elements* like
[headings](/reference/model/heading/) or
[tables](/reference/model/table/). When called, these create an element
of their respective kind. In contrast to normal functions, they can
further be used in [set rules](/reference/styling/#set-rules), [show
rules](/reference/styling/#show-rules), and
[selectors](/reference/foundations/selector/).

## Function scopes

Functions can hold related definitions in their own scope, similar to a
[module](/reference/scripting/#modules). Examples of this are
[`assert.eq`](/reference/foundations/assert/#definitions-eq) or
[`list.item`](/reference/model/list/#definitions-item). However, this
feature is currently only available for built-in functions.

## Defining functions

You can define your own function with a [let
binding](/reference/scripting/#bindings) that has a parameter list after
the binding's name. The parameter list can contain mandatory positional
parameters, named parameters with default values and [argument
sinks](/reference/foundations/arguments/).

The right-hand side of a function binding is the function body, which
can be a block or any other expression. It defines the function's return
value and can depend on the parameters. If the function body is a [code
block](/reference/scripting/#blocks), the return value is the result of
joining the values of each expression in the block.

Within a function body, the `return` keyword can be used to exit early
and optionally specify a return value. If no explicit return value is
given, the body evaluates to the result of joining all expressions
preceding the `return`.

Functions that don't return any meaningful value return
[`none`](/reference/foundations/none/ "`none`") instead. The return type
of such functions is not explicitly specified in the documentation. (An
example of this is
[`array.push`](/reference/foundations/array/#definitions-push "`array.push`")).

<div class="previewed-code">

    #let alert(body, fill: red) = {
      set text(white)
      set align(center)
      rect(
        fill: fill,
        inset: 8pt,
        radius: 4pt,
        [*Warning:\ #body*],
      )
    }

    #alert[
      Danger is imminent!
    ]

    #alert(fill: blue)[
      KEEP OFF TRACKS
    ]

<div class="preview">

![Preview](/assets/e7ac0ae1342dcd1b7bfc1dce40ec5bed.png)

</div>

</div>

## Importing functions

Functions can be imported from one file
([`module`](/reference/scripting/#modules)) into another using
<span class="typ-key">`import`</span>. For example, assume that we have
defined the `alert` function from the previous example in a file called
`foo.typ`. We can import it into another file by writing
<span class="typ-key">`import`</span>` `<span class="typ-str">`"foo.typ"`</span><span class="typ-punct">`:`</span>` alert`.

## Unnamed functions

You can also create an unnamed function without creating a binding by
specifying a parameter list followed by `=>` and the function body. If
your function has just one parameter, the parentheses around the
parameter list are optional. Unnamed functions are mainly useful for
show rules, but also for settable properties that take functions like
the page function's
[`footer`](/reference/layout/page/#parameters-footer) property.

<div class="previewed-code">

    #show "once?": it => [#it #it]
    once?

<div class="preview">

![Preview](/assets/c9779efb0fcc717fd4868ec6868bdcf9.png)

</div>

</div>

## Note on function purity

In Typst, all functions are *pure.* This means that for the same
arguments, they always return the same result. They cannot "remember"
things to produce another value when they are called a second time.

The only exception are built-in methods like
[`array.push(value)`](/reference/foundations/array/#definitions-push).
These can modify the values they are called on.


## Definitions


### with

```
function.with(
    any
) -> function
```
Returns a new function that has the given arguments pre-applied.


##### Parameters


##### arguments: any | _required_ _positional_

The arguments to apply to the function.


### where

```
function.where(
    any
) -> selector
```
Returns a selector that filters for elements belonging to this function
whose fields have the values of the given arguments.


##### Parameters


##### fields: any | _required_ _positional_

The fields to filter for.


#### Example

<div class="previewed-code">

    #show heading.where(level: 2): set text(blue)
    = Section
    == Subsection
    === Sub-subsection

<div class="preview">

![Preview](/assets/54e4780e95888ad47cba40e40c1d918a.png)

</div>

</div>

