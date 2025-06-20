
# ref

```
ref(
    label
    supplement: none auto content function
    form: str
) -> content
```
A reference to a label or bibliography.

Takes a label and cross-references it. There are two kind of references,
determined by its [`form`](/reference/model/ref/#parameters-form):
<span class="typ-str">`"normal"`</span> and
<span class="typ-str">`"page"`</span>.

The default, a <span class="typ-str">`"normal"`</span> reference,
produces a textual reference to a label. For example, a reference to a
heading will yield an appropriate string such as "Section 1" for a
reference to the first heading. The word "Section" depends on the
[`lang`](/reference/text/text/#parameters-lang) setting and is localized
accordingly. The references are also links to the respective element.
Reference syntax can also be used to
[cite](/reference/model/cite/ "cite") from a bibliography.

As the default form requires a supplement and numbering, the label must
be attached to a *referenceable element*. Referenceable elements include
[headings](/reference/model/heading/),
[figures](/reference/model/figure/),
[equations](/reference/math/equation/), and
[footnotes](/reference/model/footnote/). To create a custom
referenceable element like a theorem, you can create a figure of a
custom [`kind`](/reference/model/figure/#parameters-kind) and write a
show rule for it. In the future, there might be a more direct way to
define a custom referenceable element.

If you just want to link to a labelled element and not get an automatic
textual reference, consider using the
[`link`](/reference/model/link/ "`link`") function instead.

A <span class="typ-str">`"page"`</span> reference produces a page
reference to a label, displaying the page number at its location. You
can use the [page's
supplement](/reference/layout/page/#parameters-supplement) to modify the
text before the page number. Unlike a
<span class="typ-str">`"normal"`</span> reference, the label can be
attached to any element.

## Example

<div class="previewed-code">

    #set page(numbering: "1")
    #set heading(numbering: "1.")
    #set math.equation(numbering: "(1)")

    = Introduction <intro>
    Recent developments in
    typesetting software have
    rekindled hope in previously
    frustrated researchers. @distress
    As shown in @results (see
    #ref(<results>, form: "page")),
    we ...

    = Results <results>
    We discuss our approach in
    comparison with others.

    == Performance <perf>
    @slow demonstrates what slow
    software looks like.
    $ T(n) = O(2^n) $ <slow>

    #bibliography("works.bib")

<div class="preview">

![Preview](/assets/a792745ccec945a90763138d4e45762f.png)

</div>

</div>

## Syntax

This function also has dedicated syntax: A
<span class="typ-str">`"normal"`</span> reference to a label can be
created by typing an `@` followed by the name of the label (e.g.
<span class="typ-heading">`= Introduction`</span>` `<span class="typ-label">`<intro>`</span>
can be referenced by typing <span class="typ-ref">`@intro`</span>).

To customize the supplement, add content in square brackets after the
reference:
<span class="typ-ref">`@intro`<span class="typ-punct">`[`</span>`Chapter`<span class="typ-punct">`]`</span></span>.

## Customization

If you write a show rule for references, you can access the referenced
element through the `element` field of the reference. The `element` may
be <span class="typ-key">`none`</span> even if it exists if Typst hasn't
discovered it yet, so you always need to handle that case in your code.

<div class="previewed-code">

    #set heading(numbering: "1.")
    #set math.equation(numbering: "(1)")

    #show ref: it => {
      let eq = math.equation
      let el = it.element
      if el != none and el.func() == eq {
        // Override equation references.
        link(el.location(),numbering(
          el.numbering,
          ..counter(eq).at(el.location())
        ))
      } else {
        // Other references as usual.
        it
      }
    }

    = Beginnings <beginning>
    In @beginning we prove @pythagoras.
    $ a^2 + b^2 = c^2 $ <pythagoras>

<div class="preview">

![Preview](/assets/ff69119c08e1a5967e92f26ccad7e5ca.png)

</div>

</div>


### Parameters


### target: label | _required_ _positional_

The target label that should be referenced.

Can be a label that is defined in the document or, if the
[`form`](/reference/model/ref/#parameters-form) is set to `"normal"`, an
entry from the
[`bibliography`](/reference/model/bibliography/ "`bibliography`").


### supplement: none, auto, content, function | _named_

A supplement for the reference.

If the [`form`](/reference/model/ref/#parameters-form) is set to
<span class="typ-str">`"normal"`</span>:

- For references to headings or figures, this is added before the
  referenced number.
- For citations, this can be used to add a page number.

If the [`form`](/reference/model/ref/#parameters-form) is set to
<span class="typ-str">`"page"`</span>, then this is added before the
page number of the label referenced.

If a function is specified, it is passed the referenced element and
should return content.


#### Example

<div class="previewed-code">

    #set heading(numbering: "1.")
    #show ref.where(
      form: "normal"
    ): set ref(supplement: it => {
      if it.func() == heading {
        "Chapter"
      } else {
        "Thing"
      }
    })

    = Introduction <intro>
    In @intro, we see how to turn
    Sections into Chapters. And
    in @intro[Part], it is done
    manually.

<div class="preview">

![Preview](/assets/aa86f60f6632f6ef7a93b80a5a97c7d1.png)

</div>

</div>


### form: str | _named_

The kind of reference to produce.


#### Example

<div class="previewed-code">

    #set page(numbering: "1")

    Here <here> we are on
    #ref(<here>, form: "page").

<div class="preview">

![Preview](/assets/7c0b8deae09773dbb50f5ed89759c240.png)

</div>

</div>

