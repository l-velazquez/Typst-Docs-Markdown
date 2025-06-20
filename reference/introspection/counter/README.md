
# Counter

Counts through pages, elements, and more.

With the counter function, you can access and modify counters for pages,
headings, figures, and more. Moreover, you can define custom counters
for other things you want to count.

Since counters change throughout the course of the document, their
current value is *contextual.* It is recommended to read the chapter on
[context](/reference/context/ "context") before continuing here.

## Accessing a counter

To access the raw value of a counter, we can use the
[`get`](/reference/introspection/counter/#definitions-get) function.
This function returns an [array](/reference/foundations/array/ "array"):
Counters can have multiple levels (in the case of headings for sections,
subsections, and so on), and each item in the array corresponds to one
level.

<div class="previewed-code">

    #set heading(numbering: "1.")

    = Introduction
    Raw value of heading counter is
    #context counter(heading).get()

<div class="preview">

![Preview](/assets/8ea552ce797fc8605c34df5e705f0e54.png)

</div>

</div>

## Displaying a counter

Often, we want to display the value of a counter in a more
human-readable way. To do that, we can call the
[`display`](/reference/introspection/counter/#definitions-display)
function on the counter. This function retrieves the current counter
value and formats it either with a provided or with an automatically
inferred [numbering](/reference/model/numbering/ "numbering").

<div class="previewed-code">

    #set heading(numbering: "1.")

    = Introduction
    Some text here.

    = Background
    The current value is: #context {
      counter(heading).display()
    }

    Or in roman numerals: #context {
      counter(heading).display("I")
    }

<div class="preview">

![Preview](/assets/ec4522eb5a753d79b343291aff636a88.png)

</div>

</div>

## Modifying a counter

To modify a counter, you can use the `step` and `update` methods:

- The `step` method increases the value of the counter by one. Because
  counters can have multiple levels , it optionally takes a `level`
  argument. If given, the counter steps at the given depth.

- The `update` method allows you to arbitrarily modify the counter. In
  its basic form, you give it an integer (or an array for multiple
  levels). For more flexibility, you can instead also give it a function
  that receives the current value and returns a new value.

The heading counter is stepped before the heading is displayed, so
`Analysis` gets the number seven even though the counter is at six after
the second update.

<div class="previewed-code">

    #set heading(numbering: "1.")

    = Introduction
    #counter(heading).step()

    = Background
    #counter(heading).update(3)
    #counter(heading).update(n => n * 2)

    = Analysis
    Let's skip 7.1.
    #counter(heading).step(level: 2)

    == Analysis
    Still at #context {
      counter(heading).display()
    }

<div class="preview">

![Preview](/assets/10e62abf96165699a2432049a18a6a40.png)

</div>

</div>

## Page counter

The page counter is special. It is automatically stepped at each
pagebreak. But like other counters, you can also step it manually. For
example, you could have Roman page numbers for your preface, then switch
to Arabic page numbers for your main content and reset the page counter
to one.

<div class="previewed-code">

    #set page(numbering: "(i)")

    = Preface
    The preface is numbered with
    roman numerals.

    #set page(numbering: "1 / 1")
    #counter(page).update(1)

    = Main text
    Here, the counter is reset to one.
    We also display both the current
    page and total number of pages in
    Arabic numbers.

<div class="preview">

![Preview](/assets/3c30a8aceea73d91286b71e31d456047.png)

</div>

</div>

## Custom counters

To define your own counter, call the `counter` function with a string as
a key. This key identifies the counter globally.

<div class="previewed-code">

    #let mine = counter("mycounter")
    #context mine.display() \
    #mine.step()
    #context mine.display() \
    #mine.update(c => c * 3)
    #context mine.display()

<div class="preview">

![Preview](/assets/b15cb3320af269d859e669c3cddd652.png)

</div>

</div>

## How to step

When you define and use a custom counter, in general, you should first
step the counter and then display it. This way, the stepping behaviour
of a counter can depend on the element it is stepped for. If you were
writing a counter for, let's say, theorems, your theorem's definition
would thus first include the counter step and only then display the
counter and the theorem's contents.

<div class="previewed-code">

    #let c = counter("theorem")
    #let theorem(it) = block[
      #c.step()
      *Theorem #context c.display():*
      #it
    ]

    #theorem[$1 = 1$]
    #theorem[$2 < 3$]

<div class="preview">

![Preview](/assets/69fe98ee7391fc895dbd81c85839a421.png)

</div>

</div>

The rationale behind this is best explained on the example of the
heading counter: An update to the heading counter depends on the
heading's level. By stepping directly before the heading, we can
correctly step from `1` to `1.1` when encountering a level 2 heading. If
we were to step after the heading, we wouldn't know what to step to.

Because counters should always be stepped before the elements they
count, they always start at zero. This way, they are at one for the
first display (which happens after the first step).

## Time travel

Counters can travel through time! You can find out the final value of
the counter before it is reached and even determine what the value was
at any particular location in the document.

<div class="previewed-code">

    #let mine = counter("mycounter")

    = Values
    #context [
      Value here: #mine.get() \
      At intro: #mine.at(<intro>) \
      Final value: #mine.final()
    ]

    #mine.update(n => n + 3)

    = Introduction <intro>
    #lorem(10)

    #mine.step()
    #mine.step()

<div class="preview">

![Preview](/assets/c287511a94ac2600d9b5fb0c93f18d83.png)

</div>

</div>

## Other kinds of state

The `counter` type is closely related to
[state](/reference/introspection/state/ "state") type. Read its
documentation for more details on state management in Typst and why it
doesn't just use normal variables for counters.


## counter

```
counter(
    str label selector location function
) -> counter
```
Create a new counter identified by a key.


#### Parameters


#### key: str, label, selector, location, function | _required_ _positional_

The key that identifies this counter.

- If it is a string, creates a custom counter that is only affected by
  manual updates,
- If it is the [`page`](/reference/layout/page/ "`page`") function,
  counts through pages,
- If it is a [selector](/reference/foundations/selector/ "selector"),
  counts through elements that matches with the selector. For example,
  - provide an element function: counts elements of that type,
  - provide a
    [<span class="typ-label">`<label>`</span>](/reference/foundations/label/):
    counts elements with that label.


## Definitions


### get

```
counter.get(
) -> int array
```
Retrieves the value of the counter at the current location. Always
returns an array of integers, even if the counter has just one number.

This is equivalent to
`counter`<span class="typ-punct">`.`</span><span class="typ-func">`at`</span><span class="typ-punct">`(`</span><span class="typ-func">`here`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span><span class="typ-punct">`)`</span>.


##### Parameters


### display

```
counter.display(
    auto str function
    both: bool
) -> any
```
Displays the current value of the counter with a numbering and returns
the formatted output.


##### Parameters


##### numbering: auto, str, function | _positional_

A [numbering pattern or a function](/reference/model/numbering/), which
specifies how to display the counter. If given a function, that function
receives each number of the counter as a separate argument. If the
amount of numbers varies, e.g. for the heading argument, you can use an
[argument sink](/reference/foundations/arguments/).

If this is omitted or set to <span class="typ-key">`auto`</span>,
displays the counter with the numbering style for the counted element or
with the pattern <span class="typ-str">`"1.1"`</span> if no such style
exists.


##### both: bool | _named_

If enabled, displays the current and final top-level count together.
Both can be styled through a single numbering pattern. This is used by
the page numbering property to display the current and total number of
pages when a pattern like <span class="typ-str">`"1 / 1"`</span> is
given.


### at

```
counter.at(
    label selector location function
) -> int array
```
Retrieves the value of the counter at the given location. Always returns
an array of integers, even if the counter has just one number.

The `selector` must match exactly one element in the document. The most
useful kinds of selectors for this are
[labels](/reference/foundations/label/) and
[locations](/reference/introspection/location/).


##### Parameters


##### selector: label, selector, location, function | _required_ _positional_

The place at which the counter's value should be retrieved.


### final

```
counter.final(
) -> int array
```
Retrieves the value of the counter at the end of the document. Always
returns an array of integers, even if the counter has just one number.


##### Parameters


### step

```
counter.step(
    level: int
) -> content
```
Increases the value of the counter by one.

The update will be in effect at the position where the returned content
is inserted into the document. If you don't put the output into the
document, nothing happens! This would be the case, for example, if you
write
<span class="typ-key">`let`</span>` _ `<span class="typ-op">`=`</span>` `<span class="typ-func">`counter`</span><span class="typ-punct">`(`</span>`page`<span class="typ-punct">`)`</span><span class="typ-punct">`.`</span><span class="typ-func">`step`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span>.
Counter updates are always applied in layout order and in that case,
Typst wouldn't know when to step the counter.


##### Parameters


##### level: int | _named_

The depth at which to step the counter. Defaults to
<span class="typ-num">`1`</span>.


### update

```
counter.update(
    int array function
) -> content
```
Updates the value of the counter.

Just like with `step`, the update only occurs if you put the resulting
content into the document.


##### Parameters


##### update: int, array, function | _required_ _positional_

If given an integer or array of integers, sets the counter to that
value. If given a function, that function receives the previous counter
value (with each number as a separate argument) and has to return the
new value (integer or array).

