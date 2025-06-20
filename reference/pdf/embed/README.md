
# embed

```
pdf.embed(
    str
    bytes
    relationship: none str
    mime-type: none str
    description: none str
) -> content
```
A file that will be embedded into the output PDF.

This can be used to distribute additional files that are related to the
PDF within it. PDF readers will display the files in a file listing.

Some international standards use this mechanism to embed
machine-readable data (e.g., ZUGFeRD/Factur-X for invoices) that mirrors
the visual content of the PDF.

## Example

    #pdf.embed(
      "experiment.csv",
      relationship: "supplement",
      mime-type: "text/csv",
      description: "Raw Oxygen readings from the Arctic experiment",
    )

## Notes

- This element is ignored if exporting to a format other than PDF.
- File embeddings are not currently supported for PDF/A-2, even if the
  embedded file conforms to PDF/A-1 or PDF/A-2.


### Parameters


### path: str | _required_ _positional_

The [path](/reference/syntax/#paths) of the file to be embedded.

Must always be specified, but is only read from if no data is provided
in the following argument.


### data: bytes | _required_ _positional_

Raw file data, optionally.

If omitted, the data is read from the specified path.


### relationship: none, str | _named_

The relationship of the embedded file to the document.

Ignored if export doesn't target PDF/A-3.


### mime-type: none, str | _named_

The MIME type of the embedded file.


### description: none, str | _named_

A description for the embedded file.

