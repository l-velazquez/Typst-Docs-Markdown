
# locate

```
locate(
    label selector location function
) -> location
```
Determines the location of an element in the document.

Takes a selector that must match exactly one element and returns that
element's [`location`](/reference/introspection/location/ "`location`").
This location can, in particular, be used to retrieve the physical
[`page`](/reference/introspection/location/#definitions-page) number and
[`position`](/reference/introspection/location/#definitions-position)
(page, x, y) for that element.

## Examples

Locating a specific element:

<div class="previewed-code">

    #context [
      Introduction is at: \
      #locate(<intro>).position()
    ]

    = Introduction <intro>

<div class="preview">

![Preview](/assets/7e2cf137b2fb2fb13cb96a5377cfe632.png)

</div>

</div>


### Parameters


### selector: label, selector, location, function | _required_ _positional_

A selector that should match exactly one element. This element will be
located.

Especially useful in combination with

- [`here`](/reference/introspection/here/ "`here`") to locate the
  current context,
- a [`location`](/reference/introspection/location/ "`location`")
  retrieved from some queried element via the
  [`location()`](/reference/foundations/content/#definitions-location)
  method on content.

