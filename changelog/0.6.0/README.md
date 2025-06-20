# Version 0.6.0 (June 30, 2023)

## Package Management

- Typst now has built-in [package
  management](/reference/scripting/#packages)
- You can import [published](https://typst.app/universe/) community
  packages or create and use
  [system-local](https://github.com/typst/packages#local-packages) ones
- Published packages are also supported in the web app

## Math

- Added support for optical size variants of glyphs in math mode
- Added argument to enable
  [`limits`](/reference/math/attach/#functions-limits) conditionally
  depending on whether the equation is set in
  [`display`](/reference/math/sizes/#functions-display) or
  [`inline`](/reference/math/sizes/#functions-inline) style
- Added `gt.eq.slant` and `lt.eq.slant` symbols
- Increased precedence of factorials in math mode
  (<span class="typ-math-delim">`$`</span>`1`<span class="typ-math-op">`/`</span>`n!`<span class="typ-math-delim">`$`</span>
  works correctly now)
- Improved [underlines](/reference/math/underover/#functions-underline)
  and [overlines](/reference/math/underover/#functions-overline) in math
  mode
- Fixed usage of [`limits`](/reference/math/attach/#functions-limits)
  function in show rules
- Fixed bugs with line breaks in equations

## Text and Layout

- Added support for alternating page
  [margins](/reference/layout/page/#parameters-margin) with the `inside`
  and `outside` keys
- Added support for specifying the page
  [`binding`](/reference/layout/page/#parameters-binding)
- Added [`to`](/reference/layout/pagebreak/#parameters-to) argument to
  pagebreak function to skip to the next even or odd page
- Added basic i18n for a few more languages (TR, SQ, TL)
- Fixed bug with missing table row at page break
- Fixed bug with [underlines](/reference/text/underline/)
- Fixed bug superfluous table lines
- Fixed smart quotes after line breaks
- Fixed a crash related to text layout

## Command line interface

- **Breaking change:** Added requirement for `--root`/`TYPST_ROOT`
  directory to contain the input file because it designates the
  *project* root. Existing setups that use `TYPST_ROOT` to emulate
  package management should switch to [local
  packages](https://github.com/typst/packages#local-packages)
- **Breaking change:** Now denies file access outside of the project
  root
- Added support for local packages and on-demand package download
- Now watches all relevant files, within the root and all packages
- Now displays compilation time

## Miscellaneous Improvements

- Added [`outline.entry`](/reference/model/outline/#definitions-entry)
  to customize outline entries with show rules
- Added some hints for error messages
- Added some missing syntaxes for [`raw`](/reference/text/raw/ "`raw`")
  highlighting
- Improved rendering of rotated images in PNG export and web app
- Made [footnotes](/reference/model/footnote/) reusable and
  referenceable
- Fixed bug with citations and bibliographies in
  [`locate`](/reference/introspection/locate/ "`locate`")
- Fixed inconsistent tense in documentation

## Development

- Added [contribution
  guide](https://github.com/typst/typst/blob/main/CONTRIBUTING.md)
- Reworked `World` interface to accommodate for package management and
  make it a bit simpler to implement *(Breaking change for
  implementors)*

## Contributors
