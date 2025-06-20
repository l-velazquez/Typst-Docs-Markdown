
# bibliography

```
bibliography(
    str bytes array
    title: none auto content
    full: bool
    style: str bytes
) -> content
```
A bibliography / reference listing.

You can create a new bibliography by calling this function with a path
to a bibliography file in either one of two formats:

- A Hayagriva `.yaml`/`.yml` file. Hayagriva is a new bibliography file
  format designed for use with Typst. Visit its
  [documentation](https://github.com/typst/hayagriva/blob/main/docs/file-format.md)
  for more details.
- A BibLaTeX `.bib` file.

As soon as you add a bibliography somewhere in your document, you can
start citing things with reference syntax
(<span class="typ-ref">`@key`</span>) or explicit calls to the
[citation](/reference/model/cite/) function
(<span class="typ-func">`#`</span><span class="typ-func">`cite`</span><span class="typ-punct">`(`</span><span class="typ-label">`<key>`</span><span class="typ-punct">`)`</span>).
The bibliography will only show entries for works that were referenced
in the document.

## Styles

Typst offers a wide selection of built-in [citation and bibliography
styles](/reference/model/bibliography/#parameters-style). Beyond those,
you can add and use custom [CSL](https://citationstyles.org/) (Citation
Style Language) files. Wondering which style to use? Here are some good
defaults based on what discipline you're working in:

| Fields | Typical Styles |
|----|----|
| Engineering, IT | <span class="typ-str">`"ieee"`</span> |
| Psychology, Life Sciences | <span class="typ-str">`"apa"`</span> |
| Social sciences | <span class="typ-str">`"chicago-author-date"`</span> |
| Humanities | <span class="typ-str">`"mla"`</span>, <span class="typ-str">`"chicago-notes"`</span>, <span class="typ-str">`"harvard-cite-them-right"`</span> |
| Economics | <span class="typ-str">`"harvard-cite-them-right"`</span> |
| Physics | <span class="typ-str">`"american-physics-society"`</span> |

## Example

<div class="previewed-code">

    This was already noted by
    pirates long ago. @arrgh

    Multiple sources say ...
    @arrgh @netwok.

    #bibliography("works.bib")

<div class="preview">

![Preview](/assets/209df19e613387ac8475d78ce387afdf.png)

</div>

</div>


### Parameters


### sources: str, bytes, array | _required_ _positional_

One or multiple paths to or raw bytes for Hayagriva `.yaml` and/or
BibLaTeX `.bib` files.

This can be a:

- A path string to load a bibliography file from the given path. For
  more details about paths, see the [Paths
  section](/reference/syntax/#paths).
- Raw bytes from which the bibliography should be decoded.
- An array where each item is one of the above.


### title: none, auto, content | _named_

The title of the bibliography.

- When set to <span class="typ-key">`auto`</span>, an appropriate title
  for the [text language](/reference/text/text/#parameters-lang) will be
  used. This is the default.
- When set to <span class="typ-key">`none`</span>, the bibliography will
  not have a title.
- A custom title can be set by passing content.

The bibliography's heading will not be numbered by default, but you can
force it to be with a show-set rule:
<span class="typ-key">`show`</span>` `<span class="typ-func">`bibliography`</span><span class="typ-punct">`:`</span>` `<span class="typ-key">`set`</span>` `<span class="typ-func">`heading`</span><span class="typ-punct">`(`</span>`numbering`<span class="typ-punct">`:`</span>` `<span class="typ-str">`"1."`</span><span class="typ-punct">`)`</span>


### full: bool | _named_

Whether to include all works from the given bibliography files, even
those that weren't cited in the document.

To selectively add individual cited works without showing them, you can
also use the `cite` function with
[`form`](/reference/model/cite/#parameters-form) set to
<span class="typ-key">`none`</span>.


### style: str, bytes | _named_

The bibliography style.

This can be:

- A string with the name of one of the built-in styles (see below). Some
  of the styles listed below appear twice, once with their full name and
  once with a short alias.
- A path string to a [CSL file](https://citationstyles.org/). For more
  details about paths, see the [Paths
  section](/reference/syntax/#paths).
- Raw bytes from which a CSL style should be decoded.

