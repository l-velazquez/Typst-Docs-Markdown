# Version 0.7.0 (August 7, 2023)

## Text and Layout

- Added support for floating figures through the
  [`placement`](/reference/model/figure/#parameters-placement) argument
  on the figure function
- Added support for arbitrary floating content through the
  [`float`](/reference/layout/place/#parameters-float) argument on the
  place function
- Added support for loading `.sublime-syntax` files as highlighting
  [syntaxes](/reference/text/raw/#parameters-syntaxes) for raw blocks
- Added support for loading `.tmTheme` files as highlighting
  [themes](/reference/text/raw/#parameters-theme) for raw blocks
- Added *bounds* option to
  [`top-edge`](/reference/text/text/#parameters-top-edge) and
  [`bottom-edge`](/reference/text/text/#parameters-bottom-edge)
  arguments of text function for tight bounding boxes
- Removed nonsensical top- and bottom-edge options, e.g. *ascender* for
  the bottom edge **(Breaking change)**
- Added [`script`](/reference/text/text/#parameters-script) argument to
  text function
- Added
  [`alternative`](/reference/text/smartquote/#parameters-alternative)
  argument to smart quote function
- Added basic i18n for Japanese
- Added hyphenation support for `nb` and `nn` language codes in addition
  to `no`
- Fixed positioning of [placed elements](/reference/layout/place/) in
  containers
- Fixed overflowing containers due to optimized line breaks

## Export

- Greatly improved export of SVG images to PDF. Many thanks to
  [@LaurenzV](https://github.com/LaurenzV) for their work on this.
- Added support for the alpha channel of RGBA colors in PDF export
- Fixed a bug with PPI (pixels per inch) for PNG export

## Math

- Improved layout of primes (e.g. in
  <span class="typ-math-delim">`$`</span>`a`<span class="typ-math-op">`'`</span><span class="typ-math-op">`_`</span>`1`<span class="typ-math-delim">`$`</span>)
- Improved display of multi-primes (e.g. in
  <span class="typ-math-delim">`$`</span>`a`<span class="typ-math-op">`'`</span><span class="typ-math-op">`'`</span><span class="typ-math-delim">`$`</span>)
- Improved layout of [roots](/reference/math/roots/#functions-root)
- Changed relations to show attachments as
  [limits](/reference/math/attach/#functions-limits) by default (e.g. in
  <span class="typ-math-delim">`$`</span>`a `<span class="typ-escape">`->`</span><span class="typ-math-op">`^`</span>`x b`<span class="typ-math-delim">`$`</span>)
- Large operators and delimiters are now always vertically centered
- [Boxes](/reference/layout/box/) in equations now sit on the baseline
  instead of being vertically centered by default. Notably, this does
  not affect [blocks](/reference/layout/block/) because they are not
  inline elements.
- Added support for [weak spacing](/reference/layout/h/#parameters-weak)
- Added support for OpenType character variants
- Added support for customizing the [math class](/reference/math/class/)
  of content
- Fixed spacing around `.`, `\/`, and `...`
- Fixed spacing between closing delimiters and large operators
- Fixed a bug with math font weight selection
- Symbols and Operators **(Breaking changes)**
  - Added `id`, `im`, and `tr` text [operators](/reference/math/op/)
  - Renamed `ident` to `equiv` with alias `eq.triple` and removed
    `ident.strict` in favor of `eq.quad`
  - Renamed `ast.sq` to `ast.square` and `integral.sq` to
    `integral.square`
  - Renamed `.eqq` modifier to `.equiv` (and `.neqq` to `.nequiv`) for
    `tilde`, `gt`, `lt`, `prec`, and `succ`
  - Added `emptyset` as alias for `nothing`
  - Added `lt.curly` and `gt.curly` as aliases for `prec` and `succ`
  - Added `aleph`, `beth`, and `gimmel` as alias for `alef`, `bet`, and
    `gimel`

## Scripting

- Fields
  - Added `abs` and `em` field to [lengths](/reference/layout/length/)
  - Added `ratio` and `length` field to [relative
    lengths](/reference/layout/relative/)
  - Added `x` and `y` field to [2d
    alignments](/reference/layout/align/#parameters-alignment)
  - Added `paint`, `thickness`, `cap`, `join`, `dash`, and `miter-limit`
    field to [strokes](/reference/visualize/stroke/)
- Accessor and utility methods
  - Added [`dedup`](/reference/foundations/array/#definitions-dedup)
    method to arrays
  - Added `pt`, `mm`, `cm`, and `inches` method to
    [lengths](/reference/layout/length/)
  - Added `deg` and `rad` method to [angles](/reference/layout/angle/)
  - Added `kind`, `hex`, `rgba`, `cmyk`, and `luma` method to
    [colors](/reference/visualize/color/)
  - Added `axis`, `start`, `end`, and `inv` method to
    [directions](/reference/layout/stack/#parameters-dir)
  - Added `axis` and `inv` method to
    [alignments](/reference/layout/align/#parameters-alignment)
  - Added `inv` method to [2d
    alignments](/reference/layout/align/#parameters-alignment)
  - Added `start` argument to
    [`enumerate`](/reference/foundations/array/#definitions-enumerate)
    method on arrays
- Added [`color.mix`](/reference/visualize/color/#definitions-mix)
  function
- Added `mode` and `scope` arguments to
  [`eval`](/reference/foundations/eval/ "`eval`") function
- Added [`bytes`](/reference/foundations/bytes/ "`bytes`") type for
  holding large byte buffers
  - Added
    [`encoding`](/reference/data-loading/read/#parameters-encoding)
    argument to read function to read a file as bytes instead of a
    string
  - Added
    [`image.decode`](/reference/visualize/image/#definitions-decode)
    function for decoding an image directly from a string or bytes
  - Added [`bytes`](/reference/foundations/bytes/ "`bytes`") function
    for converting a string or an array of integers to bytes
  - Added [`array`](/reference/foundations/array/ "`array`") function
    for converting bytes to an array of integers
  - Added support for converting bytes to a string with the
    [`str`](/reference/foundations/str/ "`str`") function

## Tooling and Diagnostics

- Added support for compiler warnings
- Added warning when compilation does not converge within five attempts
  due to intense use of introspection features
- Added warnings for empty emphasis (`__` and `**`)
- Improved error message for invalid field assignments
- Improved error message after single `#`
- Improved error message when a keyword is used where an identifier is
  expected
- Fixed parameter autocompletion for functions that are in modules
- Import autocompletion now only shows the latest package version until
  a colon is typed
- Fixed autocompletion for dictionary key containing a space
- Fixed autocompletion for `for` loops

## Command line interface

- Added `typst query` subcommand to execute a
  [query](/reference/introspection/query/#command-line-queries) on the
  command line
- The `--root` and `--font-paths` arguments cannot appear in front of
  the command anymore **(Breaking change)**
- Local and cached packages are now stored in directories of the form
  `{namespace}/{name}/{version}` instead of
  `{namespace}/{name}-{version}` **(Breaking change)**
- Now prioritizes explicitly given fonts (via `--font-paths`) over
  system and embedded fonts when both exist
- Fixed `typst watch` not working with some text editors
- Fixed displayed compilation time (now includes export)

## Miscellaneous Improvements

- Added [`bookmarked`](/reference/model/heading/#parameters-bookmarked)
  argument to heading to control whether a heading becomes part of the
  PDF outline
- Added
  [`caption-pos`](/reference/model/figure/#definitions-caption-position)
  argument to control the position of a figure's caption
- Added [`metadata`](/reference/introspection/metadata/ "`metadata`")
  function for exposing an arbitrary value to the introspection system
- Fixed that a [`state`](/reference/introspection/state/ "`state`") was
  identified by the pair `(key, init)` instead of just its `key`
- Improved indent logic of [enumerations](/reference/model/enum/).
  Instead of requiring at least as much indent as the end of the marker,
  they now require only one more space indent than the start of the
  marker. As a result, even long markers like `12.` work with just 2
  spaces of indent.
- Fixed bug with indent logic of [`raw`](/reference/text/raw/ "`raw`")
  blocks
- Fixed a parsing bug with dictionaries

## Development

- Extracted parser and syntax tree into `typst-syntax` crate
- The `World::today` implementation of Typst dependents may need fixing
  if they have the same
  [bug](https://github.com/typst/typst/issues/1842) that the CLI world
  had

## Contributors
