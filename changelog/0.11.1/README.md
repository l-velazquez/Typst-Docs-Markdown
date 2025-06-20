# Version 0.11.1 (May 17, 2024)

## Security

- Fixed a vulnerability where image files at known paths could be
  embedded into the PDF even if they were outside of the project
  directory

## Bibliography

- Fixed et-al handling in subsequent citations
- Fixed suppression of title for citations and bibliography references
  with no author
- Fixed handling of initials in citation styles without a delimiter
- Fixed bug with citations in footnotes

## Text and Layout

- Fixed interaction of
  [`first-line-indent`](/reference/model/par/#parameters-first-line-indent)
  and [`outline`](/reference/model/outline/ "`outline`")
- Fixed compression of CJK punctuation marks at line start and end
- Fixed handling of [rectangles](/reference/visualize/rect/) with
  negative dimensions
- Fixed layout of [`path`](/reference/visualize/path/ "`path`") in
  explicitly sized container
- Fixed broken [`raw`](/reference/text/raw/ "`raw`") text in
  right-to-left paragraphs
- Fixed tab rendering in `raw` text with language `typ` or `typc`
- Fixed highlighting of multi-line `raw` text enclosed by single
  backticks
- Fixed indentation of overflowing lines in `raw` blocks
- Fixed extra space when `raw` text ends with a backtick

## Math

- Fixed broken [equations](/reference/math/equation/) in right-to-left
  paragraphs
- Fixed missing [blackboard
  bold](/reference/math/variants/#functions-bb) letters
- Fixed error on empty arguments in 2D math argument list
- Fixed stretching via [`mid`](/reference/math/lr/#functions-mid) for
  various characters
- Fixed that alignment points in equations were affected by
  <span class="typ-key">`set`</span>` `<span class="typ-func">`align`</span><span class="typ-punct">`(`</span><span class="typ-op">`..`</span><span class="typ-punct">`)`</span>

## Export

- Fixed [smart quotes](/reference/text/smartquote/) in PDF outline
- Fixed [patterns](/reference/visualize/tiling/) with spacing in PDF
- Fixed wrong PDF page labels when [page
  numbering](/reference/layout/page/#parameters-numbering) was disabled
  after being previously enabled

## Scripting

- Fixed overflow for large numbers in external data files (by converting
  to floats instead)
- Fixed
  [`str`<span class="typ-punct">`.`</span><span class="typ-func">`trim`</span><span class="typ-punct">`(`</span>`regex`<span class="typ-punct">`,`</span>` at`<span class="typ-punct">`:`</span>` end`<span class="typ-punct">`)`</span>](/reference/foundations/str/#definitions-trim)
  when the whole string is matched

## Miscellaneous

- Fixed deformed strokes for specific shapes and thicknesses
- Fixed newline handling in code mode: There can now be comments within
  chained method calls and between an `if` branch and the `else` keyword
- Fixed inefficiency with incremental reparsing
- Fixed autocompletions for relative file imports
- Fixed crash in autocompletion handler
- Fixed a bug where the path and entrypoint printed by `typst init` were
  not properly escaped
- Fixed various documentation errors

## Contributors
