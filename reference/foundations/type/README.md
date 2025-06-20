
# Type

Describes a kind of value.

To style your document, you need to work with values of different kinds:
Lengths specifying the size of your elements, colors for your text and
shapes, and more. Typst categorizes these into clearly defined *types*
and tells you where it expects which type of value.

Apart from basic types for numeric values and
[typical](/reference/foundations/int/)
[types](/reference/foundations/float/)
[known](/reference/foundations/str/)
[from](/reference/foundations/array/)
[programming](/reference/foundations/dictionary/) languages, Typst
provides a special type for
[*content.*](/reference/foundations/content/) A value of this type can
hold anything that you can enter into your document: Text, elements like
headings and shapes, and style information.

## Example

<div class="previewed-code">

    #let x = 10
    #if type(x) == int [
      #x is an integer!
    ] else [
      #x is another value...
    ]

    An image is of type
    #type(image("glacier.jpg")).

<div class="preview">

![Preview](/assets/7538c768430ee75e747b4f97560d4ecf.png)

</div>

</div>

The type of <span class="typ-num">`10`</span> is `int`. Now, what is the
type of `int` or even `type`?

<div class="previewed-code">

    #type(int) \
    #type(type)

<div class="preview">

![Preview](/assets/1ea220672ff0a816e76e846567e22fe0.png)

</div>

</div>

Unlike other types like `int`,
[none](/reference/foundations/none/ "none") and
[auto](/reference/foundations/auto/ "auto") do not have a name
representing them. To test if a value is one of these, compare your
value to them directly, e.g:

<div class="previewed-code">

    #let val = none
    #if val == none [
      Yep, it's none.
    ]

<div class="preview">

![Preview](/assets/9fe64b0d6307e76aa133e5f4f468d494.png)

</div>

</div>

Note that `type` will return
[`content`](/reference/foundations/content/ "`content`") for all
document elements. To programmatically determine which kind of content
you are dealing with, see
[`content.func`](/reference/foundations/content/#definitions-func "`content.func`").


## type

```
type(
    any
) -> type
```
Determines a value's type.


#### Parameters


#### value: any | _required_ _positional_

The value whose type's to determine.


### Example

<div class="previewed-code">

    #type(12) \
    #type(14.7) \
    #type("hello") \
    #type(<glacier>) \
    #type([Hi]) \
    #type(x => x + 1) \
    #type(type)

<div class="preview">

![Preview](/assets/3bff018780f2b4261ae9dc20c2e887a.png)

</div>

</div>


## Definitions

