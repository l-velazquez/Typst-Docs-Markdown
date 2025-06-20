
# link

```
link(
    str label location dictionary
    content
) -> content
```
Links to a URL or a location in the document.

By default, links do not look any different from normal text. However,
you can easily apply a style of your choice with a show rule.

## Example

<div class="previewed-code">

    #show link: underline

    https://example.com \

    #link("https://example.com") \
    #link("https://example.com")[
      See example.com
    ]

<div class="preview">

![Preview](/assets/9817d02583b839b8c8cae2e2fc58ca7e.png)

</div>

</div>

## Hyphenation

If you enable hyphenation or justification, by default, it will not
apply to links to prevent unwanted hyphenation in URLs. You can opt out
of this default via
<span class="typ-key">`show`</span>` `<span class="typ-func">`link`</span><span class="typ-punct">`:`</span>` `<span class="typ-key">`set`</span>` `<span class="typ-func">`text`</span><span class="typ-punct">`(`</span>`hyphenate`<span class="typ-punct">`:`</span>` `<span class="typ-key">`true`</span><span class="typ-punct">`)`</span>.

## Syntax

This function also has dedicated syntax: Text that starts with `http://`
or `https://` is automatically turned into a link.


### Parameters


### dest: str, label, location, dictionary | _required_ _positional_

The destination the link points to.

- To link to web pages, `dest` should be a valid URL string. If the URL
  is in the `mailto:` or `tel:` scheme and the `body` parameter is
  omitted, the email address or phone number will be the link's body,
  without the scheme.

- To link to another part of the document, `dest` can take one of three
  forms:

  - A [label](/reference/foundations/label/ "label") attached to an
    element. If you also want automatic text for the link based on the
    element, consider using a [reference](/reference/model/ref/)
    instead.

  - A [`location`](/reference/introspection/location/ "`location`")
    (typically retrieved from
    [`here`](/reference/introspection/here/ "`here`"),
    [`locate`](/reference/introspection/locate/ "`locate`") or
    [`query`](/reference/introspection/query/ "`query`")).

  - A dictionary with a `page` key of type
    [integer](/reference/foundations/int/) and `x` and `y` coordinates
    of type [length](/reference/layout/length/ "length"). Pages are
    counted from one, and the coordinates are relative to the page's top
    left corner.


#### Example

<div class="previewed-code">

    = Introduction <intro>
    #link("mailto:hello@typst.app") \
    #link(<intro>)[Go to intro] \
    #link((page: 1, x: 0pt, y: 0pt))[
      Go to top
    ]

<div class="preview">

![Preview](/assets/afe2f0708d82d4ae0eb545a1b6f83c42.png)

</div>

</div>


### body: content | _required_ _positional_

The content that should become a link.

If `dest` is an URL string, the parameter can be omitted. In this case,
the URL will be shown as the link.

