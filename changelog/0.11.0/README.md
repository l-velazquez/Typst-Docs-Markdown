# Version 0.11.0 (March 15, 2024)

## Tables

- Tables are now *much* more flexible, read the new [table
  guide](/guides/table-guide/) to get started
- Added
  [`table.cell`](/reference/model/table/#definitions-cell "`table.cell`")
  element for per-cell configuration
- Cells can now span multiple
  [columns](/reference/model/table/#definitions-cell-colspan) or
  [rows](/reference/model/table/#definitions-cell-rowspan)
- The [stroke](/reference/model/table/#definitions-cell-stroke) of
  individual cells can now be customized
- The [`align`](/reference/model/table/#parameters-align) and
  [`inset`](/reference/model/table/#parameters-inset) arguments of the
  table function now also take
  <span class="typ-punct">`(`</span>`x`<span class="typ-punct">`,`</span>` y`<span class="typ-punct">`)`</span>` `<span class="typ-op">`=>`</span>` ..`
  functions
- Added
  [`table.hline`](/reference/model/table/#definitions-hline "`table.hline`")
  and
  [`table.vline`](/reference/model/table/#definitions-vline "`table.vline`")
  for convenient line customization
- Added
  [`table.header`](/reference/model/table/#definitions-header "`table.header`")
  element for table headers that repeat on every page
- Added
  [`table.footer`](/reference/model/table/#definitions-footer "`table.footer`")
  element for table footers that repeat on every page
- All the new table functionality is also available for
  [grids](/reference/layout/grid/)
- Fixed gutter-related bugs

*Thanks to [@PgBiel](https://github.com/PgBiel) for his work on tables!*

## Templates

- You can now use template packages to get started with new projects.
  Click *Start from template* on the web app's dashboard and choose your
  preferred template or run the `typst init <template>` command in
  the CLI. You can [browse the available templates
  here](https://typst.app/universe/search/?kind=templates).
- Switching templates after the fact has become easier. You can just
  import a styling function from a different template package.
- Package authors can now submit their own templates to the [package
  repository](https://github.com/typst/packages). Share a template for a
  paper, your institution, or an original work to help the community get
  a head start on their projects.
- Templates and packages are now organized by category and discipline.
  Filter packages by either taxonomy in the *Start from template*
  wizard. If you are a package author, take a look at the new
  documentation for
  [categories](https://github.com/typst/packages/blob/main/CATEGORIES.md)
  and
  [disciplines](https://github.com/typst/packages/blob/main/DISCIPLINES.md).

## Context

- Added *context expressions:* Read the chapter on
  [context](/reference/context/ "context") to get started
- With context, you can access settable properties, e.g.
  <span class="typ-key">`context`</span>` text`<span class="typ-punct">`.`</span>`lang`
  to access the language set via
  <span class="typ-key">`set`</span>` `<span class="typ-func">`text`</span><span class="typ-punct">`(`</span>`lang`<span class="typ-punct">`:`</span>` `<span class="typ-str">`".."`</span><span class="typ-punct">`)`</span>
- The following existing functions have been made contextual:
  [`query`](/reference/introspection/query/ "`query`"),
  [`locate`](/reference/introspection/locate/ "`locate`"),
  [`measure`](/reference/layout/measure/ "`measure`"),
  [`counter.display`](/reference/introspection/counter/#definitions-display "`counter.display`"),
  [`counter.at`](/reference/introspection/counter/#definitions-at "`counter.at`"),
  [`counter.final`](/reference/introspection/counter/#definitions-final "`counter.final`"),
  [`state.at`](/reference/introspection/state/#definitions-at "`state.at`"),
  and
  [`state.final`](/reference/introspection/state/#definitions-final "`state.final`")
- Added contextual methods
  [`counter.get`](/reference/introspection/counter/#definitions-get "`counter.get`")
  and
  [`state.get`](/reference/introspection/state/#definitions-get "`state.get`")
  to retrieve the value of a counter or state in the current context
- Added contextual function
  [`here`](/reference/introspection/here/ "`here`") to retrieve the
  [location](/reference/introspection/location/ "location") of the
  current context
- The [`locate`](/reference/introspection/locate/ "`locate`") function
  now returns the location of a selector's unique match. Its old
  behavior has been replaced by context expressions and only remains
  temporarily available for compatibility.
- The
  [`counter.at`](/reference/introspection/counter/#definitions-at "`counter.at`")
  and
  [`state.at`](/reference/introspection/state/#definitions-at "`state.at`")
  methods are now more flexible: They directly accept any kind of
  [locatable](/reference/introspection/location/#locatable) selector
  with a unique match (e.g. a label) instead of just locations
- When context is available,
  [`counter.display`](/reference/introspection/counter/#definitions-display "`counter.display`")
  now directly returns the result of applying the numbering instead of
  yielding opaque content. It should not be used anymore without
  context. (Deprecation planned)
- The `state.display` function should not be used anymore, use
  [`state.get`](/reference/introspection/state/#definitions-get "`state.get`")
  instead (Deprecation planned)
- The `location` argument of
  [`query`](/reference/introspection/query/ "`query`"),
  [`counter.final`](/reference/introspection/counter/#definitions-final "`counter.final`"),
  and
  [`state.final`](/reference/introspection/state/#definitions-final "`state.final`")
  should not be used anymore (Deprecation planned)
- The `styles` argument of the `measure` function should not be used
  anymore (Deprecation planned)
- The `style` function should not be used anymore, use context instead
  (Deprecation planned)
- The correct context is now also provided in various other places where
  it is available, e.g. in show rules, layout callbacks, and numbering
  functions in the outline

## Styling

- Fixed priority of multiple [show-set
  rules](/reference/styling/#show-rules): They now apply in the same
  order as normal set rules would
- Show-set rules on the same element (e.g.
  <span class="typ-key">`show`</span>` heading`<span class="typ-punct">`.`</span><span class="typ-func">`where`</span><span class="typ-punct">`(`</span>`level`<span class="typ-punct">`:`</span>` `<span class="typ-num">`1`</span><span class="typ-punct">`)`</span><span class="typ-punct">`:`</span>` `<span class="typ-key">`set`</span>` `<span class="typ-func">`heading`</span><span class="typ-punct">`(`</span>`numbering`<span class="typ-punct">`:`</span>` `<span class="typ-str">`"1."`</span><span class="typ-punct">`)`</span>)
  now work properly
- Setting properties on an element within a transformational show rule
  (e.g.
  <span class="typ-key">`show`</span>` `<span class="typ-func">`heading`</span><span class="typ-punct">`:`</span>` it `<span class="typ-op">`=>`</span>` `<span class="typ-punct">`{`</span>` `<span class="typ-key">`set`</span>` `<span class="typ-func">`heading`</span><span class="typ-punct">`(`</span><span class="typ-op">`..`</span><span class="typ-punct">`)`</span><span class="typ-punct">`;`</span>` it `<span class="typ-punct">`}`</span>)
  is **not** supported anymore (previously it also only worked
  sometimes); use show-set rules instead **(Breaking change)**
- Text show rules that match their own output now work properly (e.g.
  <span class="typ-key">`show`</span>` `<span class="typ-str">`"cmd"`</span><span class="typ-punct">`:`</span>` `<span class="typ-raw">`` `cmd` ``</span>)
- The elements passed to show rules and returned by queries now contain
  all fields of their respective element functions rather than just
  specific ones
- All settable properties can now be used in
  [where](/reference/foundations/function/#definitions-where) selectors
- [And](/reference/foundations/selector/#definitions-and) and
  [or](/reference/foundations/selector/#definitions-or) selectors can
  now be used with show rules
- Errors within show rules and context expressions are now ignored in
  all but the last introspection iteration, in line with the behavior of
  the old [`locate`](/reference/introspection/locate/ "`locate`")
- Fixed a bug where document set rules were allowed after content

## Layout

- Added `reflow` argument to [`rotate`](/reference/layout/rotate/) and
  [`scale`](/reference/layout/scale/) which lets them affect the layout
- Fixed a bug where [floating
  placement](/reference/layout/place/#parameters-float) or [floating
  figures](/reference/model/figure/#parameters-placement) could end up
  out of order
- Fixed overlap of text and figure for full-page floating figures
- Fixed various cases where the
  [`hide`](/reference/layout/hide/ "`hide`") function didn't hide its
  contents properly
- Fixed usage of [`h`](/reference/layout/h/ "`h`") and
  [`v`](/reference/layout/v/ "`v`") in
  [stacks](/reference/layout/stack/)
- Invisible content like a counter update will no longer force a visible
  block for just itself
- Fixed a bug with horizontal spacing followed by invisible content
  (like a counter update) directly at the start of a paragraph

## Text

- Added [`stroke`](/reference/text/text/#parameters-stroke) property for
  text
- Added basic i18n for Serbian and Catalan
- Added support for contemporary Japanese
  [numbering](/reference/model/numbering/ "numbering") method
- Added patches for various wrong metadata in specific fonts
- The [text direction](/reference/text/text/#parameters-dir) can now be
  overridden within a paragraph
- Fixed Danish [smart quotes](/reference/text/smartquote/)
- Fixed font fallback next to a line break
- Fixed width adjustment of JIS-style Japanese punctuation
- Fixed Finnish translation of "Listing"
- Fixed Z-ordering of multiple text decorations (underlines, etc.)
- Fixed a bug due to which text
  [features](/reference/text/text/#parameters-features) could not be
  overridden in consecutive set rules

## Model

- Added [`depth`](/reference/model/heading/#parameters-depth) and
  [`offset`](/reference/model/heading/#parameters-offset) arguments to
  heading to increase or decrease the heading level for a bunch of
  content; the heading syntax now sets `depth` rather than `level`
  **(Breaking change)**
- List [markers](/reference/model/list/#parameters-marker) now cycle by
  default
- The [`quote`](/reference/model/quote/ "`quote`") function now more
  robustly selects the correct quotes based on language and nesting
- Fixed indent bugs related to the default show rule of
  [terms](/reference/model/terms/ "terms")

## Math

- Inline equations now automatically linebreak at appropriate places
- Added
  [`number-align`](/reference/math/equation/#parameters-number-align)
  argument to equations
- Added support for adjusting the
  [`size`](/reference/math/accent/#parameters-size) of accents relative
  to their base
- Improved positioning of accents
- [Primes](/reference/math/primes/) are now always attached as
  [scripts](/reference/math/attach/#functions-scripts) by default
- Exposed [`math.primes`](/reference/math/primes/ "`math.primes`")
  element which backs the
  <span class="typ-math-delim">`$`</span>`f`<span class="typ-math-op">`'`</span><span class="typ-math-delim">`$`</span>
  syntax in math
- Math mode is not affected by
  [`strong`](/reference/model/strong/ "`strong`") and
  [`emph`](/reference/model/emph/ "`emph`") anymore
- Fixed [`attach`](/reference/math/attach/#functions-attach) under
  [fractions](/reference/math/frac/)
- Fixed that [`math.class`](/reference/math/class/ "`math.class`") did
  not affect smart limit placement
- Fixed weak spacing in [`lr`](/reference/math/lr/#functions-lr) groups
- Fixed layout of large operators for Cambria Math font
- Fixed math styling of Hebrew symbol codepoints

## Symbols

- Added `gradient` as an alias for `nabla`
- Added `partial` as an alias for `diff`, `diff` will be deprecated in
  the future
- Added `colon.double`, `gt.approx`, `gt.napprox`, `lt.approx`, and
  `lt.napprox`
- Added `arrow.r.tilde` and `arrow.l.tilde`
- Added `tilde.dot`
- Added `forces` and `forces.not`
- Added `space.nobreak.narrow`
- Added `lrm` (Left-to-Right Mark) and `rlm` (Right-to-Left Mark)
- Fixed `star.stroked` symbol (which previously had the wrong codepoint)

## Scripting

- Arrays can now be compared lexicographically
- Added contextual method
  [`to-absolute`](/reference/layout/length/#definitions-to-absolute) to
  lengths
- Added [`calc.root`](/reference/foundations/calc/#functions-root)
- Added
  [`int.signum`](/reference/foundations/int/#definitions-signum "`int.signum`")
  and
  [`float.signum`](/reference/foundations/float/#definitions-signum "`float.signum`")
  methods
- Added
  [`float.is-nan`](/reference/foundations/float/#definitions-is-nan "`float.is-nan`")
  and
  [`float.is-infinite`](/reference/foundations/float/#definitions-is-infinite "`float.is-infinite`")
  methods
- Added
  [`int.bit-not`](/reference/foundations/int/#definitions-bit-not "`int.bit-not`"),
  [`int.bit-and`](/reference/foundations/int/#definitions-bit-and "`int.bit-and`"),
  [`int.bit-or`](/reference/foundations/int/#definitions-bit-or "`int.bit-or`"),
  [`int.bit-xor`](/reference/foundations/int/#definitions-bit-xor "`int.bit-xor`"),
  [`int.bit-lshift`](/reference/foundations/int/#definitions-bit-lshift "`int.bit-lshift`"),
  and
  [`int.bit-rshift`](/reference/foundations/int/#definitions-bit-rshift "`int.bit-rshift`")
  methods
- Added
  [`array.chunks`](/reference/foundations/array/#definitions-chunks "`array.chunks`")
  method
- A module can now be converted to a dictionary with the [dictionary
  constructor](/reference/foundations/dictionary/#constructor) to access
  its contents dynamically
- Added [`row-type`](/reference/data-loading/csv/#parameters-row-type)
  argument to `csv` function to configure how rows will be represented
- [XML parsing](/reference/data-loading/xml/) now allows DTDs (document
  type definitions)
- Improved formatting of negative numbers with
  [`str`](/reference/foundations/str/) and
  [`repr`](/reference/foundations/repr/)
- For loops can now iterate over
  [bytes](/reference/foundations/bytes/ "bytes")
- Fixed a bug with pattern matching in for loops
- Fixed a bug with labels not being part of
  [`.`<span class="typ-func">`fields`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span>](/reference/foundations/content/#definitions-fields)
  dictionaries
- Fixed a bug where unnamed argument sinks wouldn't capture excess
  arguments
- Fixed typo in `repr` output of strokes

## Syntax

- Added support for nested [destructuring
  patterns](/reference/scripting/#bindings)
- Special spaces (like thin or non-breaking spaces) are now parsed
  literally instead of being collapsed into normal spaces **(Breaking
  change)**
- Korean text can now use emphasis syntax without adding spaces
  **(Breaking change)**
- The token [`context`](/reference/context/ "`context`") is now a
  keyword and cannot be used as an identifier anymore **(Breaking
  change)**
- Nested line comments aren't allowed anymore in block comments
  **(Breaking change)**
- Fixed a bug where `x.)` would be treated as a field access
- Text elements can now span across curly braces in markup
- Fixed silently wrong parsing when function name is parenthesized
- Fixed various bugs with parsing of destructuring patterns, arrays, and
  dictionaries

## Tooling & Diagnostics

- Click-to-jump now works properly within
  [`raw`](/reference/text/raw/ "`raw`") text
- Added suggestion for accessing a field if a method doesn't exist
- Improved hint for calling a function stored in a dictionary
- Improved errors for mutable accessor functions on arrays and
  dictionaries
- Fixed error message when calling constructor of type that doesn't have
  one
- Fixed confusing error message with nested dictionaries for strokes on
  different sides
- Fixed autocompletion for multiple packages with the same name from
  different namespaces

## Visualization

- The [`image`](/reference/visualize/image/ "`image`") function doesn't
  upscale images beyond their natural size anymore
- The [`image`](/reference/visualize/image/ "`image`") function now
  respects rotation stored in EXIF metadata
- Added support for SVG filters
- Added alpha component to
  [`luma`](/reference/visualize/color/#definitions-luma) colors
- Added
  [`color.transparentize`](/reference/visualize/color/#definitions-transparentize "`color.transparentize`")
  and
  [`color.opacify`](/reference/visualize/color/#definitions-opacify "`color.opacify`")
  methods
- Improved
  [`color.negate`](/reference/visualize/color/#definitions-negate "`color.negate`")
  function
- Added [`stroke`](/reference/text/highlight/#parameters-stroke) and
  [`radius`](/reference/text/highlight/#parameters-radius) arguments to
  `highlight` function
- Changed default
  [`highlight`](/reference/text/highlight/ "`highlight`") color to be
  transparent
- CMYK to RGB conversion is now color-managed
- Fixed crash with gradients in Oklch color space
- Fixed color-mixing for hue-based spaces
- Fixed bugs with color conversion
- SVG sizes are not rounded anymore, preventing slightly wrong aspect
  ratios
- Fixed a few other SVG-related bugs
- [`color.components`](/reference/visualize/color/#definitions-components "`color.components`")
  doesn't round anything anymore

## Export

- PDFs now contain named destinations for headings derived from their
  labels
- The internal PDF structure was changed to make it easier for external
  tools to extract or modify individual pages, avoiding a bug with Typst
  PDFs in Apple Preview
- PDFs produced by Typst should now be byte-by-byte reproducible when
  <span class="typ-key">`set`</span>` `<span class="typ-func">`document`</span><span class="typ-punct">`(`</span>`date`<span class="typ-punct">`:`</span>` `<span class="typ-key">`none`</span><span class="typ-punct">`)`</span>
  is set
- Added missing flag to PDF annotation
- Fixed multiple bugs with gradients in PDF export
- Fixed a bug with patterns in PDF export
- Fixed a bug with embedding of grayscale images in PDF export
- Fixed a bug with To-Unicode mapping of CFF fonts in PDF export
- Fixed a bug with the generation of the PDF outline
- Fixed a sorting bug in PDF export leading to non-reproducible output
- Fixed a bug with transparent text in PNG export
- Exported SVG files now include units in their top-level `width` and
  `height`

## Command line interface

- Added support for passing [inputs](/reference/foundations/sys/) via a
  CLI flag
- When passing the filename `-`, Typst will now read input from stdin
- Now uses the system-native TLS implementation for network fetching
  which should be generally more robust
- Watch mode will now properly detect when a previously missing file is
  created
- Added `--color` flag to configure whether to print colored output
- Fixed user agent with which packages are downloaded
- Updated bundled fonts to the newest versions

## Development

- Added `--vendor-openssl` to CLI to configure whether to link OpenSSL
  statically instead of dynamically (not applicable to Windows and Apple
  platforms)
- Removed old tracing (and its verbosity) flag from the CLI
- Added new `--timings` flag which supersedes the old flamegraph
  profiling in the CLI
- Added minimal CLI to `typst-docs` crate for extracting the language
  and standard library documentation as JSON
- The `typst_pdf::export` function's `ident` argument switched from
  `Option` to `Smart`. It should only be set to `Smart::Custom` if you
  can provide a stable identifier (like the web app can). The CLI sets
  `Smart::Auto`.

## Contributors
