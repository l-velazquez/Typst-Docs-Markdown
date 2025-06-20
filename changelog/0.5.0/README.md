# Version 0.5.0 (June 9, 2023)

## Text and Layout

- Added [`raw`](/reference/text/raw/ "`raw`") syntax highlighting for
  many more languages
- Added support for Korean
  [numbering](/reference/model/numbering/ "numbering")
- Added basic i18n for a few more languages (NL, SV, DA)
- Improved line breaking for East Asian languages
- Expanded functionality of outline
  [`indent`](/reference/model/outline/#parameters-indent) property
- Fixed footnotes in columns
- Fixed page breaking bugs with [footnotes](/reference/model/footnote/)
- Fixed bug with handling of footnotes in lists, tables, and figures
- Fixed a bug with CJK punctuation adjustment
- Fixed a crash with rounded rectangles
- Fixed alignment of [`line`](/reference/visualize/line/ "`line`")
  elements

## Math

- **Breaking change:** The syntax rules for mathematical
  [attachments](/reference/math/attach/#functions-attach) were improved:
  <span class="typ-math-delim">`$`</span>`f`<span class="typ-math-op">`^`</span><span class="typ-func">`abs`</span><span class="typ-punct">`(`</span>`3`<span class="typ-punct">`)`</span><span class="typ-math-delim">`$`</span>
  now parses as
  <span class="typ-math-delim">`$`</span>`f`<span class="typ-math-op">`^`</span><span class="typ-punct">`(`</span><span class="typ-func">`abs`</span><span class="typ-punct">`(`</span>`3`<span class="typ-punct">`)`</span><span class="typ-punct">`)`</span><span class="typ-math-delim">`$`</span>
  instead of
  <span class="typ-math-delim">`$`</span>`(f`<span class="typ-math-op">`^`</span><span class="typ-pol">`abs`</span>`)(3)`<span class="typ-math-delim">`$`</span>.
  To disambiguate, add a space:
  <span class="typ-math-delim">`$`</span>`f`<span class="typ-math-op">`^`</span><span class="typ-pol">`zeta`</span>` (3)`<span class="typ-math-delim">`$`</span>.
- Added [forced size](/reference/math/sizes/) commands for math (e.g.,
  [`display`](/reference/math/sizes/#functions-display))
- Added [`supplement`](/reference/math/equation/#parameters-supplement)
  parameter to [`equation`](/reference/math/equation/), used by
  [references](/reference/model/ref/)
- New [symbols](/reference/symbols/sym/): `bullet`, `xor`, `slash.big`,
  `sigma.alt`, `tack.r.not`, `tack.r.short`, `tack.r.double.not`
- Fixed a bug with symbols in matrices
- Fixed a crash in the
  [`attach`](/reference/math/attach/#functions-attach) function

## Scripting

- Added new [`datetime`](/reference/foundations/datetime/ "`datetime`")
  type and
  [`datetime.today`](/reference/foundations/datetime/#definitions-today)
  to retrieve the current date
- Added
  [`str.from-unicode`](/reference/foundations/str/#definitions-from-unicode)
  and
  [`str.to-unicode`](/reference/foundations/str/#definitions-to-unicode)
  functions
- Added [`fields`](/reference/foundations/content/#definitions-fields)
  method on content
- Added `base` parameter to [`str`](/reference/foundations/str/ "`str`")
  function
- Added [`calc.exp`](/reference/foundations/calc/#functions-exp) and
  [`calc.ln`](/reference/foundations/calc/#functions-ln)
- Improved accuracy of
  [`calc.pow`](/reference/foundations/calc/#functions-pow) and
  [`calc.log`](/reference/foundations/calc/#functions-log) for specific
  bases
- Fixed [removal](/reference/foundations/dictionary/#definitions-remove)
  order for dictionary
- Fixed `.at(default: ..)` for
  [strings](/reference/foundations/str/#definitions-at) and
  [content](/reference/foundations/content/#definitions-at)
- Fixed field access on styled elements
- Removed deprecated `calc.mod` function

## Command line interface

- Added PNG export via `typst compile source.typ output-{n}.png`. The
  output path must contain `{n}` if the document has multiple pages.
- Added `--diagnostic-format=short` for Unix-style short diagnostics
- Doesn't emit color codes anymore if stderr isn't a TTY
- Now sets the correct exit when invoked with a nonexistent file
- Now ignores UTF-8 BOM in Typst files

## Miscellaneous Improvements

- Improved errors for mismatched delimiters
- Improved error message for failed length comparisons
- Fixed a bug with images not showing up in Apple Preview
- Fixed multiple bugs with the PDF outline
- Fixed citations and other searchable elements in
  [`hide`](/reference/layout/hide/ "`hide`")
- Fixed bugs with [reference
  supplements](/reference/model/ref/#parameters-supplement)
- Fixed Nix flake

## Contributors
