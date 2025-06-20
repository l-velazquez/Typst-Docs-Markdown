
# document

```
document(
    title: none content
    author: str array
    description: none content
    keywords: str array
    date: none auto datetime
) -> content
```
The root element of a document and its metadata.

All documents are automatically wrapped in a `document` element. You
cannot create a document element yourself. This function is only used
with [set rules](/reference/styling/#set-rules) to specify document
metadata. Such a set rule must not occur inside of any layout container.

<div class="previewed-code">

    #set document(title: [Hello])

    This has no visible output, but
    embeds metadata into the PDF!

<div class="preview">

![Preview](/assets/83e478c245ceb459ebe50983447ca754.png)

</div>

</div>

Note that metadata set with this function is not rendered within the
document. Instead, it is embedded in the compiled PDF file.


### Parameters


### title: none, content | _named_

The document's title. This is often rendered as the title of the PDF
viewer window.

While this can be arbitrary content, PDF viewers only support plain text
titles, so the conversion might be lossy.


### author: str, array | _named_

The document's authors.


### description: none, content | _named_

The document's description.


### keywords: str, array | _named_

The document's keywords.


### date: none, auto, datetime | _named_

The document's creation date.

If this is <span class="typ-key">`auto`</span> (default), Typst uses the
current date and time. Setting it to <span class="typ-key">`none`</span>
prevents Typst from embedding any creation date into the PDF metadata.

The year component must be at least zero in order to be embedded into a
PDF.

If you want to create byte-by-byte reproducible PDFs, set this to
something other than <span class="typ-key">`auto`</span>.

