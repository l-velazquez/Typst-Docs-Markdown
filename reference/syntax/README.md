# Syntax

Typst is a markup language. This means that you can use simple syntax to
accomplish common layout tasks. The lightweight markup syntax is
complemented by set and show rules, which let you style your document
easily and automatically. All this is backed by a tightly integrated
scripting language with built-in and user-defined functions.

## Modes

Typst has three syntactical modes: Markup, math, and code. Markup mode
is the default in a Typst document, math mode lets you write
mathematical formulas, and code mode lets you use Typst's scripting
features.

You can switch to a specific mode at any point by referring to the
following table:

| New mode | Syntax | Example |
|----|----|----|
| Code | Prefix the code with `#` | `Number: `<span class="typ-punct">`#`</span><span class="typ-punct">`(`</span><span class="typ-num">`1`</span>` `<span class="typ-op">`+`</span>` `<span class="typ-num">`2`</span><span class="typ-punct">`)`</span> |
| Math | Surround equation with <span class="typ-math-delim">`$`</span>`..`<span class="typ-math-delim">`$`</span> | <span class="typ-math-delim">`$`</span><span class="typ-escape">`-`</span>`x`<span class="typ-math-delim">`$`</span>` is the opposite of `<span class="typ-math-delim">`$`</span>`x`<span class="typ-math-delim">`$`</span> |
| Markup | Surround markup with `[..]` | <span class="typ-key">`let`</span>` name `<span class="typ-op">`=`</span>` `<span class="typ-punct">`[`</span><span class="typ-strong">`*Typst!*`</span><span class="typ-punct">`]`</span> |

Once you have entered code mode with `#`, you don't need to use further
hashes unless you switched back to markup or math mode in between.

## Markup

Typst provides built-in markup for the most common document elements.
Most of the syntax elements are just shortcuts for a corresponding
function. The table below lists all markup that is available and links
to the best place to learn more about their syntax and usage.

| Name | Example | See |
|----|----|----|
| Paragraph break | Blank line | [`parbreak`](/reference/model/parbreak/ "`parbreak`") |
| Strong emphasis | <span class="typ-strong">`*strong*`</span> | [`strong`](/reference/model/strong/ "`strong`") |
| Emphasis | <span class="typ-emph">`_emphasis_`</span> | [`emph`](/reference/model/emph/ "`emph`") |
| Raw text | <span class="typ-raw">`` `print(1)` ``</span> | [`raw`](/reference/text/raw/ "`raw`") |
| Link | <span class="typ-link">`https://typst.app/`</span> | [`link`](/reference/model/link/ "`link`") |
| Label | <span class="typ-label">`<intro>`</span> | [`label`](/reference/foundations/label/ "`label`") |
| Reference | <span class="typ-ref">`@intro`</span> | [`ref`](/reference/model/ref/ "`ref`") |
| Heading | <span class="typ-heading">`= Heading`</span> | [`heading`](/reference/model/heading/ "`heading`") |
| Bullet list | <span class="typ-marker">`-`</span>` item` | [`list`](/reference/model/list/ "`list`") |
| Numbered list | <span class="typ-marker">`+`</span>` item` | [`enum`](/reference/model/enum/ "`enum`") |
| Term list | <span class="typ-marker">`/`</span>` `<span class="typ-term">`Term`</span><span class="typ-punct">`:`</span>` description` | [`terms`](/reference/model/terms/ "`terms`") |
| Math | <span class="typ-math-delim">`$`</span>`x`<span class="typ-math-op">`^`</span>`2`<span class="typ-math-delim">`$`</span> | [Math](/reference/math/) |
| Line break | <span class="typ-escape">`\`</span> | [`linebreak`](/reference/text/linebreak/ "`linebreak`") |
| Smart quote | `'single' or "double"` | [`smartquote`](/reference/text/smartquote/ "`smartquote`") |
| Symbol shorthand | <span class="typ-escape">`~`</span>, <span class="typ-escape">`---`</span> | [Symbols](/reference/symbols/sym/) |
| Code expression | <span class="typ-func">`#`</span><span class="typ-func">`rect`</span><span class="typ-punct">`(`</span>`width`<span class="typ-punct">`:`</span>` `<span class="typ-num">`1cm`</span><span class="typ-punct">`)`</span> | [Scripting](/reference/scripting/#expressions) |
| Character escape | `Tweet at us `<span class="typ-escape">`\#`</span>`ad` | [Below](#escapes) |
| Comment | <span class="typ-comment">`/* block */`</span>, <span class="typ-comment">`// line`</span> | [Below](#comments) |

## Math mode

Math mode is a special markup mode that is used to typeset mathematical
formulas. It is entered by wrapping an equation in `$` characters. This
works both in markup and code. The equation will be typeset into its own
block if it starts and ends with at least one space (e.g.
<span class="typ-math-delim">`$`</span>` x`<span class="typ-math-op">`^`</span>`2 `<span class="typ-math-delim">`$`</span>).
Inline math can be produced by omitting the whitespace (e.g.
<span class="typ-math-delim">`$`</span>`x`<span class="typ-math-op">`^`</span>`2`<span class="typ-math-delim">`$`</span>).
An overview over the syntax specific to math mode follows:

| Name | Example | See |
|----|----|----|
| Inline math | <span class="typ-math-delim">`$`</span>`x`<span class="typ-math-op">`^`</span>`2`<span class="typ-math-delim">`$`</span> | [Math](/reference/math/) |
| Block-level math | <span class="typ-math-delim">`$`</span>` x`<span class="typ-math-op">`^`</span>`2 `<span class="typ-math-delim">`$`</span> | [Math](/reference/math/) |
| Bottom attachment | <span class="typ-math-delim">`$`</span>`x`<span class="typ-math-op">`_`</span>`1`<span class="typ-math-delim">`$`</span> | [`attach`](/reference/math/attach/) |
| Top attachment | <span class="typ-math-delim">`$`</span>`x`<span class="typ-math-op">`^`</span>`2`<span class="typ-math-delim">`$`</span> | [`attach`](/reference/math/attach/) |
| Fraction | <span class="typ-math-delim">`$`</span>`1 + `<span class="typ-punct">`(`</span>`a+b`<span class="typ-punct">`)`</span><span class="typ-math-op">`/`</span>`5`<span class="typ-math-delim">`$`</span> | [`frac`](/reference/math/frac/) |
| Line break | <span class="typ-math-delim">`$`</span>`x `<span class="typ-escape">`\`</span>` y`<span class="typ-math-delim">`$`</span> | [`linebreak`](/reference/text/linebreak/ "`linebreak`") |
| Alignment point | <span class="typ-math-delim">`$`</span>`x `<span class="typ-math-op">`&`</span>`= 2 `<span class="typ-escape">`\`</span>` `<span class="typ-math-op">`&`</span>`= 3`<span class="typ-math-delim">`$`</span> | [Math](/reference/math/) |
| Variable access | <span class="typ-math-delim">`$`</span><span class="typ-pol">`#`</span><span class="typ-pol">`x`</span><span class="typ-math-delim">`$`</span>`, `<span class="typ-math-delim">`$`</span><span class="typ-pol">`pi`</span><span class="typ-math-delim">`$`</span> | [Math](/reference/math/) |
| Field access | <span class="typ-math-delim">`$`</span><span class="typ-pol">`arrow`</span><span class="typ-punct">`.`</span><span class="typ-pol">`r`</span><span class="typ-punct">`.`</span><span class="typ-pol">`long`</span><span class="typ-math-delim">`$`</span> | [Scripting](/reference/scripting/#fields) |
| Implied multiplication | <span class="typ-math-delim">`$`</span>`x y`<span class="typ-math-delim">`$`</span> | [Math](/reference/math/) |
| Symbol shorthand | <span class="typ-math-delim">`$`</span><span class="typ-escape">`->`</span><span class="typ-math-delim">`$`</span>, <span class="typ-math-delim">`$`</span><span class="typ-escape">`!=`</span><span class="typ-math-delim">`$`</span> | [Symbols](/reference/symbols/sym/) |
| Text/string in math | <span class="typ-math-delim">`$`</span>`a `<span class="typ-str">`"is natural"`</span><span class="typ-math-delim">`$`</span> | [Math](/reference/math/) |
| Math function call | <span class="typ-math-delim">`$`</span><span class="typ-func">`floor`</span><span class="typ-punct">`(`</span>`x`<span class="typ-punct">`)`</span><span class="typ-math-delim">`$`</span> | [Math](/reference/math/) |
| Code expression | <span class="typ-math-delim">`$`</span><span class="typ-func">`#`</span><span class="typ-func">`rect`</span><span class="typ-punct">`(`</span>`width`<span class="typ-punct">`:`</span>` `<span class="typ-num">`1cm`</span><span class="typ-punct">`)`</span><span class="typ-math-delim">`$`</span> | [Scripting](/reference/scripting/#expressions) |
| Character escape | <span class="typ-math-delim">`$`</span>`x`<span class="typ-escape">`\^`</span>`2`<span class="typ-math-delim">`$`</span> | [Below](#escapes) |
| Comment | <span class="typ-math-delim">`$`</span><span class="typ-comment">`/* comment */`</span><span class="typ-math-delim">`$`</span> | [Below](#comments) |

## Code mode

Within code blocks and expressions, new expressions can start without a
leading `#` character. Many syntactic elements are specific to
expressions. Below is a table listing all syntax that is available in
code mode:

| Name | Example | See |
|----|----|----|
| None | <span class="typ-key">`none`</span> | [`none`](/reference/foundations/none/ "`none`") |
| Auto | <span class="typ-key">`auto`</span> | [`auto`](/reference/foundations/auto/ "`auto`") |
| Boolean | <span class="typ-key">`false`</span>, <span class="typ-key">`true`</span> | [`bool`](/reference/foundations/bool/ "`bool`") |
| Integer | <span class="typ-num">`10`</span>, <span class="typ-num">`0xff`</span> | [`int`](/reference/foundations/int/ "`int`") |
| Floating-point number | <span class="typ-num">`3.14`</span>, <span class="typ-num">`1e5`</span> | [`float`](/reference/foundations/float/ "`float`") |
| Length | <span class="typ-num">`2pt`</span>, <span class="typ-num">`3mm`</span>, <span class="typ-num">`1em`</span>, .. | [`length`](/reference/layout/length/ "`length`") |
| Angle | <span class="typ-num">`90deg`</span>, <span class="typ-num">`1rad`</span> | [`angle`](/reference/layout/angle/ "`angle`") |
| Fraction | <span class="typ-num">`2fr`</span> | [`fraction`](/reference/layout/fraction/ "`fraction`") |
| Ratio | <span class="typ-num">`50%`</span> | [`ratio`](/reference/layout/ratio/ "`ratio`") |
| String | <span class="typ-str">`"hello"`</span> | [`str`](/reference/foundations/str/ "`str`") |
| Label | <span class="typ-label">`<intro>`</span> | [`label`](/reference/foundations/label/ "`label`") |
| Math | <span class="typ-math-delim">`$`</span>`x`<span class="typ-math-op">`^`</span>`2`<span class="typ-math-delim">`$`</span> | [Math](/reference/math/) |
| Raw text | <span class="typ-raw">`` `print(1)` ``</span> | [`raw`](/reference/text/raw/ "`raw`") |
| Variable access | `x` | [Scripting](/reference/scripting/#blocks) |
| Code block | <span class="typ-punct">`{`</span>` `<span class="typ-key">`let`</span>` x `<span class="typ-op">`=`</span>` `<span class="typ-num">`1`</span><span class="typ-punct">`;`</span>` x `<span class="typ-op">`+`</span>` `<span class="typ-num">`2`</span>` `<span class="typ-punct">`}`</span> | [Scripting](/reference/scripting/#blocks) |
| Content block | <span class="typ-punct">`[`</span><span class="typ-strong">`*Hello*`</span><span class="typ-punct">`]`</span> | [Scripting](/reference/scripting/#blocks) |
| Parenthesized expression | <span class="typ-punct">`(`</span><span class="typ-num">`1`</span>` `<span class="typ-op">`+`</span>` `<span class="typ-num">`2`</span><span class="typ-punct">`)`</span> | [Scripting](/reference/scripting/#blocks) |
| Array | <span class="typ-punct">`(`</span><span class="typ-num">`1`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`2`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`3`</span><span class="typ-punct">`)`</span> | [Array](/reference/foundations/array/) |
| Dictionary | <span class="typ-punct">`(`</span>`a`<span class="typ-punct">`:`</span>` `<span class="typ-str">`"hi"`</span><span class="typ-punct">`,`</span>` b`<span class="typ-punct">`:`</span>` `<span class="typ-num">`2`</span><span class="typ-punct">`)`</span> | [Dictionary](/reference/foundations/dictionary/) |
| Unary operator | <span class="typ-op">`-`</span>`x` | [Scripting](/reference/scripting/#operators) |
| Binary operator | `x `<span class="typ-op">`+`</span>` y` | [Scripting](/reference/scripting/#operators) |
| Assignment | `x `<span class="typ-op">`=`</span>` `<span class="typ-num">`1`</span> | [Scripting](/reference/scripting/#operators) |
| Field access | `x`<span class="typ-punct">`.`</span>`y` | [Scripting](/reference/scripting/#fields) |
| Method call | `x`<span class="typ-punct">`.`</span><span class="typ-func">`flatten`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span> | [Scripting](/reference/scripting/#methods) |
| Function call | <span class="typ-func">`min`</span><span class="typ-punct">`(`</span>`x`<span class="typ-punct">`,`</span>` y`<span class="typ-punct">`)`</span> | [Function](/reference/foundations/function/) |
| Argument spreading | <span class="typ-func">`min`</span><span class="typ-punct">`(`</span><span class="typ-op">`..`</span>`nums`<span class="typ-punct">`)`</span> | [Arguments](/reference/foundations/arguments/) |
| Unnamed function | <span class="typ-punct">`(`</span>`x`<span class="typ-punct">`,`</span>` y`<span class="typ-punct">`)`</span>` `<span class="typ-op">`=>`</span>` x `<span class="typ-op">`+`</span>` y` | [Function](/reference/foundations/function/) |
| Let binding | <span class="typ-key">`let`</span>` x `<span class="typ-op">`=`</span>` `<span class="typ-num">`1`</span> | [Scripting](/reference/scripting/#bindings) |
| Named function | <span class="typ-key">`let`</span>` `<span class="typ-func">`f`</span><span class="typ-punct">`(`</span>`x`<span class="typ-punct">`)`</span>` `<span class="typ-op">`=`</span>` `<span class="typ-num">`2`</span>` `<span class="typ-op">`*`</span>` x` | [Function](/reference/foundations/function/) |
| Set rule | <span class="typ-key">`set`</span>` `<span class="typ-func">`text`</span><span class="typ-punct">`(`</span><span class="typ-num">`14pt`</span><span class="typ-punct">`)`</span> | [Styling](/reference/styling/#set-rules) |
| Set-if rule | <span class="typ-key">`set`</span>` `<span class="typ-func">`text`</span><span class="typ-punct">`(`</span><span class="typ-op">`..`</span><span class="typ-punct">`)`</span>` `<span class="typ-key">`if`</span>` .. ` | [Styling](/reference/styling/#set-rules) |
| Show-set rule | <span class="typ-key">`show`</span>` `<span class="typ-func">`heading`</span><span class="typ-punct">`:`</span>` `<span class="typ-key">`set`</span>` `<span class="typ-func">`block`</span><span class="typ-punct">`(`</span><span class="typ-op">`..`</span><span class="typ-punct">`)`</span> | [Styling](/reference/styling/#show-rules) |
| Show rule with function | <span class="typ-key">`show`</span>` `<span class="typ-func">`raw`</span><span class="typ-punct">`:`</span>` it `<span class="typ-op">`=>`</span>` `<span class="typ-punct">`{`</span>`..`<span class="typ-punct">`}`</span> | [Styling](/reference/styling/#show-rules) |
| Show-everything rule | <span class="typ-key">`show`</span><span class="typ-punct">`:`</span>` `<span class="typ-func">`template`</span> | [Styling](/reference/styling/#show-rules) |
| Context expression | <span class="typ-key">`context`</span>` text`<span class="typ-punct">`.`</span>`lang` | [Context](/reference/context/) |
| Conditional | <span class="typ-key">`if`</span>` x `<span class="typ-op">`==`</span>` `<span class="typ-num">`1`</span>` `<span class="typ-punct">`{`</span>`..`<span class="typ-punct">`}`</span>` `<span class="typ-key">`else`</span>` `<span class="typ-punct">`{`</span>`..`<span class="typ-punct">`}`</span> | [Scripting](/reference/scripting/#conditionals) |
| For loop | <span class="typ-key">`for`</span>` x `<span class="typ-key">`in`</span>` `<span class="typ-punct">`(`</span><span class="typ-num">`1`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`2`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`3`</span><span class="typ-punct">`)`</span>` `<span class="typ-punct">`{`</span>`..`<span class="typ-punct">`}`</span> | [Scripting](/reference/scripting/#loops) |
| While loop | <span class="typ-key">`while`</span>` x `<span class="typ-op">`<`</span>` `<span class="typ-num">`10`</span>` `<span class="typ-punct">`{`</span>`..`<span class="typ-punct">`}`</span> | [Scripting](/reference/scripting/#loops) |
| Loop control flow | <span class="typ-key">`break`</span>`, `<span class="typ-key">`continue`</span> | [Scripting](/reference/scripting/#loops) |
| Return from function | <span class="typ-key">`return`</span>` x` | [Function](/reference/foundations/function/) |
| Include module | <span class="typ-key">`include`</span>` `<span class="typ-str">`"bar.typ"`</span> | [Scripting](/reference/scripting/#modules) |
| Import module | <span class="typ-key">`import`</span>` `<span class="typ-str">`"bar.typ"`</span> | [Scripting](/reference/scripting/#modules) |
| Import items from module | <span class="typ-key">`import`</span>` `<span class="typ-str">`"bar.typ"`</span><span class="typ-punct">`:`</span>` a`<span class="typ-punct">`,`</span>` b`<span class="typ-punct">`,`</span>` c` | [Scripting](/reference/scripting/#modules) |
| Comment | <span class="typ-comment">`/* block */`</span>, <span class="typ-comment">`// line`</span> | [Below](#comments) |

## Comments

Comments are ignored by Typst and will not be included in the output.
This is useful to exclude old versions or to add annotations. To comment
out a single line, start it with `//`:

<div class="previewed-code">

    // our data barely supports
    // this claim

    We show with $p < 0.05$
    that the difference is
    significant.

<div class="preview">

![Preview](/assets/aa63c9c9fd83801f26f5ba5d0dc73151.png)

</div>

</div>

Comments can also be wrapped between `/*` and `*/`. In this case, the
comment can span over multiple lines:

<div class="previewed-code">

    Our study design is as follows:
    /* Somebody write this up:
       - 1000 participants.
       - 2x2 data design. */

<div class="preview">

![Preview](/assets/d1b7773edfcc1952006a027c9e9b8c30.png)

</div>

</div>

## Escape sequences

Escape sequences are used to insert special characters that are hard to
type or otherwise have special meaning in Typst. To escape a character,
precede it with a backslash. To insert any Unicode codepoint, you can
write a hexadecimal escape sequence:
<span class="typ-escape">`\u{1f600}`</span>. The same kind of escape
sequences also work in [strings](/reference/foundations/str/).

<div class="previewed-code">

    I got an ice cream for
    \$1.50! \u{1f600}

<div class="preview">

![Preview](/assets/d87ab5c15ab42543dde046ab1ad05951.png)

</div>

</div>

## Paths

Typst has various features that require a file path to reference
external resources such as images, Typst files, or data files. Paths are
represented as [strings](/reference/foundations/str/). There are two
kinds of paths: Relative and absolute.

- A **relative path** searches from the location of the Typst file where
  the feature is invoked. It is the default:

      #image("images/logo.png")

- An **absolute path** searches from the *root* of the project. It
  starts with a leading `/`:

      #image("/assets/logo.png")

### Project root

By default, the project root is the parent directory of the main Typst
file. For security reasons, you cannot read any files outside of the
root directory.

If you want to set a specific folder as the root of your project, you
can use the CLI's `--root` flag. Make sure that the main file is
contained in the folder's subtree!

```
typst compile --root .. file.typ
```

In the web app, the project itself is the root directory. You can always
read all files within it, no matter which one is previewed (via the eye
toggle next to each Typst file in the file panel).

### Paths and packages

A package can only load files from its own directory. Within it,
absolute paths point to the package root, rather than the project root.
For this reason, it cannot directly load files from the project
directory. If a package needs resources from the project (such as a logo
image), you must pass the already loaded image, e.g. as a named
parameter
`logo: `<span class="typ-func">`image`</span><span class="typ-punct">`(`</span><span class="typ-str">`"mylogo.svg"`</span><span class="typ-punct">`)`</span>.
Note that you can then still customize the image's appearance with a set
rule within the package.

In the future, paths might become a [distinct type from
strings](https://github.com/typst/typst/issues/971), so that they can
retain knowledge of where they were constructed. This way, resources
could be loaded from a different root.
