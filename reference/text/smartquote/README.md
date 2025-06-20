
# smartquote

```
smartquote(
    double: bool
    enabled: bool
    alternative: bool
    quotes: auto str array dictionary
) -> content
```
A language-aware quote that reacts to its context.

Automatically turns into an appropriate opening or closing quote based
on the active [text language](/reference/text/text/#parameters-lang).

## Example

<div class="previewed-code">

    "This is in quotes."

    #set text(lang: "de")
    "Das ist in Anführungszeichen."

    #set text(lang: "fr")
    "C'est entre guillemets."

<div class="preview">

![Preview](/assets/761ad48d2c02ddc1fc5485afa655abcf.png)

</div>

</div>

## Syntax

This function also has dedicated syntax: The normal quote characters
(`'` and `"`). Typst automatically makes your quotes smart.


### Parameters


### double: bool | _named_

Whether this should be a double quote.


### enabled: bool | _named_

Whether smart quotes are enabled.

To disable smartness for a single quote, you can also escape it with a
backslash.


#### Example

<div class="previewed-code">

    #set smartquote(enabled: false)

    These are "dumb" quotes.

<div class="preview">

![Preview](/assets/ca479e14f027381340c262d7483c53a8.png)

</div>

</div>


### alternative: bool | _named_

Whether to use alternative quotes.

Does nothing for languages that don't have alternative quotes, or if
explicit quotes were set.


#### Example

<div class="previewed-code">

    #set text(lang: "de")
    #set smartquote(alternative: true)

    "Das ist in anderen Anführungszeichen."

<div class="preview">

![Preview](/assets/9724cf371363233c8525ba7e26504ca6.png)

</div>

</div>


### quotes: auto, str, array, dictionary | _named_

The quotes to use.

- When set to <span class="typ-key">`auto`</span>, the appropriate
  single quotes for the [text
  language](/reference/text/text/#parameters-lang) will be used. This is
  the default.
- Custom quotes can be passed as a string, array, or dictionary of
  either
  - [string](/reference/foundations/str/): a string consisting of two
    characters containing the opening and closing double quotes
    (characters here refer to Unicode grapheme clusters)
  - [array](/reference/foundations/array/ "array"): an array containing
    the opening and closing double quotes
  - [dictionary](/reference/foundations/dictionary/ "dictionary"): an
    array containing the double and single quotes, each specified as
    either <span class="typ-key">`auto`</span>, string, or array


#### Example

<div class="previewed-code">

    #set text(lang: "de")
    'Das sind normale Anführungszeichen.'

    #set smartquote(quotes: "()")
    "Das sind eigene Anführungszeichen."

    #set smartquote(quotes: (single: ("[[", "]]"),  double: auto))
    'Das sind eigene Anführungszeichen.'

<div class="preview">

![Preview](/assets/6d2a84fef7df6d07d316017d717d89e8.png)

</div>

</div>

