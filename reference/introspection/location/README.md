
# Location

Identifies an element in the document.

A location uniquely identifies an element in the document and lets you
access its absolute position on the pages. You can retrieve the current
location with the [`here`](/reference/introspection/here/ "`here`")
function and the location of a queried or shown element with the
[`location()`](/reference/foundations/content/#definitions-location)
method on content.

## Locatable elements

Currently, only a subset of element functions is locatable. Aside from
headings and figures, this includes equations, references, quotes and
all elements with an explicit label. As a result, you *can* query for
e.g. [`strong`](/reference/model/strong/ "`strong`") elements, but you
will find only those that have an explicit label attached to them. This
limitation will be resolved in the future.


## Definitions


### page

```
location.page(
) -> int
```
Returns the page number for this location.

Note that this does not return the value of the [page
counter](/reference/introspection/counter/) at this location, but the
true page number (starting from one).

If you want to know the value of the page counter, use
<span class="typ-func">`counter`</span><span class="typ-punct">`(`</span>`page`<span class="typ-punct">`)`</span><span class="typ-punct">`.`</span><span class="typ-func">`at`</span><span class="typ-punct">`(`</span>`loc`<span class="typ-punct">`)`</span>
instead.

Can be used with [`here`](/reference/introspection/here/ "`here`") to
retrieve the physical page position of the current context:


##### Parameters


#### Example

<div class="previewed-code">

    #context [
      I am located on
      page #here().page()
    ]

<div class="preview">

![Preview](/assets/d13a1548b2d47ac4cb904c3f62c9c993.png)

</div>

</div>


### position

```
location.position(
) -> dictionary
```
Returns a dictionary with the page number and the x, y position for this
location. The page number starts at one and the coordinates are measured
from the top-left of the page.

If you only need the page number, use `page()` instead as it allows
Typst to skip unnecessary work.


##### Parameters


### page-numbering

```
location.page-numbering(
) -> none str function
```
Returns the page numbering pattern of the page at this location. This
can be used when displaying the page counter in order to obtain the
local numbering. This is useful if you are building custom indices or
outlines.

If the page numbering is set to <span class="typ-key">`none`</span> at
that location, this function returns
<span class="typ-key">`none`</span>.


##### Parameters

