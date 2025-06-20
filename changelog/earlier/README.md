# Changes in early, unversioned Typst

## March 28, 2023

- **Breaking changes:**

  - Enumerations now require a space after their marker, that is, `1.ok`
    must now be written as <span class="typ-marker">`1.`</span>` ok`
  - Changed default style for [term lists](/reference/model/terms/):
    Does not include a colon anymore and has a bit more indent

- Command line interface

  - Added `--font-path` argument for CLI
  - Embedded default fonts in CLI binary
  - Fixed build of CLI if `git` is not installed

- Miscellaneous improvements

  - Added support for disabling [matrix](/reference/math/mat/) and
    [vector](/reference/math/vec/) delimiters. Generally with
    <span class="typ-key">`#`</span><span class="typ-key">`set`</span>` math`<span class="typ-punct">`.`</span><span class="typ-func">`mat`</span><span class="typ-punct">`(`</span>`delim`<span class="typ-punct">`:`</span>` `<span class="typ-key">`none`</span><span class="typ-punct">`)`</span>
    or one-off with
    <span class="typ-math-delim">`$`</span><span class="typ-func">`mat`</span><span class="typ-punct">`(`</span>`delim`<span class="typ-punct">`:`</span>` `<span class="typ-key">`#`</span><span class="typ-key">`none`</span><span class="typ-punct">`,`</span>` 1`<span class="typ-punct">`,`</span>` 2`<span class="typ-punct">`;`</span>` 3`<span class="typ-punct">`,`</span>` 4`<span class="typ-punct">`)`</span><span class="typ-math-delim">`$`</span>.
  - Added [`separator`](/reference/model/terms/#parameters-separator)
    argument to term lists
  - Added [`round`](/reference/math/lr/#functions-round) function for
    equations
  - Numberings now allow zeros. To reset a counter, you can write
    <span class="typ-func">`#`</span><span class="typ-func">`counter`</span><span class="typ-punct">`(`</span><span class="typ-op">`..`</span><span class="typ-punct">`)`</span><span class="typ-punct">`.`</span><span class="typ-func">`update`</span><span class="typ-punct">`(`</span><span class="typ-num">`0`</span><span class="typ-punct">`)`</span>
  - Added documentation for
    <span class="typ-func">`page`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span>
    and
    <span class="typ-func">`position`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span>
    methods on
    [`location`](/reference/introspection/location/ "`location`") type
  - Added symbols for double, triple, and quadruple dot accent
  - Added smart quotes for Norwegian Bokmål
  - Added Nix flake
  - Fixed bibliography ordering in IEEE style
  - Fixed parsing of decimals in math:
    <span class="typ-math-delim">`$`</span>`1.2`<span class="typ-math-op">`/`</span>`3.4`<span class="typ-math-delim">`$`</span>
  - Fixed parsing of unbalanced delimiters in fractions:
    <span class="typ-math-delim">`$`</span>`1`<span class="typ-math-op">`/`</span>`(2 (x)`<span class="typ-math-delim">`$`</span>
  - Fixed unexpected parsing of numbers as enumerations, e.g. in `1.2`
  - Fixed combination of page fill and header
  - Fixed compiler crash if
    [`repeat`](/reference/layout/repeat/ "`repeat`") is used in page
    with automatic width
  - Fixed [matrices](/reference/math/mat/) with explicit delimiter
  - Fixed [`indent`](/reference/model/terms/#parameters-indent) property
    of term lists
  - Numerous documentation fixes
  - Links in bibliographies are now affected by link styling
  - Fixed hovering over comments in web app

## March 21, 2023

- Reference and bibliography management

  - [Bibliographies](/reference/model/bibliography/) and
    [citations](/reference/model/cite/) (currently supported styles are
    APA, Chicago Author Date, IEEE, and MLA)
  - You can now [reference](/reference/model/ref/) sections, figures,
    formulas, and works from the bibliography with
    <span class="typ-ref">`@label`</span>
  - You can make an element referenceable with a label:
    - <span class="typ-heading">`= Introduction`</span>` `<span class="typ-label">`<intro>`</span>
    - <span class="typ-math-delim">`$`</span>` A = `<span class="typ-pol">`pi`</span>` r`<span class="typ-math-op">`^`</span>`2 `<span class="typ-math-delim">`$`</span>` `<span class="typ-label">`<area>`</span>

- Introspection system for interactions between different parts of the
  document

  - [`counter`](/reference/introspection/counter/ "`counter`") function
    - Access and modify counters for pages, headings, figures, and
      equations
    - Define and use your own custom counters
    - Time travel: Find out what the counter value was or will be at
      some other point in the document (e.g. when you're building a list
      of figures, you can determine the value of the figure counter at
      any given figure).
    - Counters count in layout order and not in code order
  - [`state`](/reference/introspection/state/ "`state`") function
    - Manage arbitrary state across your document
    - Time travel: Find out the value of your state at any position in
      the document
    - State is modified in layout order and not in code order
  - [`query`](/reference/introspection/query/ "`query`") function
    - Find all occurrences of an element or a label, either in the whole
      document or before/after some location
    - Link to elements, find out their position on the pages and access
      their fields
    - Example use cases: Custom list of figures or page header with
      current chapter title
  - [`locate`](/reference/introspection/locate/ "`locate`") function
    - Determines the location of itself in the final layout
    - Can be accessed to get the `page` and `x`, `y` coordinates
    - Can be used with counters and state to find out their values at
      that location
    - Can be used with queries to find elements before or after its
      location

- New [`measure`](/reference/layout/measure/ "`measure`") function

  - Measure the layouted size of elements
  - To be used in combination with the new `style` function that lets
    you generate different content based on the style context something
    is inserted into (because that affects the measured size of content)

- Exposed content representation

  - Content is not opaque anymore
  - Content can be compared for equality
  - The tree of content elements can be traversed with code
  - Can be observed in hover tooltips or with
    [`repr`](/reference/foundations/repr/ "`repr`")
  - New [methods](/reference/foundations/content/) on content: `func`,
    `has`, `at`, and `location`
  - All optional fields on elements are now settable
  - More uniform field names (`heading.title` becomes `heading.body`,
    `list.items` becomes `list.children`, and a few more changes)

- Further improvements

  - Added [`figure`](/reference/model/figure/ "`figure`") function
  - Added [`numbering`](/reference/math/equation/#parameters-numbering)
    parameter on equation function
  - Added [`numbering`](/reference/layout/page/#parameters-numbering)
    and
    [`number-align`](/reference/layout/page/#parameters-number-align)
    parameters on page function
  - The page function's
    [`header`](/reference/layout/page/#parameters-header) and
    [`footer`](/reference/layout/page/#parameters-footer) parameters do
    not take functions anymore. If you want to customize them based on
    the page number, use the new
    [`numbering`](/reference/layout/page/#parameters-numbering)
    parameter or
    [`counter`](/reference/introspection/counter/ "`counter`") function
    instead.
  - Added
    [`footer-descent`](/reference/layout/page/#parameters-footer-descent)
    and
    [`header-ascent`](/reference/layout/page/#parameters-header-ascent)
    parameters
  - Better default alignment in header and footer
  - Fixed Arabic vowel placement
  - Fixed PDF font embedding issues
  - Renamed `math.formula` to
    [`math.equation`](/reference/math/equation/)
  - Font family must be a named argument now:
    <span class="typ-key">`#`</span><span class="typ-key">`set`</span>` `<span class="typ-func">`text`</span><span class="typ-punct">`(`</span>`font`<span class="typ-punct">`:`</span>` `<span class="typ-str">`".."`</span><span class="typ-punct">`)`</span>
  - Added support for [hanging
    indent](/reference/model/par/#parameters-hanging-indent)
  - Renamed paragraph `indent` to
    [`first-line-indent`](/reference/model/par/#parameters-first-line-indent)
  - More accurate
    [logarithm](/reference/foundations/calc/#functions-log) when base is
    `2` or `10`
  - Improved some error messages
  - Fixed layout of [`terms`](/reference/model/terms/ "`terms`") list

- Web app improvements

  - Added template gallery
  - Added buttons to insert headings, equations, raw blocks, and
    references
  - Jump to the source of something by clicking on it in the preview
    panel (works for text, equations, images, and more)
  - You can now upload your own fonts and use them in your project
  - Hover debugging and autocompletion now takes multiple files into
    account and works in show rules
  - Hover tooltips now automatically collapse multiple consecutive equal
    values
  - The preview now automatically scrolls to the right place when you
    type
  - Links are now clickable in the preview area
  - Toolbar, preview, and editor can now all be hidden
  - Added autocompletion for raw block language tags
  - Added autocompletion in SVG files
  - New back button instead of four-dots button
  - Lots of bug fixes

## February 25, 2023

- Font changes
  - New default font: Linux Libertine
  - New default font for raw blocks: DejaVu Sans Mono
  - New default font for math: Book weight of New Computer Modern Math
  - Lots of new math fonts available
  - Removed Latin Modern fonts in favor of New Computer Modern family
  - Removed unnecessary smallcaps fonts which are already accessible
    through the corresponding main font and the
    [`smallcaps`](/reference/text/smallcaps/ "`smallcaps`") function
- Improved default spacing for headings
- Added [`panic`](/reference/foundations/panic/ "`panic`") function
- Added [`clusters`](/reference/foundations/str/#definitions-clusters)
  and [`codepoints`](/reference/foundations/str/#definitions-codepoints)
  methods for strings
- Support for multiple authors in
  [`set document`](/reference/model/document/#parameters-author)
- Fixed crash when string is accessed at a position that is not a char
  boundary
- Fixed semicolon parsing in
  <span class="typ-pol">`#`</span><span class="typ-pol">`var`</span>` ;`
- Fixed incremental parsing when inserting backslash at end of
  <span class="typ-str">`#`</span><span class="typ-str">`"abc"`</span>
- Fixed names of a few font families (including Noto Sans Symbols and
  New Computer Modern families)
- Fixed autocompletion for font families
- Improved incremental compilation for user-defined functions

## February 15, 2023

- [Box](/reference/layout/box/) and
  [block](/reference/layout/block/ "block") have gained `fill`,
  `stroke`, `radius`, and `inset` properties
- Blocks may now be explicitly sized, fixed-height blocks can still
  break across pages
- Blocks can now be configured to be
  [`breakable`](/reference/layout/block/#parameters-breakable) or not
- [Numbering style](/reference/model/enum/#parameters-numbering) can now
  be configured for nested enums
- [Markers](/reference/model/list/#parameters-marker) can now be
  configured for nested lists
- The [`eval`](/reference/foundations/eval/ "`eval`") function now
  expects code instead of markup and returns an arbitrary value. Markup
  can still be evaluated by surrounding the string with brackets.
- PDFs generated by Typst now contain XMP metadata
- Link boxes are now disabled in PDF output
- Tables don't produce small empty cells before a pagebreak anymore
- Fixed raw block highlighting bug

## February 12, 2023

- Shapes, images, and transformations (move/rotate/scale/repeat) are now
  block-level. To integrate them into a paragraph, use a
  [`box`](/reference/layout/box/ "`box`") as with other elements.
- A colon is now required in an "everything" show rule: Write
  <span class="typ-key">`show`</span><span class="typ-punct">`:`</span>` it `<span class="typ-op">`=>`</span>` ..`
  instead of
  <span class="typ-key">`show`</span>` it `<span class="typ-op">`=>`</span>` ..`.
  This prevents intermediate states that ruin your whole document.
- Non-math content like a shape or table in a math formula is now
  centered vertically
- Support for widow and orphan prevention within containers
- Support for [RTL](/reference/text/text/#parameters-dir) in lists,
  grids, and tables
- Support for explicit <span class="typ-key">`auto`</span> sizing for
  boxes and shapes
- Support for fractional (i.e. <span class="typ-num">`1fr`</span>)
  widths for boxes
- Fixed bug where columns jump to next page
- Fixed bug where list items have no leading
- Fixed relative sizing in lists, squares and grid auto columns
- Fixed relative displacement in
  [`place`](/reference/layout/place/ "`place`") function
- Fixed that lines don't have a size
- Fixed bug where
  <span class="typ-key">`set`</span>` `<span class="typ-func">`document`</span><span class="typ-punct">`(`</span><span class="typ-op">`..`</span><span class="typ-punct">`)`</span>
  complains about being after content
- Fixed parsing of
  <span class="typ-key">`not`</span>` `<span class="typ-key">`in`</span>
  operation
- Fixed hover tooltips in math
- Fixed bug where a heading show rule may not contain a pagebreak when
  an outline is present
- Added [`baseline`](/reference/layout/box/#parameters-baseline)
  property on [`box`](/reference/layout/box/ "`box`")
- Added [`tg`](/reference/math/op/) and [`ctg`](/reference/math/op/)
  operators in math
- Added delimiter setting for [`cases`](/reference/math/cases/) function
- Parentheses are now included when accepting a function autocompletion

## February 2, 2023

- Merged text and math symbols, renamed a few symbols (including `infty`
  to `infinity` with the alias `oo`)
- Fixed missing italic mappings
- Math italics correction is now applied properly
- Parentheses now scale in
  <span class="typ-math-delim">`$`</span><span class="typ-func">`zeta`</span><span class="typ-punct">`(`</span>`x`<span class="typ-math-op">`/`</span>`2`<span class="typ-punct">`)`</span><span class="typ-math-delim">`$`</span>
- Fixed placement of large root index
- Fixed spacing in
  <span class="typ-math-delim">`$`</span><span class="typ-func">`abs`</span><span class="typ-punct">`(`</span><span class="typ-escape">`-`</span>`x`<span class="typ-punct">`)`</span><span class="typ-math-delim">`$`</span>
- Fixed inconsistency between text and identifiers in math
- Accents are now ignored when positioning superscripts
- Fixed vertical alignment in matrices
- Fixed `text` set rule in `raw` show rule
- Heading and list markers now parse consistently
- Allow arbitrary math directly in content

## January 30, 2023

[Go to the announcement blog
post.](https://typst.app/blog/2023/january-update)

- New expression syntax in markup/math
  - Blocks cannot be directly embedded in markup anymore
  - Like other expressions, they now require a leading hash
  - More expressions available with hash, including literals
    (<span class="typ-str">`#`</span><span class="typ-str">`"string"`</span>)
    as well as field access and method call without space:
    <span class="typ-pol">`#`</span><span class="typ-pol">`emoji`</span><span class="typ-punct">`.`</span><span class="typ-pol">`face`</span>
- New import syntax
  - <span class="typ-key">`#`</span><span class="typ-key">`import`</span>` `<span class="typ-str">`"module.typ"`</span>
    creates binding named `module`
  - <span class="typ-key">`#`</span><span class="typ-key">`import`</span>` `<span class="typ-str">`"module.typ"`</span><span class="typ-punct">`:`</span>` a`<span class="typ-punct">`,`</span>` b`
    or
    <span class="typ-key">`#`</span><span class="typ-key">`import`</span>` `<span class="typ-str">`"module.typ"`</span><span class="typ-punct">`:`</span>` `<span class="typ-op">`*`</span>
    to import items
  - <span class="typ-key">`#`</span><span class="typ-key">`import`</span>` emoji`<span class="typ-punct">`:`</span>` face`<span class="typ-punct">`,`</span>` turtle`
    to import from already bound module
- New symbol handling
  - Removed symbol notation
  - Symbols are now in modules: `sym`, `emoji`, and `math`
  - Math module also reexports all of `sym`
  - Modified through field access, still order-independent
  - Unknown modifiers are not allowed anymore
  - Support for custom symbol definitions with `symbol` function
  - Symbols now listed in documentation
- New `math` module
  - Contains all math-related functions
  - Variables and function calls directly in math (without hash) access
    this module instead of the global scope, but can also access local
    variables
  - Can be explicitly used in code, e.g.
    <span class="typ-key">`#`</span><span class="typ-key">`set`</span>` math`<span class="typ-punct">`.`</span><span class="typ-func">`vec`</span><span class="typ-punct">`(`</span>`delim`<span class="typ-punct">`:`</span>` `<span class="typ-str">`"["`</span><span class="typ-punct">`)`</span>
- Delimiter matching in math
  - Any opening delimiters matches any closing one
  - When matched, they automatically scale
  - To prevent scaling, escape them
  - To forcibly match two delimiters, use `lr` function
  - Line breaks may occur between matched delimiters
  - Delimiters may also be unbalanced
  - You can also use the `lr` function to scale the brackets (or just
    one bracket) to a specific size manually
- Multi-line math with alignment
  - The `\` character inserts a line break
  - The `&` character defines an alignment point
  - Alignment points also work for underbraces, vectors, cases, and
    matrices
  - Multiple alignment points are supported
- More capable math function calls
  - Function calls directly in math can now take code expressions with
    hash
  - They can now also take named arguments
  - Within math function calls, semicolons turn preceding arguments to
    arrays to support matrices:
    <span class="typ-math-delim">`$`</span><span class="typ-func">`mat`</span><span class="typ-punct">`(`</span>`1`<span class="typ-punct">`,`</span>` 2`<span class="typ-punct">`;`</span>` 3`<span class="typ-punct">`,`</span>` 4`<span class="typ-punct">`)`</span><span class="typ-math-delim">`$`</span>
- Arbitrary content in math
  - Text, images, and other arbitrary content can now be embedded in
    math
  - Math now also supports font fallback to support e.g. CJK and emoji
- More math features
  - New text operators: `op` function, `lim`, `max`, etc.
  - New matrix function: `mat`
  - New n-ary roots with `root` function:
    <span class="typ-math-delim">`$`</span><span class="typ-func">`root`</span><span class="typ-punct">`(`</span>`3`<span class="typ-punct">`,`</span>` x`<span class="typ-punct">`)`</span><span class="typ-math-delim">`$`</span>
  - New under- and overbraces, -brackets, and -lines
  - New `abs` and `norm` functions
  - New shorthands: `[|`, `|]`, and `||`
  - New `attach` function, overridable attachments with `script` and
    `limit`
  - Manual spacing in math, with `h`, `thin`, `med`, `thick` and `quad`
  - Symbols and other content may now be used like a function, e.g.
    <span class="typ-math-delim">`$`</span><span class="typ-func">`zeta`</span><span class="typ-punct">`(`</span>`x`<span class="typ-punct">`)`</span><span class="typ-math-delim">`$`</span>
  - Added Fira Math font, removed Noto Sans Math font
  - Support for alternative math fonts through
    <span class="typ-key">`#`</span><span class="typ-key">`show`</span>` math`<span class="typ-punct">`.`</span><span class="typ-func">`formula`</span><span class="typ-punct">`:`</span>` `<span class="typ-key">`set`</span>` `<span class="typ-func">`text`</span><span class="typ-punct">`(`</span><span class="typ-str">`"Fira Math"`</span><span class="typ-punct">`)`</span>
- More library improvements
  - New `calc` module, `abs`, `min`, `max`, `even`, `odd` and `mod`
    moved there
  - New `message` argument on `assert` function
  - The `pairs` method on dictionaries now returns an array of length-2
    arrays instead of taking a closure
  - The method call
    `dict`<span class="typ-punct">`.`</span><span class="typ-func">`at`</span><span class="typ-punct">`(`</span><span class="typ-str">`"key"`</span><span class="typ-punct">`)`</span>
    now always fails if `"key"` doesn't exist Previously, it was allowed
    in assignments. Alternatives are
    `dict`<span class="typ-punct">`.`</span>`key `<span class="typ-op">`=`</span>` x`
    and
    `dict`<span class="typ-punct">`.`</span><span class="typ-func">`insert`</span><span class="typ-punct">`(`</span><span class="typ-str">`"key"`</span><span class="typ-punct">`,`</span>` x`<span class="typ-punct">`)`</span>.
- Smarter editor functionality
  - Autocompletion for local variables
  - Autocompletion for methods available on a value
  - Autocompletion for symbols and modules
  - Autocompletion for imports
  - Hover over an identifier to see its value(s)
- Further editor improvements
  - New Font menu with previews
  - Single projects may now be shared with share links
  - New dashboard experience if projects are shared with you
  - Keyboard Shortcuts are now listed in the menus and there are more of
    them
  - New Offline indicator
  - Tooltips for all buttons
  - Improved account protection
  - Moved Status indicator into the error list button
- Further fixes
  - Multiple bug fixes for incremental parser
  - Fixed closure parameter capturing
  - Fixed tons of math bugs
  - Bugfixes for performance, file management, editing reliability
  - Added redirection to the page originally navigated to after signin
