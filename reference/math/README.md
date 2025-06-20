Typst has special [syntax](/reference/syntax/#math) and library
functions to typeset mathematical formulas. Math formulas can be
displayed inline with text or as separate blocks. They will be typeset
into their own block if they start and end with at least one space (e.g.
<span class="typ-math-delim">`$`</span>` x`<span class="typ-math-op">`^`</span>`2 `<span class="typ-math-delim">`$`</span>).

## Variables

In math, single letters are always displayed as is. Multiple letters,
however, are interpreted as variables and functions. To display multiple
letters verbatim, you can place them into quotes and to access single
letter variables, you can use the [hash
syntax](/reference/scripting/#expressions).

<div class="previewed-code">

    $ A = pi r^2 $
    $ "area" = pi dot "radius"^2 $
    $ cal(A) :=
        { x in RR | x "is natural" } $
    #let x = 5
    $ #x < 17 $

<div class="preview">

![Preview](/assets/8524e76a7c6784dd9c30bb62d92a4897.png)

</div>

</div>

## Symbols

Math mode makes a wide selection of [symbols](/reference/symbols/sym/)
like `pi`, `dot`, or `RR` available. Many mathematical symbols are
available in different variants. You can select between different
variants by applying [modifiers](/reference/foundations/symbol/) to the
symbol. Typst further recognizes a number of shorthand sequences like
`=>` that approximate a symbol. When such a shorthand exists, the
symbol's documentation lists it.

<div class="previewed-code">

    $ x < y => x gt.eq.not y $

<div class="preview">

![Preview](/assets/dd08c3941abc7b8b1c9310fbebf71b6e.png)

</div>

</div>

## Line Breaks

Formulas can also contain line breaks. Each line can contain one or
multiple *alignment points* (`&`) which are then aligned.

<div class="previewed-code">

    $ sum_(k=0)^n k
        &= 1 + ... + n \
        &= (n(n+1)) / 2 $

<div class="preview">

![Preview](/assets/e18e117e8b98666dc9823bbeed6dd264.png)

</div>

</div>

## Function calls

Math mode supports special function calls without the hash prefix. In
these "math calls", the argument list works a little differently than in
code:

- Within them, Typst is still in "math mode". Thus, you can write math
  directly into them, but need to use hash syntax to pass code
  expressions (except for strings, which are available in the math
  syntax).
- They support positional and named arguments, as well as argument
  spreading.
- They don't support trailing content blocks.
- They provide additional syntax for 2-dimensional argument lists. The
  semicolon (`;`) merges preceding arguments separated by commas into an
  array argument.

<div class="previewed-code">

    $ frac(a^2, 2) $
    $ vec(1, 2, delim: "[") $
    $ mat(1, 2; 3, 4) $
    $ mat(..#range(1, 5).chunks(2)) $
    $ lim_x =
        op("lim", limits: #true)_x $

<div class="preview">

![Preview](/assets/a04e7f595e2b6bd62e8eb21bcf63a042.png)

</div>

</div>

To write a verbatim comma or semicolon in a math call, escape it with a
backslash. The colon on the other hand is only recognized in a special
way if directly preceded by an identifier, so to display it verbatim in
those cases, you can just insert a space before it.

Functions calls preceded by a hash are normal code function calls and
not affected by these rules.

## Alignment

When equations include multiple *alignment points* (`&`), this creates
blocks of alternatingly right- and left-aligned columns. In the example
below, the expression `(3x + y) / 7` is right-aligned and `= 9` is
left-aligned. The word "given" is also left-aligned because `&&` creates
two alignment points in a row, alternating the alignment twice. `& &`
and `&&` behave exactly the same way. Meanwhile, "multiply by 7" is
right-aligned because just one `&` precedes it. Each alignment point
simply alternates between right-aligned/left-aligned.

<div class="previewed-code">

    $ (3x + y) / 7 &= 9 && "given" \
      3x + y &= 63 & "multiply by 7" \
      3x &= 63 - y && "subtract y" \
      x &= 21 - y/3 & "divide by 3" $

<div class="preview">

![Preview](/assets/f1233da95c9167f12592cfc2f7cf3674.png)

</div>

</div>

## Math fonts

You can set the math font by with a [show-set
rule](/reference/styling/#show-rules) as demonstrated below. Note that
only special OpenType math fonts are suitable for typesetting maths.

<div class="previewed-code">

    #show math.equation: set text(font: "Fira Math")
    $ sum_(i in NN) 1 + i $

<div class="preview">

![Preview](/assets/a86f5771fd97e49bb413be94448c5f66.png)

</div>

</div>

## Math module

All math functions are part of the `math`
[module](/reference/scripting/#modules), which is available by default
in equations. Outside of equations, they can be accessed with the
`math.` prefix.

- [accent](/reference/math/accent/) Attaches an accent to a base.
- [attach](/reference/math/attach/) Subscript, superscripts, and limits.
- [binom](/reference/math/binom/) A binomial expression.
- [cancel](/reference/math/cancel/) Displays a diagonal line over a part of an equation.
- [cases](/reference/math/cases/) A case distinction.
- [class](/reference/math/class/) Forced use of a certain math class.
- [equation](/reference/math/equation/) A mathematical equation.
- [frac](/reference/math/frac/) A mathematical fraction.
- [lr](/reference/math/lr/) Delimiter matching.
- [mat](/reference/math/mat/) A matrix.
- [op](/reference/math/op/) A text operator in an equation.
- [primes](/reference/math/primes/) Grouped primes.
- [roots](/reference/math/roots/) Square and non-square roots.
- [sizes](/reference/math/sizes/) Forced size styles for expressions within formulas.
- [stretch](/reference/math/stretch/) Stretches a glyph.
- [styles](/reference/math/styles/) Alternate letterforms within formulas.
- [underover](/reference/math/underover/) Delimiters above or below parts of an equation.
- [variants](/reference/math/variants/) Alternate typefaces within formulas.
- [vec](/reference/math/vec/) A column vector.
