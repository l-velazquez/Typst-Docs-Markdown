
# Selector

A filter for selecting elements within the document.

You can construct a selector in the following ways:

- you can use an element
  [function](/reference/foundations/function/ "function")
- you can filter for an element function with [specific
  fields](/reference/foundations/function/#definitions-where)
- you can use a [string](/reference/foundations/str/) or [regular
  expression](/reference/foundations/regex/)
- you can use a
  [<span class="typ-label">`<label>`</span>](/reference/foundations/label/)
- you can use a
  [`location`](/reference/introspection/location/ "`location`")
- call the [`selector`](/reference/foundations/selector/ "`selector`")
  constructor to convert any of the above types into a selector value
  and use the methods below to refine it

Selectors are used to [apply styling
rules](/reference/styling/#show-rules) to elements. You can also use
selectors to [query](/reference/introspection/query/ "query") the
document for certain types of elements.

Furthermore, you can pass a selector to several of Typst's built-in
functions to configure their behaviour. One such example is the
[outline](/reference/model/outline/ "outline") where it can be used to
change which elements are listed within the outline.

Multiple selectors can be combined using the methods shown below.
However, not all kinds of selectors are supported in all places, at the
moment.

## Example

<div class="previewed-code">

    #context query(
      heading.where(level: 1)
        .or(heading.where(level: 2))
    )

    = This will be found
    == So will this
    === But this will not.

<div class="preview">

![Preview](/assets/496fb688b3f52c8190d084ec07b2c611.png)

</div>

</div>


## selector

```
selector(
    str regex label selector location function
) -> selector
```
Turns a value into a selector. The following values are accepted:

- An element function like a `heading` or `figure`.
- A <span class="typ-label">`<label>`</span>.
- A more complex selector like
  `heading`<span class="typ-punct">`.`</span><span class="typ-func">`where`</span><span class="typ-punct">`(`</span>`level`<span class="typ-punct">`:`</span>` `<span class="typ-num">`1`</span><span class="typ-punct">`)`</span>.


#### Parameters


#### target: str, regex, label, selector, location, function | _required_ _positional_

Can be an element function like a `heading` or `figure`, a
<span class="typ-label">`<label>`</span> or a more complex selector like
`heading`<span class="typ-punct">`.`</span><span class="typ-func">`where`</span><span class="typ-punct">`(`</span>`level`<span class="typ-punct">`:`</span>` `<span class="typ-num">`1`</span><span class="typ-punct">`)`</span>.


## Definitions


### or

```
selector.or(
    str regex label selector location function
) -> selector
```
Selects all elements that match this or any of the other selectors.


##### Parameters


##### others: str, regex, label, selector, location, function | _required_ _positional_

The other selectors to match on.


### and

```
selector.and(
    str regex label selector location function
) -> selector
```
Selects all elements that match this and all of the other selectors.


##### Parameters


##### others: str, regex, label, selector, location, function | _required_ _positional_

The other selectors to match on.


### before

```
selector.before(
    label selector location function
    inclusive: bool
) -> selector
```
Returns a modified selector that will only match elements that occur
before the first match of `end`.


##### Parameters


##### end: label, selector, location, function | _required_ _positional_

The original selection will end at the first match of `end`.


##### inclusive: bool | _named_

Whether `end` itself should match or not. This is only relevant if both
selectors match the same type of element. Defaults to
<span class="typ-key">`true`</span>.


### after

```
selector.after(
    label selector location function
    inclusive: bool
) -> selector
```
Returns a modified selector that will only match elements that occur
after the first match of `start`.


##### Parameters


##### start: label, selector, location, function | _required_ _positional_

The original selection will start at the first match of `start`.


##### inclusive: bool | _named_

Whether `start` itself should match or not. This is only relevant if
both selectors match the same type of element. Defaults to
<span class="typ-key">`true`</span>.

