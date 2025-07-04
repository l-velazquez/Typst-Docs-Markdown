# Version 0.2.0 (April 11, 2023)

## Breaking changes

- Removed support for iterating over index and value in [for
  loops](/reference/scripting/#loops). This is now handled via unpacking
  and enumerating. Same goes for the
  [`map`](/reference/foundations/array/#definitions-map) method.
- [Dictionaries](/reference/foundations/dictionary/) now iterate in
  insertion order instead of alphabetical order.

## New features

- Added [unpacking syntax](/reference/scripting/#bindings) for let
  bindings, which allows things like
  <span class="typ-key">`let`</span>` `<span class="typ-punct">`(`</span>`1`<span class="typ-punct">`,`</span>` 2`<span class="typ-punct">`)`</span>` `<span class="typ-op">`=`</span>` array`
- Added
  [`enumerate`](/reference/foundations/array/#definitions-enumerate)
  method
- Added [`path`](/reference/visualize/path/ "`path`") function for
  drawing Bézier paths
- Added [`layout`](/reference/layout/layout/ "`layout`") function to
  access the size of the surrounding page or container
- Added `key` parameter to
  [`sorted`](/reference/foundations/array/#definitions-sorted) method

## Command line interface

- Fixed `--open` flag blocking the program
- New Computer Modern font is now embedded into the binary
- Shell completions and man pages can now be generated by setting the
  `GEN_ARTIFACTS` environment variable to a target directory and then
  building Typst

## Miscellaneous improvements

- Fixed page numbering in outline
- Added basic i18n for a few more languages (AR, NB, CS, NN, PL, SL, ES,
  UA, VI)
- Added a few numbering patterns (Ihora, Chinese)
- Added `sinc` [operator](/reference/math/op/)
- Fixed bug where math could not be hidden with
  [`hide`](/reference/layout/hide/ "`hide`")
- Fixed sizing issues with box, block, and shapes
- Fixed some translations
- Fixed inversion of "R" in
  [`cal`](/reference/math/variants/#functions-cal) and
  [`frak`](/reference/math/variants/#functions-frak) styles
- Fixed some styling issues in math
- Fixed supplements of references to headings
- Fixed syntax highlighting of identifiers in certain scenarios
- [Ratios](/reference/layout/ratio/) can now be multiplied with more
  types and be converted to [floats](/reference/foundations/float/) with
  the [`float`](/reference/foundations/float/ "`float`") function

## Contributors
