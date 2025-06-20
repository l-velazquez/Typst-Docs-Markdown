
# here

```
here(
) -> location
```
Provides the current location in the document.

You can think of `here` as a low-level building block that directly
extracts the current location from the active
[context](/reference/context/ "context"). Some other functions use it
internally: For instance,
`counter`<span class="typ-punct">`.`</span><span class="typ-func">`get`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span>
is equivalent to
`counter`<span class="typ-punct">`.`</span><span class="typ-func">`at`</span><span class="typ-punct">`(`</span><span class="typ-func">`here`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span><span class="typ-punct">`)`</span>.

Within show rules on
[locatable](/reference/introspection/location/#locatable) elements,
<span class="typ-func">`here`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span>
will match the location of the shown element.

If you want to display the current page number, refer to the
documentation of the
[`counter`](/reference/introspection/counter/ "`counter`") type. While
`here` can be used to determine the physical page number, typically you
want the logical page number that may, for instance, have been reset
after a preface.

## Examples

Determining the current position in the document in combination with the
[`position`](/reference/introspection/location/#definitions-position)
method:

<div class="previewed-code">

    #context [
      I am located at
      #here().position()
    ]

<div class="preview">

![Preview](/assets/e4fac373c1481ceacbb3fa948d38fa8b.png)

</div>

</div>

Running a [query](/reference/introspection/query/ "query") for elements
before the current position:

<div class="previewed-code">

    = Introduction
    = Background

    There are
    #context query(
      selector(heading).before(here())
    ).len()
    headings before me.

    = Conclusion

<div class="preview">

![Preview](/assets/e43587e9371906b123b86b92c0aa9ff0.png)

</div>

</div>

Refer to the [`selector`](/reference/foundations/selector/ "`selector`")
type for more details on before/after selectors.


### Parameters

