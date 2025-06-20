# Version 0.10.0 (December 4, 2023)

## Bibliography management

- Added support for citation collapsing (e.g. `[1]-[3]` instead of
  `[1], [2], [3]`) if requested by a CSL style
- Fixed bug where an additional space would appear after a group of
  citations
- Fixed link show rules for links in the bibliography
- Fixed show-set rules on citations
- Fixed bibliography-related crashes that happened on some systems
- Corrected name of the GB/T 7714 family of styles from 7114 to 7714
- Fixed missing title in some bibliography styles
- Fixed printing of volumes in some styles
- Fixed delimiter order for contributors in some styles (e.g. APA)
- Fixed behavior of alphanumeric style
- Fixed multiple bugs with GB/T 7714 style
- Fixed escaping in Hayagriva values
- Fixed crashes with empty dates in Hayagriva files
- Fixed bug with spacing around math blocks
- Fixed title case formatting after verbatim text and apostrophes
- Page ranges in `.bib` files can now be arbitrary strings
- Multi-line values in `.bib` files are now parsed correctly
- Entry keys in `.bib` files now allow more characters
- Fixed error message for empty dates in `.bib` files
- Added support for years of lengths other than 4 without leading zeros
  in `.bib` files
- More LaTeX commands (e.g. for quotes) are now respected in `.bib`
  files

## Visualization

- Added support for [patterns](/reference/visualize/tiling/) as fills
  and strokes
- The `alpha` parameter of the
  [`components`](/reference/visualize/color/#definitions-components)
  function on colors is now a named parameter **(Breaking change)**
- Added support for the
  [Oklch](/reference/visualize/color/#definitions-oklch) color space
- Improved conversions between colors in different color spaces
- Removed restrictions on
  [Oklab](/reference/visualize/color/#definitions-oklab) chroma
  component
- Fixed [clipping](/reference/layout/block/#parameters-clip) on blocks
  and boxes without a stroke
- Fixed bug with [gradients](/reference/visualize/gradient/) on math
- Fixed bug with gradient rotation on text
- Fixed bug with gradient colors in PDF
- Fixed relative base of Oklab chroma ratios
- Fixed Oklab color negation

## Text and Layout

- CJK text can now be emphasized with the `*` and `_` syntax even when
  there are no spaces
- Added basic i18n for Greek and Estonian
- Improved default [figure caption
  separator](/reference/model/figure/#definitions-caption-separator) for
  Chinese, French, and Russian
- Changed default [figure
  supplement](/reference/model/figure/#parameters-supplement) for
  Russian to short form
- Fixed
  [CJK-Latin-spacing](/reference/text/text/#parameters-cjk-latin-spacing)
  before line breaks and in
  [`locate`](/reference/introspection/locate/ "`locate`") calls
- Fixed line breaking at the end of links

## Math

- Added [`mid`](/reference/math/lr/#functions-mid) function for scaling
  a delimiter up to the height of the surrounding
  [`lr`](/reference/math/lr/#functions-lr) group
- The [`op`](/reference/math/op/) function can now take any content, not
  just strings
- Improved documentation for [math
  alignment](/reference/math/#alignment)
- Fixed swallowing of trailing comma when a symbol is used in a
  function-like way (e.g. `pi(a,b,)`)

## Scripting

- Any non-identifier dictionary key is now interpreted as an expression:
  For instance,
  <span class="typ-punct">`(`</span><span class="typ-punct">`(`</span>`key`<span class="typ-punct">`)`</span><span class="typ-punct">`:`</span>` value`<span class="typ-punct">`)`</span>
  will create a dictionary with a dynamic key
- The [`stroke`](/reference/visualize/stroke/ "`stroke`") type now has a
  constructor that converts a value to a stroke or creates one from its
  parts
- Added constructor for
  [`arguments`](/reference/foundations/arguments/ "`arguments`") type
- Added
  [`calc.div-euclid`](/reference/foundations/calc/#functions-div-euclid)
  and
  [`calc.rem-euclid`](/reference/foundations/calc/#functions-rem-euclid)
  functions
- Fixed equality of
  [`arguments`](/reference/foundations/arguments/ "`arguments`")
- Fixed [`repr`](/reference/foundations/repr/ "`repr`")of
  [`cmyk`](/reference/visualize/color/#definitions-cmyk) colors
- Fixed crashes with provided elements like figure captions, outline
  entries, and footnote entries

## Tooling and Diagnostics

- Show rules that match on their own output now produce an appropriate
  error message instead of a crash (this is a first step, in the future
  they will just work)
- Too highly or infinitely nested layouts now produce error messages
  instead of crashes
- Added hints for invalid identifiers
- Added hint when trying to use a manually constructed footnote or
  outline entry
- Added missing details to autocompletions for types
- Improved error message when passing a named argument where a
  positional one is expected
- Jump from click now works on raw blocks

## Export

- PDF compilation output is now again fully byte-by-byte reproducible if
  the document's [`date`](/reference/model/document/#parameters-date) is
  set manually
- Fixed color export in SVG
- Fixed PDF metadata encoding of multiple
  [authors](/reference/model/document/#parameters-author)

## Command line interface

- Fixed a major bug where `typst watch` would confuse files and fail to
  pick up updates
- Fetching of the release metadata in `typst update` now respects
  proxies
- Fixed bug with `--open` flag on Windows when the path contains a space
- The `TYPST_FONT_PATHS` environment variable can now contain multiple
  paths (separated by `;` on Windows and `:` elsewhere)
- Updated embedded New Computer Modern fonts to version 4.7
- The watching process doesn't stop anymore when the main file contains
  invalid UTF-8

## Miscellaneous Improvements

- Parallelized image encoding in PDF export
- Improved the internal representation of content for improved
  performance
- Optimized introspection (query, counter, etc.) performance
- The [document title](/reference/model/document/#parameters-title) can
  now be arbitrary content instead of just a string
- The [`number-align`](/reference/model/enum/#parameters-number-align)
  parameter on numbered lists now also accepts vertical alignments
- Fixed selectors on [quote](/reference/model/quote/ "quote") elements
- Fixed parsing of
  <span class="typ-key">`#`</span><span class="typ-key">`return`</span>
  expression in markup
- Fixed bug where inline equations were displayed in equation outlines
- Fixed potential CRLF issue in [`raw`](/reference/text/raw/ "`raw`")
  blocks
- Fixed a bug where Chinese numbering couldn't exceed the number 255

## Development

- Merged `typst` and `typst-library` and extracted `typst-pdf`,
  `typst-svg`, and `typst-render` into separate crates
- The Nix flake now includes the git revision when running
  `typst --version`

## Contributors
