
# footnote

```
footnote(
    numbering: str function
    label content
) -> content
```
A footnote.

Includes additional remarks and references on the same page with
footnotes. A footnote will insert a superscript number that links to the
note at the bottom of the page. Notes are numbered sequentially
throughout your document and can break across multiple pages.

To customize the appearance of the entry in the footnote listing, see
[`footnote.entry`](/reference/model/footnote/#definitions-entry). The
footnote itself is realized as a normal superscript, so you can use a
set rule on the [`super`](/reference/text/super/ "`super`") function to
customize it. You can also apply a show rule to customize only the
footnote marker (superscript number) in the running text.

## Example

<div class="previewed-code">

    Check the docs for more details.
    #footnote[https://typst.app/docs]

<div class="preview">

![Preview](/assets/46ec759f820fc0e90ea67d6ce7b5b1a4.png)

</div>

</div>

The footnote automatically attaches itself to the preceding word, even
if there is a space before it in the markup. To force space, you can use
the string
<span class="typ-str">`#`</span><span class="typ-str">`" "`</span> or
explicit [horizontal spacing](/reference/layout/h/).

By giving a label to a footnote, you can have multiple references to it.

<div class="previewed-code">

    You can edit Typst documents online.
    #footnote[https://typst.app/app] <fn>
    Checkout Typst's website. @fn
    And the online app. #footnote(<fn>)

<div class="preview">

![Preview](/assets/c440921edaf4561cc5879a27a70e3c19.png)

</div>

</div>

*Note:* Set and show rules in the scope where `footnote` is called may
not apply to the footnote's content. See
[here](https://github.com/typst/typst/issues/1467#issuecomment-1588799440)
for more information.


### Parameters


### numbering: str, function | _named_

How to number footnotes.

By default, the footnote numbering continues throughout your document.
If you prefer per-page footnote numbering, you can reset the footnote
[counter](/reference/introspection/counter/ "counter") in the page
[header](/reference/layout/page/#parameters-header). In the future,
there might be a simpler way to achieve this.


#### Example

<div class="previewed-code">

    #set footnote(numbering: "*")

    Footnotes:
    #footnote[Star],
    #footnote[Dagger]

<div class="preview">

![Preview](/assets/9595205e7485a18731b013c2de7d09b.png)

</div>

</div>


### body: label, content | _required_ _positional_

The content to put into the footnote. Can also be the label of another
footnote this one should point to.


## Definitions


### entry

```
footnote.entry(
    content
    separator: content
    clearance: length
    gap: length
    indent: length
) -> content
```
An entry in a footnote list.

This function is not intended to be called directly. Instead, it is used
in set and show rules to customize footnote listings.


##### Parameters


##### note: content | _required_ _positional_

The footnote for this entry. Its location can be used to determine the
footnote counter state.


###### Example

<div class="previewed-code">

    #show footnote.entry: it => {
      let loc = it.note.location()
      numbering(
        "1: ",
        ..counter(footnote).at(loc),
      )
      it.note.body
    }

    Customized #footnote[Hello]
    listing #footnote[World! 🌏]

<div class="preview">

![Preview](/assets/a484d77b028ceac481e5e778e1f529ef.png)

</div>

</div>


##### separator: content | _named_

The separator between the document body and the footnote listing.


###### Example

<div class="previewed-code">

    #set footnote.entry(
      separator: repeat[.]
    )

    Testing a different separator.
    #footnote[
      Unconventional, but maybe
      not that bad?
    ]

<div class="preview">

![Preview](/assets/d8165b7e239fd7abba7e37be24cd8a87.png)

</div>

</div>


##### clearance: length | _named_

The amount of clearance between the document body and the separator.


###### Example

<div class="previewed-code">

    #set footnote.entry(clearance: 3em)

    Footnotes also need ...
    #footnote[
      ... some space to breathe.
    ]

<div class="preview">

![Preview](/assets/8c623ff98c6ccf436a5f43239994bfa9.png)

</div>

</div>


##### gap: length | _named_

The gap between footnote entries.


###### Example

<div class="previewed-code">

    #set footnote.entry(gap: 0.8em)

    Footnotes:
    #footnote[Spaced],
    #footnote[Apart]

<div class="preview">

![Preview](/assets/dec820ba95d4ecbfdb3ba2984410d61d.png)

</div>

</div>


##### indent: length | _named_

The indent of each footnote entry.


###### Example

<div class="previewed-code">

    #set footnote.entry(indent: 0em)

    Footnotes:
    #footnote[No],
    #footnote[Indent]

<div class="preview">

![Preview](/assets/fb3904fde8d00e917a2933d395967783.png)

</div>

</div>


#### Example

<div class="previewed-code">

    #show footnote.entry: set text(red)

    My footnote listing
    #footnote[It's down here]
    has red text!

<div class="preview">

![Preview](/assets/39070e2c8c085851bcd6e717c5eba257.png)

</div>

</div>

*Note:* Footnote entry properties must be uniform across each page run
(a page run is a sequence of pages without an explicit pagebreak in
between). For this reason, set and show rules for footnote entries
should be defined before any page content, typically at the very start
of the document.

