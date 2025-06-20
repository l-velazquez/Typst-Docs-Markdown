# Scripting

Typst embeds a powerful scripting language. You can automate your
documents and create more sophisticated styles with code. Below is an
overview over the scripting concepts.

## Expressions

In Typst, markup and code are fused into one. All but the most common
elements are created with *functions.* To make this as convenient as
possible, Typst provides compact syntax to embed a code expression into
markup: An expression is introduced with a hash (`#`) and normal markup
parsing resumes after the expression is finished. If a character would
continue the expression but should be interpreted as text, the
expression can forcibly be ended with a semicolon (`;`).

<div class="previewed-code">

    #emph[Hello] \
    #emoji.face \
    #"hello".len()

<div class="preview">

![Preview](/assets/56fcebfd54e87e06f0936777ca6c4f31.png)

</div>

</div>

The example above shows a few of the available expressions, including
[function calls](/reference/foundations/function/), [field
accesses](/reference/scripting/#fields), and [method
calls](/reference/scripting/#methods). More kinds of expressions are
discussed in the remainder of this chapter. A few kinds of expressions
are not compatible with the hash syntax (e.g. binary operator
expressions). To embed these into markup, you can use parentheses, as in
<span class="typ-punct">`#`</span><span class="typ-punct">`(`</span><span class="typ-num">`1`</span>` `<span class="typ-op">`+`</span>` `<span class="typ-num">`2`</span><span class="typ-punct">`)`</span>.

## Blocks

To structure your code and embed markup into it, Typst provides two
kinds of *blocks:*

- **Code block:**
  <span class="typ-punct">`{`</span>` `<span class="typ-key">`let`</span>` x `<span class="typ-op">`=`</span>` `<span class="typ-num">`1`</span><span class="typ-punct">`;`</span>` x `<span class="typ-op">`+`</span>` `<span class="typ-num">`2`</span>` `<span class="typ-punct">`}`</span>  
  When writing code, you'll probably want to split up your computation
  into multiple statements, create some intermediate variables and so
  on. Code blocks let you write multiple expressions where one is
  expected. The individual expressions in a code block should be
  separated by line breaks or semicolons. The output values of the
  individual expressions in a code block are joined to determine the
  block's value. Expressions without useful output, like
  <span class="typ-key">`let`</span> bindings yield
  <span class="typ-key">`none`</span>, which can be joined with any
  value without effect.

- **Content block:**
  <span class="typ-punct">`[`</span><span class="typ-strong">`*Hey*`</span>` there!`<span class="typ-punct">`]`</span>  
  With content blocks, you can handle markup/content as a programmatic
  value, store it in variables and pass it to
  [functions](/reference/foundations/function/). Content blocks are
  delimited by square brackets and can contain arbitrary markup. A
  content block results in a value of type
  [content](/reference/foundations/content/ "content"). An arbitrary
  number of content blocks can be passed as trailing arguments to
  functions. That is,
  <span class="typ-func">`list`</span><span class="typ-punct">`(`</span><span class="typ-punct">`[`</span>`A`<span class="typ-punct">`]`</span><span class="typ-punct">`,`</span>` `<span class="typ-punct">`[`</span>`B`<span class="typ-punct">`]`</span><span class="typ-punct">`)`</span>
  is equivalent to
  <span class="typ-func">`list`</span><span class="typ-punct">`[`</span>`A`<span class="typ-punct">`]`</span><span class="typ-punct">`[`</span>`B`<span class="typ-punct">`]`</span>.

Content and code blocks can be nested arbitrarily. In the example below,
<span class="typ-punct">`[`</span>`hello `<span class="typ-punct">`]`</span>
is joined with the output of
`a `<span class="typ-op">`+`</span>` `<span class="typ-punct">`[`</span>` the `<span class="typ-punct">`]`</span>` `<span class="typ-op">`+`</span>` b`
yielding
<span class="typ-punct">`[`</span>`hello from the `<span class="typ-strong">`*world*`</span><span class="typ-punct">`]`</span>.

<div class="previewed-code">

    #{
      let a = [from]
      let b = [*world*]
      [hello ]
      a + [ the ] + b
    }

<div class="preview">

![Preview](/assets/f5f1a59a923ddd7899e3844457f683a1.png)

</div>

</div>

## Bindings and Destructuring

As already demonstrated above, variables can be defined with
<span class="typ-key">`let`</span> bindings. The variable is assigned
the value of the expression that follows the `=` sign. The assignment of
a value is optional, if no value is assigned, the variable will be
initialized as <span class="typ-key">`none`</span>. The
<span class="typ-key">`let`</span> keyword can also be used to create a
[custom named
function](/reference/foundations/function/#defining-functions).
Variables can be accessed for the rest of the containing block (or the
rest of the file if there is no containing block).

<div class="previewed-code">

    #let name = "Typst"
    This is #name's documentation.
    It explains #name.

    #let add(x, y) = x + y
    Sum is #add(2, 3).

<div class="preview">

![Preview](/assets/cab2fd22fe9abd4d4b827c1bc30aee2f.png)

</div>

</div>

Let bindings can also be used to destructure
[arrays](/reference/foundations/array/) and
[dictionaries](/reference/foundations/dictionary/). In this case, the
left-hand side of the assignment should mirror an array or dictionary.
The `..` operator can be used once in the pattern to collect the
remainder of the array's or dictionary's items.

<div class="previewed-code">

    #let (x, y) = (1, 2)
    The coordinates are #x, #y.

    #let (a, .., b) = (1, 2, 3, 4)
    The first element is #a.
    The last element is #b.

    #let books = (
      Shakespeare: "Hamlet",
      Homer: "The Odyssey",
      Austen: "Persuasion",
    )

    #let (Austen,) = books
    Austen wrote #Austen.

    #let (Homer: h) = books
    Homer wrote #h.

    #let (Homer, ..other) = books
    #for (author, title) in other [
      #author wrote #title.
    ]

<div class="preview">

![Preview](/assets/574a8a54d94246e011156a58bb988f10.png)

</div>

</div>

You can use the underscore to discard elements in a destructuring
pattern:

<div class="previewed-code">

    #let (_, y, _) = (1, 2, 3)
    The y coordinate is #y.

<div class="preview">

![Preview](/assets/2d320f557a31c13c47827649626f615e.png)

</div>

</div>

Destructuring also works in argument lists of functions ...

<div class="previewed-code">

    #let left = (2, 4, 5)
    #let right = (3, 2, 6)
    #left.zip(right).map(
      ((a,b)) => a + b
    )

<div class="preview">

![Preview](/assets/eb451d0a1cf36461e8a56ce203acf067.png)

</div>

</div>

... and on the left-hand side of normal assignments. This can be useful
to swap variables among other things.

<div class="previewed-code">

    #{
      let a = 1
      let b = 2
      (a, b) = (b, a)
      [a = #a, b = #b]
    }

<div class="preview">

![Preview](/assets/2c2bcc6a2509a95daa0bc4e986ee7e6d.png)

</div>

</div>

## Conditionals

With a conditional, you can display or compute different things
depending on whether some condition is fulfilled. Typst supports
<span class="typ-key">`if`</span>,
`else `<span class="typ-key">`if`</span> and `else` expressions. When
the condition evaluates to <span class="typ-key">`true`</span>, the
conditional yields the value resulting from the if's body, otherwise
yields the value resulting from the else's body.

<div class="previewed-code">

    #if 1 < 2 [
      This is shown
    ] else [
      This is not.
    ]

<div class="preview">

![Preview](/assets/9f03dfe97f385ab1a6d01127a9152c4d.png)

</div>

</div>

Each branch can have a code or content block as its body.

- <span class="typ-key">`if`</span>` condition `<span class="typ-punct">`{`</span>`..`<span class="typ-punct">`}`</span>
- <span class="typ-key">`if`</span>` condition `<span class="typ-punct">`[`</span>`..`<span class="typ-punct">`]`</span>
- <span class="typ-key">`if`</span>` condition `<span class="typ-punct">`[`</span>`..`<span class="typ-punct">`]`</span>` `<span class="typ-key">`else`</span>` `<span class="typ-punct">`{`</span>`..`<span class="typ-punct">`}`</span>
- <span class="typ-key">`if`</span>` condition `<span class="typ-punct">`[`</span>`..`<span class="typ-punct">`]`</span>` `<span class="typ-key">`else`</span>` `<span class="typ-key">`if`</span>` condition `<span class="typ-punct">`{`</span>`..`<span class="typ-punct">`}`</span>` `<span class="typ-key">`else`</span>` `<span class="typ-punct">`[`</span>`..`<span class="typ-punct">`]`</span>

## Loops

With loops, you can repeat content or compute something iteratively.
Typst supports two types of loops: <span class="typ-key">`for`</span>
and <span class="typ-key">`while`</span> loops. The former iterate over
a specified collection whereas the latter iterate as long as a condition
stays fulfilled. Just like blocks, loops *join* the results from each
iteration into one value.

In the example below, the three sentences created by the for loop join
together into a single content value and the length-1 arrays in the
while loop join together into one larger array.

<div class="previewed-code">

    #for c in "ABC" [
      #c is a letter.
    ]

    #let n = 2
    #while n < 10 {
      n = (n * 2) - 1
      (n,)
    }

<div class="preview">

![Preview](/assets/ef87ec09b6f156465a2deb8f2ca4620b.png)

</div>

</div>

For loops can iterate over a variety of collections:

- <span class="typ-key">`for`</span>` value `<span class="typ-key">`in`</span>` array `<span class="typ-punct">`{`</span>`..`<span class="typ-punct">`}`</span>  
  Iterates over the items in the
  [array](/reference/foundations/array/ "array"). The destructuring
  syntax described in [Let binding](/reference/scripting/#bindings) can
  also be used here.

- <span class="typ-key">`for`</span>` pair `<span class="typ-key">`in`</span>` dict `<span class="typ-punct">`{`</span>`..`<span class="typ-punct">`}`</span>  
  Iterates over the key-value pairs of the
  [dictionary](/reference/foundations/dictionary/ "dictionary"). The
  pairs can also be destructured by using
  <span class="typ-key">`for`</span>` `<span class="typ-punct">`(`</span>`key`<span class="typ-punct">`,`</span>` value`<span class="typ-punct">`)`</span>` `<span class="typ-key">`in`</span>` dict `<span class="typ-punct">`{`</span>`..`<span class="typ-punct">`}`</span>.
  It is more efficient than
  <span class="typ-key">`for`</span>` pair `<span class="typ-key">`in`</span>` dict`<span class="typ-punct">`.`</span><span class="typ-func">`pairs`</span><span class="typ-punct">`(`</span><span class="typ-punct">`)`</span>` `<span class="typ-punct">`{`</span>`..`<span class="typ-punct">`}`</span>
  because it doesn't create a temporary array of all key-value pairs.

- <span class="typ-key">`for`</span>` letter `<span class="typ-key">`in`</span>` `<span class="typ-str">`"abc"`</span>` `<span class="typ-punct">`{`</span>`..`<span class="typ-punct">`}`</span>  
  Iterates over the characters of the
  [string](/reference/foundations/str/). Technically, it iterates over
  the grapheme clusters of the string. Most of the time, a grapheme
  cluster is just a single codepoint. However, a grapheme cluster could
  contain multiple codepoints, like a flag emoji.

- <span class="typ-key">`for`</span>` byte `<span class="typ-key">`in`</span>` `<span class="typ-func">`bytes`</span><span class="typ-punct">`(`</span><span class="typ-str">`"😀"`</span><span class="typ-punct">`)`</span>` `<span class="typ-punct">`{`</span>`..`<span class="typ-punct">`}`</span>  
  Iterates over the [bytes](/reference/foundations/bytes/ "bytes"),
  which can be converted from a [string](/reference/foundations/str/) or
  [read](/reference/data-loading/read/ "read") from a file without
  encoding. Each byte value is an [integer](/reference/foundations/int/)
  between <span class="typ-num">`0`</span> and
  <span class="typ-num">`255`</span>.

To control the execution of the loop, Typst provides the
<span class="typ-key">`break`</span> and
<span class="typ-key">`continue`</span> statements. The former performs
an early exit from the loop while the latter skips ahead to the next
iteration of the loop.

<div class="previewed-code">

    #for letter in "abc nope" {
      if letter == " " {
        break
      }

      letter
    }

<div class="preview">

![Preview](/assets/8ba145cb687a39c8f9146abd55f943f9.png)

</div>

</div>

The body of a loop can be a code or content block:

- <span class="typ-key">`for`</span>` .. in collection `<span class="typ-punct">`{`</span>`..`<span class="typ-punct">`}`</span>
- <span class="typ-key">`for`</span>` .. in collection `<span class="typ-punct">`[`</span>`..`<span class="typ-punct">`]`</span>
- <span class="typ-key">`while`</span>` condition `<span class="typ-punct">`{`</span>`..`<span class="typ-punct">`}`</span>
- <span class="typ-key">`while`</span>` condition `<span class="typ-punct">`[`</span>`..`<span class="typ-punct">`]`</span>

## Fields

You can use *dot notation* to access fields on a value. For values of
type [`content`](/reference/foundations/content/ "`content`"), you can
also use the
[`fields`](/reference/foundations/content/#definitions-fields) function
to list the fields.

The value in question can be either:

- a [dictionary](/reference/foundations/dictionary/ "dictionary") that
  has the specified key,
- a [symbol](/reference/foundations/symbol/ "symbol") that has the
  specified modifier,
- a [module](/reference/foundations/module/ "module") containing the
  specified definition,
- [content](/reference/foundations/content/ "content") consisting of an
  element that has the specified field. The available fields match the
  arguments of the [element
  function](/reference/foundations/function/#element-functions) that
  were given when the element was constructed.

<div class="previewed-code">

    #let it = [= Heading]
    #it.body \
    #it.depth \
    #it.fields()

    #let dict = (greet: "Hello")
    #dict.greet \
    #emoji.face

<div class="preview">

![Preview](/assets/e560cf75c003b55ee615a91fba54908a.png)

</div>

</div>

## Methods

A *method call* is a convenient way to call a function that is scoped to
a value's [type](/reference/foundations/type/ "type"). For example, we
can call the [`str.len`](/reference/foundations/str/#definitions-len)
function in the following two equivalent ways:

<div class="previewed-code">

    #str.len("abc") is the same as
    #"abc".len()

<div class="preview">

![Preview](/assets/8fc9134962ea2ca6f8f3beaa1a77c940.png)

</div>

</div>

The structure of a method call is
`value`<span class="typ-punct">`.`</span><span class="typ-func">`method`</span><span class="typ-punct">`(`</span><span class="typ-op">`..`</span>`args`<span class="typ-punct">`)`</span>
and its equivalent full function call is
<span class="typ-func">`type`</span><span class="typ-punct">`(`</span>`value`<span class="typ-punct">`)`</span><span class="typ-punct">`.`</span><span class="typ-func">`method`</span><span class="typ-punct">`(`</span>`value`<span class="typ-punct">`,`</span>` `<span class="typ-op">`..`</span>`args`<span class="typ-punct">`)`</span>.
The documentation of each type lists its scoped functions. You cannot
currently define your own methods.

<div class="previewed-code">

    #let values = (1, 2, 3, 4)
    #values.pop() \
    #values.len() \

    #("a, b, c"
        .split(", ")
        .join[ --- ])

    #"abc".len() is the same as
    #str.len("abc")

<div class="preview">

![Preview](/assets/69c81d74d21d4e212b8bdde97b02c949.png)

</div>

</div>

There are a few special functions that modify the value they are called
on (e.g.
[`array.push`](/reference/foundations/array/#definitions-push)). These
functions *must* be called in method form. In some cases, when the
method is only called for its side effect, its return value should be
ignored (and not participate in joining). The canonical way to discard a
value is with a let binding:
<span class="typ-key">`let`</span>` _ `<span class="typ-op">`=`</span>` array`<span class="typ-punct">`.`</span><span class="typ-func">`remove`</span><span class="typ-punct">`(`</span><span class="typ-num">`1`</span><span class="typ-punct">`)`</span>.

## Modules

You can split up your Typst projects into multiple files called
*modules.* A module can refer to the content and definitions of another
module in multiple ways:

- **Including:**
  <span class="typ-key">`include`</span>` `<span class="typ-str">`"bar.typ"`</span>  
  Evaluates the file at the path `bar.typ` and returns the resulting
  [content](/reference/foundations/content/ "content").

- **Import:**
  <span class="typ-key">`import`</span>` `<span class="typ-str">`"bar.typ"`</span>  
  Evaluates the file at the path `bar.typ` and inserts the resulting
  [module](/reference/foundations/module/ "module") into the current
  scope as `bar` (filename without extension). You can use the `as`
  keyword to rename the imported module:
  <span class="typ-key">`import`</span>` `<span class="typ-str">`"bar.typ"`</span>` `<span class="typ-key">`as`</span>` baz`.
  You can import nested items using dot notation:
  <span class="typ-key">`import`</span>` `<span class="typ-str">`"bar.typ"`</span><span class="typ-punct">`:`</span>` baz`<span class="typ-punct">`.`</span>`a`.

- **Import items:**
  <span class="typ-key">`import`</span>` `<span class="typ-str">`"bar.typ"`</span><span class="typ-punct">`:`</span>` a`<span class="typ-punct">`,`</span>` b`  
  Evaluates the file at the path `bar.typ`, extracts the values of the
  variables `a` and `b` (that need to be defined in `bar.typ`, e.g.
  through <span class="typ-key">`let`</span> bindings) and defines them
  in the current file. Replacing `a, b` with `*` loads all variables
  defined in a module. You can use the `as` keyword to rename the
  individual items:
  <span class="typ-key">`import`</span>` `<span class="typ-str">`"bar.typ"`</span><span class="typ-punct">`:`</span>` a `<span class="typ-key">`as`</span>` one`<span class="typ-punct">`,`</span>` b `<span class="typ-key">`as`</span>` two`

Instead of a path, you can also use a [module
value](/reference/foundations/module/), as shown in the following
example:

<div class="previewed-code">

    #import emoji: face
    #face.grin

<div class="preview">

![Preview](/assets/9c38d95483bccbf7479a82427087ab2a.png)

</div>

</div>

## Packages

To reuse building blocks across projects, you can also create and import
Typst *packages.* A package import is specified as a triple of a
namespace, a name, and a version.

<div class="previewed-code">

    #import "@preview/example:0.1.0": add
    #add(2, 7)

<div class="preview">

![Preview](/assets/3d994560e3517e38057aec147c441de6.png)

</div>

</div>

The `preview` namespace contains packages shared by the community. You
can find all available community packages on [Typst
Universe](https://typst.app/universe/).

If you are using Typst locally, you can also create your own
system-local packages. For more details on this, see the [package
repository](https://github.com/typst/packages).

## Operators

The following table lists all available unary and binary operators with
effect, arity (unary, binary) and precedence level (higher binds
stronger). Some operations, such as
[modulus](/reference/foundations/calc/#functions-rem-euclid), do not
have a special syntax and can be achieved using functions from the
[`calc`](/reference/foundations/calc/) module.

| Operator | Effect | Arity | Precedence |
|:--:|----|:--:|:--:|
| <span class="typ-op">`-`</span> | Negation | Unary | 7 |
| <span class="typ-op">`+`</span> | No effect (exists for symmetry) | Unary | 7 |
| `*` | Multiplication | Binary | 6 |
| `/` | Division | Binary | 6 |
| <span class="typ-op">`+`</span> | Addition | Binary | 5 |
| <span class="typ-op">`-`</span> | Subtraction | Binary | 5 |
| `==` | Check equality | Binary | 4 |
| `!=` | Check inequality | Binary | 4 |
| `<` | Check less-than | Binary | 4 |
| `<=` | Check less-than or equal | Binary | 4 |
| `>` | Check greater-than | Binary | 4 |
| `>=` | Check greater-than or equal | Binary | 4 |
| `in` | Check if in collection | Binary | 4 |
| <span class="typ-key">`not`</span>` `<span class="typ-key">`in`</span> | Check if not in collection | Binary | 4 |
| <span class="typ-key">`not`</span> | Logical "not" | Unary | 3 |
| `and` | Short-circuiting logical "and" | Binary | 3 |
| `or` | Short-circuiting logical "or" | Binary | 2 |
| `=` | Assignment | Binary | 1 |
| `+=` | Add-Assignment | Binary | 1 |
| `-=` | Subtraction-Assignment | Binary | 1 |
| `*=` | Multiplication-Assignment | Binary | 1 |
| `/=` | Division-Assignment | Binary | 1 |
