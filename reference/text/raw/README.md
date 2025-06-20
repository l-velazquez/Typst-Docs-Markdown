
# raw

```
raw(
    str
    block: bool
    lang: none str
    align: alignment
    syntaxes: str bytes array
    theme: none auto str bytes
    tab-size: int
) -> content
```
Raw text with optional syntax highlighting.

Displays the text verbatim and in a monospace font. This is typically
used to embed computer code into your document.

## Example

<div class="previewed-code">

    Adding `rbx` to `rcx` gives
    the desired result.

    What is ```rust fn main()``` in Rust
    would be ```c int main()``` in C.

    ```rust
    fn main() {
        println!("Hello World!");
    }
    ```

    This has ``` `backticks` ``` in it
    (but the spaces are trimmed). And
    ``` here``` the leading space is
    also trimmed.

<div class="preview">

![Preview](/assets/1c6e6aa444c644eee774123542b7a4f6.png)

</div>

</div>

You can also construct a [`raw`](/reference/text/raw/ "`raw`") element
programmatically from a string (and provide the language tag via the
optional [`lang`](/reference/text/raw/#parameters-lang) argument).

<div class="previewed-code">

    #raw("fn " + "main() {}", lang: "rust")

<div class="preview">

![Preview](/assets/30d00188c2b14f13cf697cc8c1fb8f3d.png)

</div>

</div>

## Syntax

This function also has dedicated syntax. You can enclose text in 1 or 3+
backticks (`` ` ``) to make it raw. Two backticks produce empty raw
text. This works both in markup and code.

When you use three or more backticks, you can additionally specify a
language tag for syntax highlighting directly after the opening
backticks. Within raw blocks, everything (except for the language tag,
if applicable) is rendered as is, in particular, there are no escape
sequences.

The language tag is an identifier that directly follows the opening
backticks only if there are three or more backticks. If your text starts
with something that looks like an identifier, but no syntax highlighting
is needed, start the text with a single space (which will be trimmed) or
use the single backtick syntax. If your text should start or end with a
backtick, put a space before or after it (it will be trimmed).


### Parameters


### text: str | _required_ _positional_

The raw text.

You can also use raw blocks creatively to create custom syntaxes for
your automations.


#### Example

<div class="previewed-code">

    // Parse numbers in raw blocks with the
    // `mydsl` tag and sum them up.
    #show raw.where(lang: "mydsl"): it => {
      let sum = 0
      for part in it.text.split("+") {
        sum += int(part.trim())
      }
      sum
    }

    ```mydsl
    1 + 2 + 3 + 4 + 5
    ```

<div class="preview">

![Preview](/assets/e95a5eae34283fc132d0b8949399b41d.png)

</div>

</div>


### block: bool | _named_

Whether the raw text is displayed as a separate block.

In markup mode, using one-backtick notation makes this
<span class="typ-key">`false`</span>. Using three-backtick notation
makes it <span class="typ-key">`true`</span> if the enclosed content
contains at least one line break.


#### Example

<div class="previewed-code">

    // Display inline code in a small box
    // that retains the correct baseline.
    #show raw.where(block: false): box.with(
      fill: luma(240),
      inset: (x: 3pt, y: 0pt),
      outset: (y: 3pt),
      radius: 2pt,
    )

    // Display block code in a larger block
    // with more padding.
    #show raw.where(block: true): block.with(
      fill: luma(240),
      inset: 10pt,
      radius: 4pt,
    )

    With `rg`, you can search through your files quickly.
    This example searches the current directory recursively
    for the text `Hello World`:

    ```bash
    rg "Hello World"
    ```

<div class="preview">

![Preview](/assets/3e05c29a6af60a7e77667a5640e9ccc3.png)

</div>

</div>


### lang: none, str | _named_

The language to syntax-highlight in.

Apart from typical language tags known from Markdown, this supports the
<span class="typ-str">`"typ"`</span>,
<span class="typ-str">`"typc"`</span>, and
<span class="typ-str">`"typm"`</span> tags for [Typst
markup](/reference/syntax/#markup), [Typst
code](/reference/syntax/#code), and [Typst
math](/reference/syntax/#math), respectively.


#### Example

<div class="previewed-code">

    ```typ
    This is *Typst!*
    ```

    This is ```typ also *Typst*```, but inline!

<div class="preview">

![Preview](/assets/6e35373cc945b3d9ac522ef64138479c.png)

</div>

</div>


### align: alignment | _named_

The horizontal alignment that each line in a raw block should have. This
option is ignored if this is not a raw block (if specified
`block: false` or single backticks were used in markup mode).

By default, this is set to `start`, meaning that raw text is aligned
towards the start of the text direction inside the block by default,
regardless of the current context's alignment (allowing you to center
the raw block itself without centering the text inside it, for example).


#### Example

<div class="previewed-code">

    #set raw(align: center)

    ```typc
    let f(x) = x
    code = "centered"
    ```

<div class="preview">

![Preview](/assets/42863ad475a373b308500053afc9afc3.png)

</div>

</div>


### syntaxes: str, bytes, array | _named_

Additional syntax definitions to load. The syntax definitions should be
in the [`sublime-syntax` file
format](https://www.sublimetext.com/docs/syntax.html).

You can pass any of the following values:

- A path string to load a syntax file from the given path. For more
  details about paths, see the [Paths
  section](/reference/syntax/#paths).
- Raw bytes from which the syntax should be decoded.
- An array where each item is one of the above.


#### Example

<div class="previewed-code">

    #set raw(syntaxes: "SExpressions.sublime-syntax")

    ```sexp
    (defun factorial (x)
      (if (zerop x)
        ; with a comment
        1
        (* x (factorial (- x 1)))))
    ```

<div class="preview">

![Preview](/assets/7f5c04b4a7636eec32f8b54d18867f8a.png)

</div>

</div>


### theme: none, auto, str, bytes | _named_

The theme to use for syntax highlighting. Themes should be in the
[`tmTheme` file
format](https://www.sublimetext.com/docs/color_schemes_tmtheme.html).

You can pass any of the following values:

- <span class="typ-key">`none`</span>: Disables syntax highlighting.
- <span class="typ-key">`auto`</span>: Highlights with Typst's default
  theme.
- A path string to load a theme file from the given path. For more
  details about paths, see the [Paths
  section](/reference/syntax/#paths).
- Raw bytes from which the theme should be decoded.

Applying a theme only affects the color of specifically highlighted
text. It does not consider the theme's foreground and background
properties, so that you retain control over the color of raw text. You
can apply the foreground color yourself with the
[`text`](/reference/text/text/ "`text`") function and the background
with a [filled block](/reference/layout/block/#parameters-fill). You
could also use the [`xml`](/reference/data-loading/xml/ "`xml`")
function to extract these properties from the theme.


#### Example

<div class="previewed-code">

    #set raw(theme: "halcyon.tmTheme")
    #show raw: it => block(
      fill: rgb("#1d2433"),
      inset: 8pt,
      radius: 5pt,
      text(fill: rgb("#a2aabc"), it)
    )

    ```typ
    = Chapter 1
    #let hi = "Hello World"
    ```

<div class="preview">

![Preview](/assets/ff79dd534cb52ac3a90c032ff7df46c3.png)

</div>

</div>


### tab-size: int | _named_

The size for a tab stop in spaces. A tab is replaced with enough spaces
to align with the next multiple of the size.


#### Example

<div class="previewed-code">

    #set raw(tab-size: 8)
    ```tsv
    Year    Month   Day
    2000    2   3
    2001    2   1
    2002    3   10
    ```

<div class="preview">

![Preview](/assets/38037df252d0e30521ad3ae36d5093cb.png)

</div>

</div>


## Definitions


### line

```
raw.line(
    int
    int
    str
    content
) -> content
```
A highlighted line of raw text.

This is a helper element that is synthesized by
[`raw`](/reference/text/raw/ "`raw`") elements.

It allows you to access various properties of the line, such as the line
number, the raw non-highlighted text, the highlighted text, and whether
it is the first or last line of the raw block.


##### Parameters


##### number: int | _required_ _positional_

The line number of the raw line inside of the raw block, starts at 1.


##### count: int | _required_ _positional_

The total number of lines in the raw block.


##### text: str | _required_ _positional_

The line of raw text.


##### body: content | _required_ _positional_

The highlighted raw text.

