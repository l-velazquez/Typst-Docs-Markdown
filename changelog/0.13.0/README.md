# Version 0.13.0 (February 19, 2025)

## Highlights

- There is now a distinction between [proper
  paragraphs](/reference/model/par/) and just inline-level content. This
  is important for future work on accessibility and means that [first
  line indent](/reference/model/par/#parameters-first-line-indent) can
  now be enabled for all paragraphs instead of just consecutive ones.
- The [`outline`](/reference/model/outline/ "`outline`") has a better
  out-of-the-box look and is more customizable
- The new [`curve`](/reference/visualize/curve/ "`curve`") function
  (that supersedes the `path` function) provides a simpler and more
  flexible interface for creating Bézier curves
- The `image` function now supports raw [pixel raster
  formats](/reference/visualize/image/#parameters-format) for generating
  images from within Typst
- Functions that accept [file paths](/reference/syntax/#paths) now also
  accept raw [bytes](/reference/foundations/bytes/ "bytes"), for full
  flexibility
- WebAssembly [plugins](/reference/foundations/plugin/) are more
  flexible and automatically run multi-threaded
- Fixed a long-standing bug where single-letter strings in math
  (<span class="typ-math-delim">`$`</span><span class="typ-str">`"a"`</span><span class="typ-math-delim">`$`</span>)
  would be displayed in italics
- You can now specify which charset should be
  [covered](/reference/text/text/#parameters-font) by which font family
- The [`pdf.embed`](/reference/pdf/embed/ "`pdf.embed`") function lets
  you embed arbitrary files in the exported PDF
- HTML export is currently under active development. The feature is
  still *very* incomplete, but already available for experimentation
  behind a feature flag.

## Model

- There is now a distinction between [proper
  paragraphs](/reference/model/par/) and just inline-level content
  **(Breaking change)**
  - All text at the root of a document is wrapped in paragraphs.
    Meanwhile, text in a container (like a block) is only wrapped in a
    paragraph if the container holds any block-level content. If all of
    the content is inline-level, no paragraph is created.
  - In the laid-out document, it's not immediately visible whether text
    became part of a paragraph. However, it is still important for
    accessibility, HTML export, and for properties like
    `first-line-indent`.
  - Show rules on `par` now only affect proper paragraphs
  - The `first-line-indent` and `hanging-indent` properties also only
    affect proper paragraphs
  - Creating a
    <span class="typ-func">`par`</span><span class="typ-punct">`[`</span>`..`<span class="typ-punct">`]`</span>
    with body content that is not fully inline-level will result in a
    warning
  - The default show rules of various built-in elements like lists,
    quotes, etc. were adjusted to ensure they produce/don't produce
    paragraphs as appropriate
  - Removed support for booleans and content in
    [`outline.indent`](/reference/model/outline/#parameters-indent "`outline.indent`")
- The [`outline`](/reference/model/outline/ "`outline`") function was
  fully reworked to improve its out-of-the-box behavior **(Breaking
  change)**
  - [Outline entries](/reference/model/outline/#definitions-entry) are
    now [blocks](/reference/layout/block/) and are thus affected by
    block spacing
  - The <span class="typ-key">`auto`</span> indentation mode now aligns
    numberings and titles outline-wide for a grid-like look
  - Automatic indentation now also indents entries without a numbering
  - Titles wrapping over multiple lines now have hanging indent
  - The page number won't appear alone on its own line anymore
  - The link now spans the full entry instead of just the title and page
    number
  - The default spacing between outline leader dots was increased
  - The [`fill`](/reference/model/outline/#definitions-entry-fill)
    parameter was moved from `outline` to `outline.entry` and can thus
    be configured through show-set rules
  - Removed `body` and `page` fields from outline entry
  - Added `indented`, `prefix`, `inner`, `body`, and `page` methods on
    outline entries to simplify writing of show rules
- Added configuration to
  [`par.first-line-indent`](/reference/model/par/#parameters-first-line-indent "`par.first-line-indent`")
  for indenting all paragraphs instead of just consecutive ones
- Added [`form`](/reference/model/ref/#parameters-form) parameter to
  `ref` function. Setting the form to
  <span class="typ-str">`"page"`</span> will produce a page reference
  instead of a textual one.
- Added
  [`document.description`](/reference/model/document/#parameters-description "`document.description`")
  field, which results in corresponding PDF and HTML metadata
- Added
  [`enum.reversed`](/reference/model/enum/#parameters-reversed "`enum.reversed`")
  parameter
- Added support for Greek
  [numbering](/reference/model/numbering/ "numbering")
- When the [`link`](/reference/model/link/ "`link`") function wraps
  around a container like a [block](/reference/layout/block/ "block"),
  it will now generate only one link for the whole block instead of
  individual links for all the visible leaf elements. This significantly
  reduces PDF file sizes when combining `link` and
  [`repeat`](/reference/layout/repeat/ "`repeat`").
- The [`link`](/reference/model/link/ "`link`") function will now only
  strip one prefix (like `mailto:` or `tel:`) instead of multiple
- The link function now suppresses hyphenation via a built-in show-set
  rule rather than through its default show rule
- Displaying the page counter without a specified numbering will now
  take the page numbering into account

## Visualization

- Added new [`curve`](/reference/visualize/curve/ "`curve`") function
  that supersedes the [`path`](/reference/visualize/path/ "`path`")
  function and provides a simpler and more flexible interface. The
  `path` function is now deprecated.
- The `image` function now supports raw [pixel raster
  formats](/reference/visualize/image/#parameters-format). This can be
  used to generate images from within Typst without the need for
  encoding in an image exchange format.
- Added
  [`image.scaling`](/reference/visualize/image/#parameters-scaling "`image.scaling`")
  parameter for configuring how an image is scaled by PNG export and PDF
  viewers (smooth or pixelated)
- Added
  [`image.icc`](/reference/visualize/image/#parameters-icc "`image.icc`")
  parameter for providing or overriding the ICC profile of an image
- Renamed `pattern` to
  [`tiling`](/reference/visualize/tiling/ "`tiling`"). The name
  `pattern` remains as a deprecated alias.
- Added
  [`gradient.center`](/reference/visualize/gradient/#definitions-center "`gradient.center`"),
  [`gradient.radius`](/reference/visualize/gradient/#definitions-radius "`gradient.radius`"),
  [`gradient.focal-center`](/reference/visualize/gradient/#definitions-focal-center "`gradient.focal-center`"),
  and
  [`gradient.focal-radius`](/reference/visualize/gradient/#definitions-focal-radius "`gradient.focal-radius`")
  methods
- Fixed interaction of clipping and outset on
  [`box`](/reference/layout/box/ "`box`") and
  [`block`](/reference/layout/block/ "`block`")
- Fixed panic with [`path`](/reference/visualize/path/ "`path`") of
  infinite length
- Fixed non-solid (e.g. tiling) text fills in clipped blocks
- Fixed a crash for images with a DPI value of zero
- Fixed floating-point error in
  [`gradient.repeat`](/reference/visualize/gradient/#definitions-repeat "`gradient.repeat`")
- Auto-detection of image formats from a raw buffer now has support for
  SVGs

## Scripting

- Functions that accept [file paths](/reference/syntax/#paths) now also
  accept raw [bytes](/reference/foundations/bytes/ "bytes")
  - [`image`](/reference/visualize/image/ "`image`"),
    [`cbor`](/reference/data-loading/cbor/ "`cbor`"),
    [`csv`](/reference/data-loading/csv/ "`csv`"),
    [`json`](/reference/data-loading/json/ "`json`"),
    [`toml`](/reference/data-loading/toml/ "`toml`"),
    [`xml`](/reference/data-loading/xml/ "`xml`"), and
    [`yaml`](/reference/data-loading/yaml/ "`yaml`") now support a path
    string or bytes and their `.decode` variants are deprecated
  - [`plugin`](/reference/foundations/plugin/ "`plugin`"),
    [`bibliography`](/reference/model/bibliography/ "`bibliography`"),
    [`bibliography.style`](/reference/model/bibliography/#parameters-style "`bibliography.style`"),
    [`cite.style`](/reference/model/cite/#parameters-style "`cite.style`"),
    [`raw.theme`](/reference/text/raw/#parameters-theme "`raw.theme`"),
    and
    [`raw.syntaxes`](/reference/text/raw/#parameters-syntaxes "`raw.syntaxes`")
    now accept bytes in addition to path strings. These did not have
    `.decode` variants, so this adds new flexibility.
  - The `path` argument/field of
    [`image`](/reference/visualize/image/ "`image`") and
    [`bibliography`](/reference/model/bibliography/ "`bibliography`")
    was renamed to `source` and `sources`, respectively **(Minor
    breaking change)**
- Improved WebAssembly [plugins](/reference/foundations/plugin/)
  - The `plugin` type is replaced by a [`plugin`
    function](/reference/foundations/plugin/) that returns a
    [module](/reference/foundations/module/ "module") containing normal
    Typst functions. This module can be used with import syntax.
    **(Breaking change)**
  - Plugins now automatically run in multiple threads without any
    changes by plugin authors
  - A new
    [`plugin.transition`](/reference/foundations/plugin/#definitions-transition "`plugin.transition`")
    API is introduced which allows plugins to run impure initialization
    in a way that doesn't break Typst's purity guarantees
- The variable name bound by a bare import (no renaming, no import list)
  is now determined statically and dynamic imports without `as` renaming
  (e.g.
  <span class="typ-key">`import`</span>` `<span class="typ-str">`"ot"`</span>` `<span class="typ-op">`+`</span>` `<span class="typ-str">`"her.typ"`</span>)
  are a hard error **(Breaking change)**
- Values of the
  [`arguments`](/reference/foundations/arguments/ "`arguments`") type
  can now be added with `+` and [joined](/reference/scripting/#blocks)
  in curly-braced code blocks
- Functions in an element function's scope can now be called with method
  syntax, bringing elements and types closer (in anticipation of a
  future full unification of the two). Currently, this is only useful
  for
  [`outline.entry`](/reference/model/outline/#definitions-entry "`outline.entry`")
  as no other element function defines methods.
- Added
  [`calc.norm`](/reference/foundations/calc/#functions-norm "`calc.norm`")
  function
- Added support for 32-bit floats in
  [`float.from-bytes`](/reference/foundations/float/#definitions-from-bytes "`float.from-bytes`")
  and
  [`float.to-bytes`](/reference/foundations/float/#definitions-to-bytes "`float.to-bytes`")
- The [`decimal`](/reference/foundations/decimal/ "`decimal`")
  constructor now also accepts decimal values
- Improved `repr` of [symbols](/reference/foundations/symbol/),
  [arguments](/reference/foundations/arguments/ "arguments"), and
  [types](/reference/foundations/type/)
- Duplicate [symbol](/reference/foundations/symbol/ "symbol") variants
  and modifiers are now a hard error **(Breaking change)**

## Math

- Fixed a bug where single letter strings in math
  (<span class="typ-math-delim">`$`</span><span class="typ-str">`"a"`</span><span class="typ-math-delim">`$`</span>)
  would be displayed in italics
- Math function calls can now have hyphenated named arguments and
  support [argument
  spreading](/reference/foundations/arguments/#spreading)
- Better looking accents thanks to support for the `flac` (Flattened
  Accent Forms) and `dtls` (Dotless Forms) OpenType features
- Added `lcm` [text operator](/reference/math/op/)
- The [`bold`](/reference/math/styles/#functions-bold) function now
  works with ϝ and Ϝ
- The [`italic`](/reference/math/styles/#functions-italic) function now
  works with ħ
- Fixed a bug where the extent of a math equation was wrongly affected
  by internal metadata
- Fixed interaction of [`lr`](/reference/math/lr/#functions-lr) and
  [context](/reference/context/ "context") expressions
- Fixed weak spacing being unconditionally ignored in
  [`lr`](/reference/math/lr/#functions-lr)
- Fixed sub/superscripts sometimes being in the wrong position with
  [`lr`](/reference/math/lr/#functions-lr)
- Fixed multi-line annotations (e.g. overbrace) changing the math
  baseline
- Fixed merging of attachments when the base is a nested equation
- Fixed resolving of contextual (em-based) text sizes within math
- Fixed spacing around up tacks (⊥)

## Bibliography

- Prose and author-only citations now use editor names if the author
  names are unavailable
- Some non-standard but widely used BibLaTeX `editortype`s like
  `producer`, `writer`, `scriptwriter`, and `none` (defined by
  widespread style `biblatex-chicago` to mean performers within `music`
  and `video` entries) are now recognized
- CSL styles can now render affixes around the bibliography
- For BibTeX entries with `eprinttype = {pubmed}`, the PubMed ID will
  now be correctly processed
- Whitespace handling for strings delimiting initialized names has been
  improved
- Uppercase spelling after apostrophes used as quotation marks is now
  possible
- Fixed bugs around the handling of CSL delimiting characters
- Fixed a problem with parsing multibyte characters in page ranges that
  could prevent Hayagriva from parsing some BibTeX page ranges
- Updated CSL APA style
- Updated CSL locales for Finnish, Swiss German, Austrian German,
  German, and Arabic

## Text

- Added support for specifying which charset should be
  [covered](/reference/text/text/#parameters-font) by which font family
- Added [`all`](/reference/text/smallcaps/#parameters-all) parameter to
  `smallcaps` function that also enables small capitals on uppercase
  letters
- Added basic i18n for Basque and Bulgarian
- [Justification](/reference/model/par/#parameters-justify) does not
  affect [raw](/reference/text/raw/ "raw") blocks anymore
- [CJK-Latin-spacing](/reference/text/text/#parameters-cjk-latin-spacing)
  does not affect [raw](/reference/text/raw/ "raw") text anymore
- Fixed wrong language codes being used for Greek and Ukrainian
- Fixed default quotes for Croatian and Bulgarian
- Fixed crash in RTL text handling
- Added support for [`raw`](/reference/text/raw/ "`raw`") syntax
  highlighting for a few new languages: CFML, NSIS, and WGSL
- New font metadata exception for New Computer Modern Sans Math
- Updated bundled New Computer Modern fonts to version 7.0.1

## Layout

- Fixed various bugs with footnotes
  - Fixed footnotes getting lost when multiple footnotes were nested
    within another footnote
  - Fixed endless loops with empty and overlarge footnotes
  - Fixed crash with overlarge footnotes within a floating placement
- Fixed sizing of quadratic shapes
  ([`square`](/reference/visualize/square/ "`square`") and
  [`circle`](/reference/visualize/circle/ "`circle`"))
- Fixed
  [`block.sticky`](/reference/layout/block/#parameters-sticky "`block.sticky`")
  not working properly at the top of a container
- Fixed crash due to consecutive weak spacing
- Fixed crash when a [block](/reference/layout/block/ "block") or text
  have negative sizes
- Fixed unnecessary hyphenations occurring in rare scenarios due to a
  bad interaction between padding and paragraph optimization
- Fixed lone [citations](/reference/model/cite/) in
  [`align`](/reference/layout/align/ "`align`") not becoming their own
  paragraph

## Syntax

- Top-level closing square brackets that do not have a matching opening
  square bracket are now a hard error **(Minor breaking change)**
- Adding a space between the identifier and the parentheses in a set
  rule is not allowed anymore **(Minor breaking change)**
- Numbers with a unit cannot have a base prefix anymore, e.g.
  `0b100000pt` is not allowed anymore. Previously, it was syntactically
  allowed but always resolved to a value of zero. **(Minor breaking
  change)**
- Using `is` as an identifier will now warn as it might become a keyword
  in the future
- Fixed minor whitespace handling bugs
  - in math mode argument lists
  - at the end of headings
  - between a term list's term and description
- Fixed parsing of empty single line raw blocks with 3+ backticks and a
  language tag
- Fixed minor bug with parentheses parsing in math
- Markup that can only appear at the start of the line (headings, lists)
  can now also appear at the start of a list item
- A shebang `#!` at the very start of a file is now ignored

## PDF export

- Added [`pdf.embed`](/reference/pdf/embed/ "`pdf.embed`") function for
  embedding arbitrary files in the exported PDF
- Added support for PDF/A-3b export
- The PDF timestamp will now contain the timezone by default

## HTML export

**Note:** HTML export is currently under active development. The feature
is still *very* incomplete, but already available for experimentation
behind a feature flag.

- Added HTML output support for some (but not all) of the built-in
  elements
- Added [`html.elem`](/reference/html/elem/ "`html.elem`") function for
  outputting an arbitrary HTML element
- Added [`html.frame`](/reference/html/frame/ "`html.frame`") function
  for integrating content that requires layout into HTML (by embedding
  an SVG)
- Added [`target`](/reference/foundations/target/ "`target`") function
  which returns either <span class="typ-str">`"paged"`</span> or
  <span class="typ-str">`"html"`</span> depending on the export target

## Tooling and Diagnostics

- Autocompletion improvements
  - Added autocompletion for file paths
  - Smarter autocompletion of variables: Completing
    <span class="typ-func">`rect`</span><span class="typ-punct">`(`</span>`fill`<span class="typ-punct">`:`</span>` |`<span class="typ-punct">`)`</span>
    will now only show variables which contain a valid fill (either
    directly or nested, e.g. a dictionary containing a valid fill)
  - Different functions will now autocomplete with different brackets
    (round vs square) depending on which kind is more useful
  - Positional parameters which are already provided aren't
    autocompleted again anymore
  - Fixed variable autocompletion not considering parameters
  - Added autocompletion snippets for common figure usages
  - Fixed autocompletion after half-completed import item
  - Fixed autocompletion for `cite` function
- Added warning when an unconditional return in a code block discards
  joined content
- Fixed error message when accessing non-existent label
- Fixed handling of nested imports in IDE functionality

## Command Line Interface

- Added `--features` argument and `TYPST_FEATURES` environment variable
  for opting into experimental features. The only feature so far is
  `html`.
- Added a live reloading HTTP server to `typst watch` when targeting
  HTML
- Fixed self-update not being aware about certain target architectures
- Fixed crash when piping `typst fonts` output to another command
- Fixed handling of relative paths in `--make-deps` output
- Fixed handling of multipage SVG and PNG export in `--make-deps` output
- Colons in filenames are now correctly escaped in `--make-deps` output

## Symbols

- New
  - `inter`, `inter.and`, `inter.big`, `inter.dot`, `inter.double`,
    `inter.sq`, `inter.sq.big`, `inter.sq.double`, `integral.inter`
  - `asymp`, `asymp.not`
  - `mapsto`, `mapsto.long`
  - `divides.not.rev`, `divides.struck`
  - `interleave`, `interleave.big`, `interleave.struck`
  - `eq.triple.not`, `eq.dots`, `eq.dots.down`, `eq.dots.up`
  - `smt`, `smt.eq`, `lat`, `lat.eq`
  - `colon.tri`, `colon.tri.op`
  - `dagger.triple`, `dagger.l`, `dagger.r`, `dagger.inv`
  - `hourglass.stroked`, `hourglass.filled`
  - `die.six`, `die.five`, `die.four`, `die.three`, `die.two`, `die.one`
  - `errorbar.square.stroked`, `errorbar.square.filled`,
    `errorbar.diamond.stroked`, `errorbar.diamond.filled`,
    `errorbar.circle.stroked`, `errorbar.circle.filled`
  - `numero`
- Renamed **(Breaking change)**
  - `ohm.inv` to `Omega.inv`
- Changed codepoint **(Breaking change)**
  - `angle.l.double` from `《` to `⟪`
  - `angle.r.double` from `》` to `⟫`
  - `angstrom` from U+212B (`Å`) to U+00C5 (`Å`)
- Deprecated
  - `sect` and all its variants in favor of `inter`
  - `integral.sect` in favor of `integral.inter`
- Removed **(Breaking change)**
  - `degree.c` in favor of `°C`
    (<span class="typ-math-delim">`$`</span><span class="typ-func">`upright`</span><span class="typ-punct">`(`</span>`°C`<span class="typ-punct">`)`</span><span class="typ-math-delim">`$`</span>
    or
    <span class="typ-math-delim">`$`</span><span class="typ-func">`upright`</span><span class="typ-punct">`(`</span><span class="typ-pol">`degree`</span>` C`<span class="typ-punct">`)`</span><span class="typ-math-delim">`$`</span>
    in math)
  - `degree.f` in favor of `°F`
    (<span class="typ-math-delim">`$`</span><span class="typ-func">`upright`</span><span class="typ-punct">`(`</span>`°F`<span class="typ-punct">`)`</span><span class="typ-math-delim">`$`</span>
    or
    <span class="typ-math-delim">`$`</span><span class="typ-func">`upright`</span><span class="typ-punct">`(`</span><span class="typ-pol">`degree`</span>` F`<span class="typ-punct">`)`</span><span class="typ-math-delim">`$`</span>
    in math)
  - `kelvin` in favor of just K
    (<span class="typ-math-delim">`$`</span><span class="typ-func">`upright`</span><span class="typ-punct">`(`</span>`K`<span class="typ-punct">`)`</span><span class="typ-math-delim">`$`</span>
    in math)
  - `ohm` in favor of `Omega`

## Deprecations

- The [`path`](/reference/visualize/path/ "`path`") function in favor of
  the [`curve`](/reference/visualize/curve/ "`curve`") function
- The name `pattern` for tiling patterns in favor of the new name
  [`tiling`](/reference/visualize/tiling/ "`tiling`")
- [`image.decode`](/reference/visualize/image/#definitions-decode "`image.decode`"),
  [`cbor.decode`](/reference/data-loading/cbor/#definitions-decode "`cbor.decode`"),
  [`csv.decode`](/reference/data-loading/csv/#definitions-decode "`csv.decode`"),
  [`json.decode`](/reference/data-loading/json/#definitions-decode "`json.decode`"),
  [`toml.decode`](/reference/data-loading/toml/#definitions-decode "`toml.decode`"),
  [`xml.decode`](/reference/data-loading/xml/#definitions-decode "`xml.decode`"),
  [`yaml.decode`](/reference/data-loading/yaml/#definitions-decode "`yaml.decode`")
  in favor of the top-level functions directly accepting both paths and
  bytes
- The `sect` and its variants in favor of `inter`, and `integral.sect`
  in favor of `integral.inter`
- The compatibility behavior of type/str comparisons (e.g.
  `int `<span class="typ-op">`==`</span>` `<span class="typ-str">`"integer"`</span>)
  which was temporarily introduced in Typst 0.8 now emits warnings. It
  will be removed in Typst 0.14.

## Removals

- Removed `style` function and `styles` argument of
  [`measure`](/reference/layout/measure/ "`measure`"), use a
  [context](/reference/context/ "context") expression instead
  **(Breaking change)**
- Removed `state.display` function, use
  [`state.get`](/reference/introspection/state/#definitions-get "`state.get`")
  instead **(Breaking change)**
- Removed `location` argument of
  [`state.at`](/reference/introspection/state/#definitions-at "`state.at`"),
  [`counter.at`](/reference/introspection/counter/#definitions-at "`counter.at`"),
  and [`query`](/reference/introspection/query/ "`query`") **(Breaking
  change)**
- Removed compatibility behavior where
  [`counter.display`](/reference/introspection/counter/#definitions-display "`counter.display`")
  worked without [context](/reference/context/ "context") **(Breaking
  change)**
- Removed compatibility behavior of
  [`locate`](/reference/introspection/locate/ "`locate`") **(Breaking
  change)**

## Development

- The `typst::compile` function is now generic and can return either a
  `PagedDocument` or an `HtmlDocument`
- `typst-timing` now supports WebAssembly targets via `web-sys` when the
  `wasm` feature is enabled
- Increased minimum supported Rust version to 1.80
- Fixed linux/arm64 Docker image

## Contributors
