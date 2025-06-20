# Version 0.8.0 (September 13, 2023)

## Scripting

- Plugins (thanks to [@astrale-sharp](https://github.com/astrale-sharp)
  and [@arnaudgolfouse](https://github.com/arnaudgolfouse))
  - Typst can now load [plugins](/reference/foundations/plugin/) that
    are compiled to WebAssembly
  - Anything that can be compiled to WebAssembly can thus be loaded as a
    plugin
  - These plugins are fully encapsulated (no access to file system or
    network)
  - Plugins can be shipped as part of
    [packages](/reference/scripting/#packages)
  - Plugins work just the same in the web app
- Types are now first-class values **(Breaking change)**
  - A [type](/reference/foundations/type/ "type") is now itself a value
  - Some types can be called like functions (those that have a
    constructor), e.g. [`int`](/reference/foundations/int/ "`int`") and
    [`str`](/reference/foundations/str/ "`str`")
  - Type checks are now of the form
    <span class="typ-func">`type`</span><span class="typ-punct">`(`</span><span class="typ-num">`10`</span><span class="typ-punct">`)`</span>` `<span class="typ-op">`==`</span>` int`
    instead of the old
    <span class="typ-func">`type`</span><span class="typ-punct">`(`</span><span class="typ-num">`10`</span><span class="typ-punct">`)`</span>` `<span class="typ-op">`==`</span>` `<span class="typ-str">`"integer"`</span>.
    [Compatibility](/reference/foundations/type/#compatibility) with the
    old way will remain for a while to give package authors time to
    upgrade, but it will be removed at some point.
  - Methods are now syntax sugar for calling a function scoped to a
    type, meaning that
    <span class="typ-str">`"hello"`</span><span class="typ-punct">`.`</span><span class="typ-func">`len`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span>
    is equivalent to
    `str`<span class="typ-punct">`.`</span><span class="typ-func">`len`</span><span class="typ-punct">`(`</span><span class="typ-str">`"hello"`</span><span class="typ-punct">`)`</span>
- Added support for [`import`](/reference/scripting/#modules) renaming
  with `as`
- Added a [`duration`](/reference/foundations/duration/ "`duration`")
  type
- Added support for [CBOR](/reference/data-loading/cbor/) encoding and
  decoding
- Added encoding and decoding functions from and to bytes for data
  formats:
  [`json.decode`](/reference/data-loading/json/#definitions-decode),
  [`json.encode`](/reference/data-loading/json/#definitions-encode), and
  similar functions for other formats
- Added
  [`array.intersperse`](/reference/foundations/array/#definitions-intersperse)
  function
- Added [`str.rev`](/reference/foundations/str/#definitions-rev)
  function
- Added `calc.tau` constant
- Made [bytes](/reference/foundations/bytes/ "bytes") joinable and
  addable
- Made [`array.zip`](/reference/foundations/array/#definitions-zip)
  function variadic
- Fixed bug with [`eval`](/reference/foundations/eval/ "`eval`") when
  the `mode` was set to <span class="typ-str">`"math"`</span>
- Fixed bug with
  [`ends-with`](/reference/foundations/str/#definitions-ends-with)
  function on strings
- Fixed bug with destructuring in combination with break, continue, and
  return
- Fixed argument types of [hyperbolic
  functions](/reference/foundations/calc/#functions-cosh), they don't
  allow angles anymore **(Breaking change)**
- Renamed some color methods: `rgba` becomes `to-rgba`, `cmyk` becomes
  `to-cmyk`, and `luma` becomes `to-luma` **(Breaking change)**

## Export

- Added SVG export (thanks to
  [@Enter-tainer](https://github.com/Enter-tainer))
- Fixed bugs with PDF font embedding
- Added support for page labels that reflect the [page
  numbering](/reference/layout/page/#parameters-numbering) style in the
  PDF

## Text and Layout

- Added [`highlight`](/reference/text/highlight/ "`highlight`") function
  for highlighting text with a background color
- Added
  [`polygon.regular`](/reference/visualize/polygon/#definitions-regular)
  function for drawing a regular polygon
- Added support for tabs in [`raw`](/reference/text/raw/ "`raw`")
  elements alongside
  [`tab-width`](/reference/text/raw/#parameters-tab-size) parameter
- The layout engine now tries to prevent "runts" (final lines consisting
  of just a single word)
- Added Finnish translations
- Added hyphenation support for Polish
- Improved handling of consecutive smart quotes of different kinds
- Fixed vertical alignments for
  [`number-align`](/reference/layout/page/#parameters-number-align)
  argument on page function **(Breaking change)**
- Fixed weak pagebreaks after counter updates
- Fixed missing text in SVG when the text font is set to "New Computer
  Modern"
- Fixed translations for Chinese
- Fixed crash for empty text in show rule
- Fixed leading spaces when there's a linebreak after a number and a
  comma
- Fixed placement of floating elements in columns and other containers
- Fixed sizing of block containing just a single box

## Math

- Added support for [augmented
  matrices](/reference/math/mat/#parameters-augment)
- Removed support for automatic matching of fences like `|` and `||` as
  there were too many false positives. You can use functions like
  [`abs`](/reference/math/lr/#functions-abs) or
  [`norm`](/reference/math/lr/#functions-norm) or an explicit
  [`lr`](/reference/math/lr/#functions-lr) call instead. **(Breaking
  change)**
- Fixed spacing after number with decimal point in math
- Fixed bug with primes in subscript
- Fixed weak spacing
- Fixed crash when text within math contains a newline

## Tooling and Diagnostics

- Added hints when trying to call a function stored in a dictionary
  without extra parentheses
- Fixed hint when referencing an equation without numbering
- Added more details to some diagnostics (e.g. when SVG decoding fails)

## Command line interface

- Added `typst update` command for self-updating the CLI (thanks to
  [@jimvdl](https://github.com/jimvdl))
- Added download progress indicator for packages and updates
- Added `--format` argument to explicitly specify the output format
- The CLI now respects proxy configuration through environment variables
  and has a new `--cert` option for setting a custom CA certificate
- Fixed crash when field wasn't present and `--one` is passed to
  `typst query`

## Miscellaneous Improvements

- Added [page setup guide](/guides/page-setup-guide/)
- Added [`figure.caption`](/reference/model/figure/#definitions-caption)
  function that can be used for simpler figure customization (**Breaking
  change** because `it.caption` now renders the full caption with
  supplement in figure show rules and manual outlines)
- Moved `caption-pos` argument to `figure.caption` function and renamed
  it to `position` **(Breaking change)**
- Added
  [`separator`](/reference/model/figure/#definitions-caption-separator)
  argument to `figure.caption` function
- Added support for combination of and/or and before/after
  [selectors](/reference/foundations/selector/)
- Packages can now specify a [minimum compiler
  version](https://github.com/typst/packages#package-format) they
  require to work
- Fixed parser bug where method calls could be moved onto their own line
  for <span class="typ-key">`#`</span><span class="typ-key">`let`</span>
  expressions in markup **(Breaking change)**
- Fixed bugs in sentence and title case conversion for bibliographies
- Fixed supplements for alphanumeric and author-title bibliography
  styles
- Fixed off-by-one error in APA bibliography style

## Development

- Made `Span` and `FileId` more type-safe so that all error conditions
  must be handled by `World` implementors

## Contributors
