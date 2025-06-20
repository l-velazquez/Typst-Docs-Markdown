
# cite

```
cite(
    label
    supplement: none content
    form: none str
    style: auto str bytes
) -> content
```
Cite a work from the bibliography.

Before you starting citing, you need to add a
[bibliography](/reference/model/bibliography/ "bibliography") somewhere
in your document.

## Example

<div class="previewed-code">

    This was already noted by
    pirates long ago. @arrgh

    Multiple sources say ...
    @arrgh @netwok.

    You can also call `cite`
    explicitly. #cite(<arrgh>)

    #bibliography("works.bib")

<div class="preview">

![Preview](/assets/55e96c2ce29d5004db05ce402b9d7f16.png)

</div>

</div>

If your source name contains certain characters such as slashes, which
are not recognized by the `<>` syntax, you can explicitly call `label`
instead.

    Computer Modern is an example of a modernist serif typeface.
    #cite(label("DBLP:books/lib/Knuth86a")).

## Syntax

This function indirectly has dedicated syntax.
[References](/reference/model/ref/) can be used to cite works from the
bibliography. The label then corresponds to the citation key.


### Parameters


### key: label | _required_ _positional_

The citation key that identifies the entry in the bibliography that
shall be cited, as a label.


#### Example

<div class="previewed-code">

    // All the same
    @netwok \
    #cite(<netwok>) \
    #cite(label("netwok"))

<div class="preview">

![Preview](/assets/7f2bf55bb64a9e53f205533aff50ef8e.png)

</div>

</div>


### supplement: none, content | _named_

A supplement for the citation such as page or chapter number.

In reference syntax, the supplement can be added in square brackets:


#### Example

<div class="previewed-code">

    This has been proven. @distress[p.~7]

    #bibliography("works.bib")

<div class="preview">

![Preview](/assets/c89f5ad2321ecda4146b0ab593e62aab.png)

</div>

</div>


### form: none, str | _named_

The kind of citation to produce. Different forms are useful in different
scenarios: A normal citation is useful as a source at the end of a
sentence, while a "prose" citation is more suitable for inclusion in the
flow of text.

If set to <span class="typ-key">`none`</span>, the cited work is
included in the bibliography, but nothing will be displayed.


#### Example

<div class="previewed-code">

    #cite(<netwok>, form: "prose")
    show the outsized effects of
    pirate life on the human psyche.

<div class="preview">

![Preview](/assets/c426a6cd0fd21f3d6429a380072c7fac.png)

</div>

</div>


### style: auto, str, bytes | _named_

The citation style.

This can be:

- <span class="typ-key">`auto`</span> to automatically use the
  [bibliography's
  style](/reference/model/bibliography/#parameters-style) for citations.
- A string with the name of one of the built-in styles (see below). Some
  of the styles listed below appear twice, once with their full name and
  once with a short alias.
- A path string to a [CSL file](https://citationstyles.org/). For more
  details about paths, see the [Paths
  section](/reference/syntax/#paths).
- Raw bytes from which a CSL style should be decoded.

