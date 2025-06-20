
# Regex

A regular expression.

Can be used as a [show rule selector](/reference/styling/#show-rules)
and with [string methods](/reference/foundations/str/) like `find`,
`split`, and `replace`.

[See here](https://docs.rs/regex/latest/regex/#syntax) for a
specification of the supported syntax.

## Example

<div class="previewed-code">

    // Works with string methods.
    #"a,b;c".split(regex("[,;]"))

    // Works with show rules.
    #show regex("\d+"): set text(red)

    The numbers 1 to 10.

<div class="preview">

![Preview](/assets/52d7d724092529d8f2059dc7991c18f8.png)

</div>

</div>


## regex

```
regex(
    str
) -> regex
```
Create a regular expression from a string.


#### Parameters


#### regex: str | _required_ _positional_

The regular expression as a string.

Most regex escape sequences just work because they are not valid Typst
escape sequences. To produce regex escape sequences that are also valid
in Typst (e.g. <span class="typ-escape">`\\`</span>), you need to escape
twice. Thus, to match a verbatim backslash, you would need to write
<span class="typ-func">`regex`</span><span class="typ-punct">`(`</span><span class="typ-str">`"\\\\"`</span><span class="typ-punct">`)`</span>.

If you need many escape sequences, you can also create a raw element and
extract its text to use it for your regular expressions:


##### Example

<span class="typ-func">`regex`</span><span class="typ-punct">`(`</span><span class="typ-raw">`` `\d+\.\d+\.\d+` ``</span><span class="typ-punct">`.`</span>`text`<span class="typ-punct">`)`</span>.


## Definitions

