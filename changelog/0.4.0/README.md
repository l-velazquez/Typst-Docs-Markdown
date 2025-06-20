# Version 0.4.0 (May 20, 2023)

## Footnotes

- Implemented support for footnotes
- The [`footnote`](/reference/model/footnote/ "`footnote`") function
  inserts a footnote
- The [`footnote.entry`](/reference/model/footnote/#definitions-entry)
  function can be used to customize the footnote listing
- The <span class="typ-str">`"chicago-notes"`</span> [citation
  style](/reference/model/cite/#parameters-style) is now available

## Documentation

- Added a [Guide for LaTeX users](/guides/guide-for-latex-users/)
- Now shows default values for optional arguments
- Added richer outlines in "On this Page"
- Added initial support for search keywords: "Table of Contents" will
  now find the [outline](/reference/model/outline/ "outline") function.
  Suggestions for more keywords are welcome!
- Fixed issue with search result ranking
- Fixed many more small issues

## Math

- **Breaking change**: Alignment points (`&`) in equations now alternate
  between left and right alignment
- Added support for writing roots with Unicode: For example,
  <span class="typ-math-delim">`$`</span><span class="typ-func">`root`</span><span class="typ-punct">`(`</span>`x+y`<span class="typ-punct">`)`</span><span class="typ-math-delim">`$`</span>
  can now also be written as
  <span class="typ-math-delim">`$`</span><span class="typ-math-op">`√`</span><span class="typ-punct">`(`</span>`x+y`<span class="typ-punct">`)`</span><span class="typ-math-delim">`$`</span>
- Fixed uneven vertical
  [`attachment`](/reference/math/attach/#functions-attach) alignment
- Fixed spacing on decorated elements (e.g., spacing around a
  [canceled](/reference/math/cancel/) operator)
- Fixed styling for stretchable symbols
- Added `tack.r.double`, `tack.l.double`, `dotless.i` and `dotless.j`
  [symbols](/reference/symbols/sym/)
- Fixed show rules on symbols (e.g.
  <span class="typ-key">`show`</span>` sym`<span class="typ-punct">`.`</span><span class="typ-func">`tack`</span><span class="typ-punct">`:`</span>` `<span class="typ-key">`set`</span>` `<span class="typ-func">`text`</span><span class="typ-punct">`(`</span>`blue`<span class="typ-punct">`)`</span>)
- Fixed missing rename from `ast.op` to `ast` that should have been in
  the previous release

## Scripting

- Added function scopes: A function can now hold related definitions in
  its own scope, similar to a module. The new
  [`assert.eq`](/reference/foundations/assert/#definitions-eq) function,
  for instance, is part of the
  [`assert`](/reference/foundations/assert/ "`assert`") function's
  scope. Note that function scopes are currently only available for
  built-in functions.
- Added [`assert.eq`](/reference/foundations/assert/#definitions-eq) and
  [`assert.ne`](/reference/foundations/assert/#definitions-ne) functions
  for simpler equality and inequality assertions with more helpful error
  messages
- Exposed [list](/reference/model/list/#definitions-item),
  [enum](/reference/model/enum/#definitions-item), and [term
  list](/reference/model/terms/#definitions-item) items in their
  respective functions' scope
- The `at` methods on
  [strings](/reference/foundations/str/#definitions-at),
  [arrays](/reference/foundations/array/#definitions-at),
  [dictionaries](/reference/foundations/dictionary/#definitions-at), and
  [content](/reference/foundations/content/#definitions-at) now support
  specifying a default value
- Added support for passing a function to
  [`replace`](/reference/foundations/str/#definitions-replace) that is
  called with each match.
- Fixed [replacement](/reference/foundations/str/#definitions-replace)
  strings: They are now inserted completely verbatim instead of
  supporting the previous (unintended) magic dollar syntax for capture
  groups
- Fixed bug with trailing placeholders in destructuring patterns
- Fixed bug with underscore in parameter destructuring
- Fixed crash with nested patterns and when hovering over an invalid
  pattern
- Better error messages when casting to an
  [integer](/reference/foundations/int/) or
  [float](/reference/foundations/float/) fails

## Text and Layout

- Implemented sophisticated CJK punctuation adjustment
- Disabled [overhang](/reference/text/text/#parameters-overhang) for CJK
  punctuation
- Added basic translations for Traditional Chinese
- Fixed [alignment](/reference/text/raw/#parameters-align) of text
  inside raw blocks (centering a raw block, e.g. through a figure, will
  now keep the text itself left-aligned)
- Added support for passing a array instead of a function to configure
  table cell [alignment](/reference/model/table/#parameters-align) and
  [fill](/reference/model/table/#parameters-fill) per column
- Fixed automatic figure
  [`kind`](/reference/model/figure/#parameters-kind) detection
- Made alignment of [enum
  numbers](/reference/model/enum/#parameters-number-align) configurable,
  defaulting to `end`
- Figures can now be made breakable with a show-set rule for blocks in
  figure
- Initial fix for smart quotes in RTL languages

## Export

- Fixed ligatures in PDF export: They are now copyable and searchable
- Exported PDFs now embed ICC profiles for images that have them
- Fixed export of strokes with zero thickness

## Web app

- Projects can now contain folders
- Added upload by drag-and-drop into the file panel
- Files from the file panel can now be dragged into the editor to insert
  them into a Typst file
- You can now copy-paste images and other files from your computer
  directly into the editor
- Added a button to resend confirmation email
- Added an option to invert preview colors in dark mode
- Added tips to the loading screen and the Help menu. Feel free to
  propose more!
- Added syntax highlighting for YAML files
- Allowed middle mouse button click on many buttons to navigate into a
  new tab
- Allowed more project names
- Fixed overridden Vim mode keybindings
- Fixed many bugs regarding file upload and more

## Miscellaneous Improvements

- Improved performance of counters, state, and queries
- Improved incremental parsing for more efficient recompilations
- Added support for `.yaml` extension in addition to `.yml` for
  bibliographies
- The CLI now emits escape codes only if the output is a TTY
- For users of the `typst` crate: The `Document` is now `Sync` again and
  the `World` doesn't have to be `'static` anymore

## Contributors
