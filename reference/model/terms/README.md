
# terms

```
terms(
    tight: bool
    separator: content
    indent: length
    hanging-indent: length
    spacing: auto length
    content array
) -> content
```
A list of terms and their descriptions.

Displays a sequence of terms and their descriptions vertically. When the
descriptions span over multiple lines, they use hanging indent to
communicate the visual hierarchy.

## Example

<div class="previewed-code">

    / Ligature: A merged glyph.
    / Kerning: A spacing adjustment
      between two adjacent letters.

<div class="preview">

![Preview](/assets/aa37504d32456bf458b5c7eee362226b.png)

</div>

</div>

## Syntax

This function also has dedicated syntax: Starting a line with a slash,
followed by a term, a colon and a description creates a term list item.


### Parameters


### tight: bool | _named_

Defines the default
[spacing](/reference/model/terms/#parameters-spacing) of the term list.
If it is <span class="typ-key">`false`</span>, the items are spaced
apart with [paragraph
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

    / Fact: If a term list has a lot
      of text, and maybe other inline
      content, it should not be tight
      anymore.

    / Tip: To make it wide, simply
      insert a blank line between the
      items.

<div class="preview">

![Preview](/assets/b2492e47606096d9421d4cbd70fa57ee.png)

</div>

</div>


### separator: content | _named_

The separator between the item and the description.

If you want to just separate them with a certain amount of space, use
<span class="typ-func">`h`</span><span class="typ-punct">`(`</span><span class="typ-num">`2cm`</span><span class="typ-punct">`,`</span>` weak`<span class="typ-punct">`:`</span>` `<span class="typ-key">`true`</span><span class="typ-punct">`)`</span>
as the separator and replace <span class="typ-num">`2cm`</span> with
your desired amount of space.


#### Example

<div class="previewed-code">

    #set terms(separator: [: ])

    / Colon: A nice separator symbol.

<div class="preview">

![Preview](/assets/c72c9b94c23c97ff7d953b75fe9e645a.png)

</div>

</div>


### indent: length | _named_

The indentation of each item.


### hanging-indent: length | _named_

The hanging indent of the description.

This is in addition to the whole item's `indent`.


#### Example

<div class="previewed-code">

    #set terms(hanging-indent: 0pt)
    / Term: This term list does not
      make use of hanging indents.

<div class="preview">

![Preview](/assets/eb262b284ad3d89b51c01466a52f2be7.png)

</div>

</div>


### spacing: auto, length | _named_

The spacing between the items of the term list.

If set to <span class="typ-key">`auto`</span>, uses paragraph
[`leading`](/reference/model/par/#parameters-leading) for tight term
lists and paragraph
[`spacing`](/reference/model/par/#parameters-spacing) for wide
(non-tight) term lists.


### children: content, array | _required_ _positional_

The term list's children.

When using the term list syntax, adjacent items are automatically
collected into term lists, even through constructs like for loops.


#### Example

<div class="previewed-code">

    #for (year, product) in (
      "1978": "TeX",
      "1984": "LaTeX",
      "2019": "Typst",
    ) [/ #product: Born in #year.]

<div class="preview">

![Preview](/assets/c24bd033a8de4e4493468693f58d2549.png)

</div>

</div>


## Definitions


### item

```
terms.item(
    content
    content
) -> content
```
A term list item.


##### Parameters


##### term: content | _required_ _positional_

The term described by the list item.


##### description: content | _required_ _positional_

The description of the term.

