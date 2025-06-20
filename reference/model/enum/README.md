
# enum

```
enum(
    tight: bool
    numbering: str function
    start: auto int
    full: bool
    reversed: bool
    indent: length
    body-indent: length
    spacing: auto length
    number-align: alignment
    content array
) -> content
```
A numbered list.

Displays a sequence of items vertically and numbers them consecutively.

## Example

<div class="previewed-code">

    Automatically numbered:
    + Preparations
    + Analysis
    + Conclusions

    Manually numbered:
    2. What is the first step?
    5. I am confused.
    +  Moving on ...

    Multiple lines:
    + This enum item has multiple
      lines because the next line
      is indented.

    Function call.
    #enum[First][Second]

<div class="preview">

![Preview](/assets/1eb9c9d6644abdb5cd7fa5380e664268.png)

</div>

</div>

You can easily switch all your enumerations to a different numbering
style with a set rule.

<div class="previewed-code">

    #set enum(numbering: "a)")

    + Starting off ...
    + Don't forget step two

<div class="preview">

![Preview](/assets/8456faf1af030be46f7ff78c398b5533.png)

</div>

</div>

You can also use [`enum.item`](/reference/model/enum/#definitions-item)
to programmatically customize the number of each item in the
enumeration:

<div class="previewed-code">

    #enum(
      enum.item(1)[First step],
      enum.item(5)[Fifth step],
      enum.item(10)[Tenth step]
    )

<div class="preview">

![Preview](/assets/b9141b8d7ae4bfb17096d07196e54c30.png)

</div>

</div>

## Syntax

This functions also has dedicated syntax:

- Starting a line with a plus sign creates an automatically numbered
  enumeration item.
- Starting a line with a number followed by a dot creates an explicitly
  numbered enumeration item.

Enumeration items can contain multiple paragraphs and other block-level
content. All content that is indented more than an item's marker becomes
part of that item.


### Parameters


### tight: bool | _named_

Defines the default [spacing](/reference/model/enum/#parameters-spacing)
of the enumeration. If it is <span class="typ-key">`false`</span>, the
items are spaced apart with [paragraph
spacing](/reference/model/par/#parameters-spacing). If it is
<span class="typ-key">`true`</span>, they use [paragraph
leading](/reference/model/par/#parameters-leading) instead. This makes
the list more compact, which can look better if the items are short.

In markup mode, the value of this parameter is determined based on
whether items are separated with a blank line. If items directly follow
each other, this is set to <span class="typ-key">`true`</span>; if items
are separated by a blank line, this is set to
<span class="typ-key">`false`</span>. The markup-defined tightness
cannot be overridden with set rules.


#### Example

<div class="previewed-code">

    + If an enum has a lot of text, and
      maybe other inline content, it
      should not be tight anymore.

    + To make an enum wide, simply
      insert a blank line between the
      items.

<div class="preview">

![Preview](/assets/860a2d566023cbbb1db95dcf595b00d.png)

</div>

</div>


### numbering: str, function | _named_

How to number the enumeration. Accepts a [numbering pattern or
function](/reference/model/numbering/).

If the numbering pattern contains multiple counting symbols, they apply
to nested enums. If given a function, the function receives one argument
if `full` is <span class="typ-key">`false`</span> and multiple arguments
if `full` is <span class="typ-key">`true`</span>.


#### Example

<div class="previewed-code">

    #set enum(numbering: "1.a)")
    + Different
    + Numbering
      + Nested
      + Items
    + Style

    #set enum(numbering: n => super[#n])
    + Superscript
    + Numbering!

<div class="preview">

![Preview](/assets/6ffe69a133dcf921fd85cc0ea784dc6c.png)

</div>

</div>


### start: auto, int | _named_

Which number to start the enumeration with.


#### Example

<div class="previewed-code">

    #enum(
      start: 3,
      [Skipping],
      [Ahead],
    )

<div class="preview">

![Preview](/assets/36a68c2147cbb6bab67e17fdc428636a.png)

</div>

</div>


### full: bool | _named_

Whether to display the full numbering, including the numbers of all
parent enumerations.


#### Example

<div class="previewed-code">

    #set enum(numbering: "1.a)", full: true)
    + Cook
      + Heat water
      + Add ingredients
    + Eat

<div class="preview">

![Preview](/assets/79c2f47e7f76011c7feb16cb65816454.png)

</div>

</div>


### reversed: bool | _named_

Whether to reverse the numbering for this enumeration.


#### Example

<div class="previewed-code">

    #set enum(reversed: true)
    + Coffee
    + Tea
    + Milk

<div class="preview">

![Preview](/assets/5528dd706f7b5b1f480846f2534d812c.png)

</div>

</div>


### indent: length | _named_

The indentation of each item.


### body-indent: length | _named_

The space between the numbering and the body of each item.


### spacing: auto, length | _named_

The spacing between the items of the enumeration.

If set to <span class="typ-key">`auto`</span>, uses paragraph
[`leading`](/reference/model/par/#parameters-leading) for tight
enumerations and paragraph
[`spacing`](/reference/model/par/#parameters-spacing) for wide
(non-tight) enumerations.


### number-align: alignment | _named_

The alignment that enum numbers should have.

By default, this is set to `end `<span class="typ-op">`+`</span>` top`,
which aligns enum numbers towards end of the current text direction (in
left-to-right script, for example, this is the same as `right`) and at
the top of the line. The choice of `end` for horizontal alignment of
enum numbers is usually preferred over `start`, as numbers then grow
away from the text instead of towards it, avoiding certain visual
issues. This option lets you override this behaviour, however. (Also to
note is that the [unordered list](/reference/model/list/) uses a
different method for this, by giving the `marker` content an alignment
directly.).


#### Example

<div class="previewed-code">

    #set enum(number-align: start + bottom)

    Here are some powers of two:
    1. One
    2. Two
    4. Four
    8. Eight
    16. Sixteen
    32. Thirty two

<div class="preview">

![Preview](/assets/b3ecd497dafdcfac8a756e159ec2e2fc.png)

</div>

</div>


### children: content, array | _required_ _positional_

The numbered list's items.

When using the enum syntax, adjacent items are automatically collected
into enumerations, even through constructs like for loops.


#### Example

<div class="previewed-code">

    #for phase in (
       "Launch",
       "Orbit",
       "Descent",
    ) [+ #phase]

<div class="preview">

![Preview](/assets/f616921cf92bf200c0c7ed5c12d99ff1.png)

</div>

</div>


## Definitions


### item

```
enum.item(
    none int
    content
) -> content
```
An enumeration item.


##### Parameters


##### number: none, int | _positional_

The item's number.


##### body: content | _required_ _positional_

The item's body.

