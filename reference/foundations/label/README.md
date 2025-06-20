
# Label

A label for an element.

Inserting a label into content attaches it to the closest preceding
element that is not a space. The preceding element must be in the same
scope as the label, which means that
`Hello `<span class="typ-punct">`#`</span><span class="typ-punct">`[`</span><span class="typ-label">`<label>`</span><span class="typ-punct">`]`</span>,
for instance, wouldn't work.

A labelled element can be [referenced](/reference/model/ref/),
[queried](/reference/introspection/query/) for, and
[styled](/reference/styling/) through its label.

Once constructed, you can get the name of a label using
[`str`](/reference/foundations/str/#constructor).

## Example

<div class="previewed-code">

    #show <a>: set text(blue)
    #show label("b"): set text(red)

    = Heading <a>
    *Strong* #label("b")

<div class="preview">

![Preview](/assets/97765723d8aff99a5c36e2fcda86a09f.png)

</div>

</div>

## Syntax

This function also has dedicated syntax: You can create a label by
enclosing its name in angle brackets. This works both in markup and
code. A label's name can contain letters, numbers, `_`, `-`, `:`, and
`.`.

Note that there is a syntactical difference when using the dedicated
syntax for this function. In the code below, the
<span class="typ-label">`<a>`</span> terminates the heading and thus
attaches to the heading itself, whereas the
<span class="typ-func">`#`</span><span class="typ-func">`label`</span><span class="typ-punct">`(`</span><span class="typ-str">`"b"`</span><span class="typ-punct">`)`</span>
is part of the heading and thus attaches to the heading's text.

    // Equivalent to `#heading[Introduction] <a>`.
    = Introduction <a>

    // Equivalent to `#heading[Conclusion #label("b")]`.
    = Conclusion #label("b")

Currently, labels can only be attached to elements in markup mode, not
in code mode. This might change in the future.


## label

```
label(
    str
) -> label
```
Creates a label from a string.


#### Parameters


#### name: str | _required_ _positional_

The name of the label.


## Definitions

