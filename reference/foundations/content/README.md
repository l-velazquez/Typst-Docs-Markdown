
# Content

A piece of document content.

This type is at the heart of Typst. All markup you write and most
[functions](/reference/foundations/function/) you call produce content
values. You can create a content value by enclosing markup in square
brackets. This is also how you pass content to functions.

## Example

<div class="previewed-code">

    Type of *Hello!* is
    #type([*Hello!*])

<div class="preview">

![Preview](/assets/5f8a9e925db86201f749a5dfd49d2d6a.png)

</div>

</div>

Content can be added with the `+` operator, [joined
together](/reference/scripting/#blocks) and multiplied with integers.
Wherever content is expected, you can also pass a
[string](/reference/foundations/str/) or
<span class="typ-key">`none`</span>.

## Representation

Content consists of elements with fields. When constructing an element
with its *element function,* you provide these fields as arguments and
when you have a content value, you can access its fields with [field
access syntax](/reference/scripting/#field-access).

Some fields are required: These must be provided when constructing an
element and as a consequence, they are always available through field
access on content of that type. Required fields are marked as such in
the documentation.

Most fields are optional: Like required fields, they can be passed to
the element function to configure them for a single element. However,
these can also be configured with [set
rules](/reference/styling/#set-rules) to apply them to all elements
within a scope. Optional fields are only available with field access
syntax when they were explicitly passed to the element function, not
when they result from a set rule.

Each element has a default appearance. However, you can also completely
customize its appearance with a [show
rule](/reference/styling/#show-rules). The show rule is passed the
element. It can access the element's field and produce arbitrary content
from it.

In the web app, you can hover over a content variable to see exactly
which elements the content is composed of and what fields they have.
Alternatively, you can inspect the output of the
[`repr`](/reference/foundations/repr/ "`repr`") function.


## Definitions


### func

```
content.func(
) -> function
```
The content's element function. This function can be used to create the
element contained in this content. It can be used in set and show rules
for the element. Can be compared with global functions to check whether
you have a specific kind of element.


##### Parameters


### has

```
content.has(
    str
) -> bool
```
Whether the content has the specified field.


##### Parameters


##### field: str | _required_ _positional_

The field to look for.


### at

```
content.at(
    str
    default: any
) -> any
```
Access the specified field on the content. Returns the default value if
the field does not exist or fails with an error if no default value was
specified.


##### Parameters


##### field: str | _required_ _positional_

The field to access.


##### default: any | _named_

A default value to return if the field does not exist.


### fields

```
content.fields(
) -> dictionary
```
Returns the fields of this content.


##### Parameters


#### Example

<div class="previewed-code">

    #rect(
      width: 10cm,
      height: 10cm,
    ).fields()

<div class="preview">

![Preview](/assets/ccd95853027f57c192e348066aff8697.png)

</div>

</div>


### location

```
content.location(
) -> none location
```
The location of the content. This is only available on content returned
by [query](/reference/introspection/query/ "query") or provided by a
[show rule](/reference/styling/#show-rules), for other content it will
be <span class="typ-key">`none`</span>. The resulting location can be
used with [counters](/reference/introspection/counter/),
[state](/reference/introspection/state/ "state") and
[queries](/reference/introspection/query/).


##### Parameters

