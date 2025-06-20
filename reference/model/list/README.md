
# list

```
list(
    tight: bool
    marker: content array function
    indent: length
    body-indent: length
    spacing: auto length
    content
) -> content
```
A bullet list.

Displays a sequence of items vertically, with each item introduced by a
marker.

## Example

<div class="previewed-code">

    Normal list.
    - Text
    - Math
    - Layout
    - ...

    Multiple lines.
    - This list item spans multiple
      lines because it is indented.

    Function call.
    #list(
      [Foundations],
      [Calculate],
      [Construct],
      [Data Loading],
    )

<div class="preview">

![Preview](/assets/74677de8cf5a4d31e8fa3289f72ef793.png)

</div>

</div>

## Syntax

This functions also has dedicated syntax: Start a line with a hyphen,
followed by a space to create a list item. A list item can contain
multiple paragraphs and other block-level content. All content that is
indented more than an item's marker becomes part of that item.


### Parameters


### tight: bool | _named_

Defines the default [spacing](/reference/model/list/#parameters-spacing)
of the list. If it is <span class="typ-key">`false`</span>, the items
are spaced apart with [paragraph
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

    - If a list has a lot of text, and
      maybe other inline content, it
      should not be tight anymore.

    - To make a list wide, simply insert
      a blank line between the items.

<div class="preview">

![Preview](/assets/e0550f184e59c73e3e6754be9bf20509.png)

</div>

</div>


### marker: content, array, function | _named_

The marker which introduces each item.

Instead of plain content, you can also pass an array with multiple
markers that should be used for nested lists. If the list nesting depth
exceeds the number of markers, the markers are cycled. For total
control, you may pass a function that maps the list's nesting depth
(starting from <span class="typ-num">`0`</span>) to a desired marker.


#### Example

<div class="previewed-code">

    #set list(marker: [--])
    - A more classic list
    - With en-dashes

    #set list(marker: ([•], [--]))
    - Top-level
      - Nested
      - Items
    - Items

<div class="preview">

![Preview](/assets/ac615939521f18810e441de210d068b5.png)

</div>

</div>


### indent: length | _named_

The indent of each item.


### body-indent: length | _named_

The spacing between the marker and the body of each item.


### spacing: auto, length | _named_

The spacing between the items of the list.

If set to <span class="typ-key">`auto`</span>, uses paragraph
[`leading`](/reference/model/par/#parameters-leading) for tight lists
and paragraph [`spacing`](/reference/model/par/#parameters-spacing) for
wide (non-tight) lists.


### children: content | _required_ _positional_

The bullet list's children.

When using the list syntax, adjacent items are automatically collected
into lists, even through constructs like for loops.


#### Example

<div class="previewed-code">

    #for letter in "ABC" [
      - Letter #letter
    ]

<div class="preview">

![Preview](/assets/b1cb6d05790b8d83af9497216eea34d3.png)

</div>

</div>


## Definitions


### item

```
list.item(
    content
) -> content
```
A bullet list item.


##### Parameters


##### body: content | _required_ _positional_

The item's body.

