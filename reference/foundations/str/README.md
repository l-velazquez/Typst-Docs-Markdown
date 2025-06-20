
# String

A sequence of Unicode codepoints.

You can iterate over the grapheme clusters of the string using a [for
loop](/reference/scripting/#loops). Grapheme clusters are basically
characters but keep together things that belong together, e.g. multiple
codepoints that together form a flag emoji. Strings can be added with
the `+` operator, [joined together](/reference/scripting/#blocks) and
multiplied with integers.

Typst provides utility methods for string manipulation. Many of these
methods (e.g., `split`, `trim` and `replace`) operate on *patterns:* A
pattern can be either a string or a [regular
expression](/reference/foundations/regex/). This makes the methods quite
versatile.

All lengths and indices are expressed in terms of UTF-8 bytes. Indices
are zero-based and negative indices wrap around to the end of the
string.

You can convert a value to a string with this type's constructor.

## Example

<div class="previewed-code">

    #"hello world!" \
    #"\"hello\n  world\"!" \
    #"1 2 3".split() \
    #"1,2;3".split(regex("[,;]")) \
    #(regex("\d+") in "ten euros") \
    #(regex("\d+") in "10 euros")

<div class="preview">

![Preview](/assets/80af3d02723d93b772f369bd4771758e.png)

</div>

</div>

## Escape sequences

Just like in markup, you can escape a few symbols in strings:

- <span class="typ-escape">`\\`</span> for a backslash
- <span class="typ-escape">`\"`</span> for a quote
- <span class="typ-escape">`\n`</span> for a newline
- <span class="typ-escape">`\r`</span> for a carriage return
- <span class="typ-escape">`\t`</span> for a tab
- <span class="typ-escape">`\u{1f600}`</span> for a hexadecimal Unicode
  escape sequence


## str

```
str(
    int float str bytes label decimal version type
    base: int
) -> str
```
Converts a value to a string.

- Integers are formatted in base 10. This can be overridden with the
  optional `base` parameter.
- Floats are formatted in base 10 and never in exponential notation.
- Negative integers and floats are formatted with the Unicode minus sign
  ("−" U+2212) instead of the ASCII minus sign ("-" U+002D).
- From labels the name is extracted.
- Bytes are decoded as UTF-8.

If you wish to convert from and to Unicode code points, see the
[`to-unicode`](/reference/foundations/str/#definitions-to-unicode) and
[`from-unicode`](/reference/foundations/str/#definitions-from-unicode)
functions.


#### Parameters


#### value: int, float, str, bytes, label, decimal, version, type | _required_ _positional_

The value that should be converted to a string.


#### base: int | _named_

The base (radix) to display integers in, between 2 and 36.


### Example

<div class="previewed-code">

    #str(10) \
    #str(4000, base: 16) \
    #str(2.7) \
    #str(1e8) \
    #str(<intro>)

<div class="preview">

![Preview](/assets/d3a8d1f73f9f3fe3387aef170763059c.png)

</div>

</div>


## Definitions


### len

```
str.len(
) -> int
```
The length of the string in UTF-8 encoded bytes.


##### Parameters


### first

```
str.first(
) -> str
```
Extracts the first grapheme cluster of the string. Fails with an error
if the string is empty.


##### Parameters


### last

```
str.last(
) -> str
```
Extracts the last grapheme cluster of the string. Fails with an error if
the string is empty.


##### Parameters


### at

```
str.at(
    int
    default: any
) -> any
```
Extracts the first grapheme cluster after the specified index. Returns
the default value if the index is out of bounds or fails with an error
if no default value was specified.


##### Parameters


##### index: int | _required_ _positional_

The byte index. If negative, indexes from the back.


##### default: any | _named_

A default value to return if the index is out of bounds.


### slice

```
str.slice(
    int
    none int
    count: int
) -> str
```
Extracts a substring of the string. Fails with an error if the start or
end index is out of bounds.


##### Parameters


##### start: int | _required_ _positional_

The start byte index (inclusive). If negative, indexes from the back.


##### end: none, int | _positional_

The end byte index (exclusive). If omitted, the whole slice until the
end of the string is extracted. If negative, indexes from the back.


##### count: int | _named_

The number of bytes to extract. This is equivalent to passing
`start + count` as the `end` position. Mutually exclusive with `end`.


### clusters

```
str.clusters(
) -> array
```
Returns the grapheme clusters of the string as an array of substrings.


##### Parameters


### codepoints

```
str.codepoints(
) -> array
```
Returns the Unicode codepoints of the string as an array of substrings.


##### Parameters


### to-unicode

```
str.to-unicode(
    str
) -> int
```
Converts a character into its corresponding code point.


##### Parameters


##### character: str | _required_ _positional_

The character that should be converted.


#### Example

<div class="previewed-code">

    #"a".to-unicode() \
    #("a\u{0300}"
       .codepoints()
       .map(str.to-unicode))

<div class="preview">

![Preview](/assets/ab9d2dcfa58024f9f0b4109859b1eb23.png)

</div>

</div>


### from-unicode

```
str.from-unicode(
    int
) -> str
```
Converts a unicode code point into its corresponding string.


##### Parameters


##### value: int | _required_ _positional_

The code point that should be converted.


#### Example

<div class="previewed-code">

    #str.from-unicode(97)

<div class="preview">

![Preview](/assets/bcdcdcb063b865dfeef8fe2a367c6b0d.png)

</div>

</div>


### normalize

```
str.normalize(
    form: str
) -> str
```
Normalizes the string to the given Unicode normal form.

This is useful when manipulating strings containing Unicode combining
characters.


##### Parameters


##### form: str | _named_




#### Example

    #assert.eq("é".normalize(form: "nfd"), "e\u{0301}")
    #assert.eq("ſ́".normalize(form: "nfkc"), "ś")


### contains

```
str.contains(
    str regex
) -> bool
```
Whether the string contains the specified pattern.

This method also has dedicated syntax: You can write
<span class="typ-str">`"bc"`</span>` `<span class="typ-key">`in`</span>` `<span class="typ-str">`"abcd"`</span>
instead of
<span class="typ-str">`"abcd"`</span><span class="typ-punct">`.`</span><span class="typ-func">`contains`</span><span class="typ-punct">`(`</span><span class="typ-str">`"bc"`</span><span class="typ-punct">`)`</span>.


##### Parameters


##### pattern: str, regex | _required_ _positional_

The pattern to search for.


### starts-with

```
str.starts-with(
    str regex
) -> bool
```
Whether the string starts with the specified pattern.


##### Parameters


##### pattern: str, regex | _required_ _positional_

The pattern the string might start with.


### ends-with

```
str.ends-with(
    str regex
) -> bool
```
Whether the string ends with the specified pattern.


##### Parameters


##### pattern: str, regex | _required_ _positional_

The pattern the string might end with.


### find

```
str.find(
    str regex
) -> none str
```
Searches for the specified pattern in the string and returns the first
match as a string or <span class="typ-key">`none`</span> if there is no
match.


##### Parameters


##### pattern: str, regex | _required_ _positional_

The pattern to search for.


### position

```
str.position(
    str regex
) -> none int
```
Searches for the specified pattern in the string and returns the index
of the first match as an integer or <span class="typ-key">`none`</span>
if there is no match.


##### Parameters


##### pattern: str, regex | _required_ _positional_

The pattern to search for.


### match

```
str.match(
    str regex
) -> none dictionary
```
Searches for the specified pattern in the string and returns a
dictionary with details about the first match or
<span class="typ-key">`none`</span> if there is no match.

The returned dictionary has the following keys:

- `start`: The start offset of the match
- `end`: The end offset of the match
- `text`: The text that matched.
- `captures`: An array containing a string for each matched capturing
  group. The first item of the array contains the first matched
  capturing, not the whole match! This is empty unless the `pattern` was
  a regex with capturing groups.


##### Parameters


##### pattern: str, regex | _required_ _positional_

The pattern to search for.


### matches

```
str.matches(
    str regex
) -> array
```
Searches for the specified pattern in the string and returns an array of
dictionaries with details about all matches. For details about the
returned dictionaries, see above.


##### Parameters


##### pattern: str, regex | _required_ _positional_

The pattern to search for.


### replace

```
str.replace(
    str regex
    str function
    count: int
) -> str
```
Replace at most `count` occurrences of the given pattern with a
replacement string or function (beginning from the start). If no count
is given, all occurrences are replaced.


##### Parameters


##### pattern: str, regex | _required_ _positional_

The pattern to search for.


##### replacement: str, function | _required_ _positional_

The string to replace the matches with or a function that gets a
dictionary for each match and can return individual replacement strings.


##### count: int | _named_

If given, only the first `count` matches of the pattern are placed.


### trim

```
str.trim(
    none str regex
    at: alignment
    repeat: bool
) -> str
```
Removes matches of a pattern from one or both sides of the string, once
or repeatedly and returns the resulting string.


##### Parameters


##### pattern: none, str, regex | _positional_

The pattern to search for. If <span class="typ-key">`none`</span>, trims
white spaces.


##### at: alignment | _named_

Can be `start` or `end` to only trim the start or end of the string. If
omitted, both sides are trimmed.


##### repeat: bool | _named_

Whether to repeatedly removes matches of the pattern or just once.
Defaults to <span class="typ-key">`true`</span>.


### split

```
str.split(
    none str regex
) -> array
```
Splits a string at matches of a specified pattern and returns an array
of the resulting parts.

When the empty string is used as a separator, it separates every
character (i.e., Unicode code point) in the string, along with the
beginning and end of the string. In practice, this means that the
resulting list of parts will contain the empty string at the start and
end of the list.


##### Parameters


##### pattern: none, str, regex | _positional_

The pattern to split at. Defaults to whitespace.


### rev

```
str.rev(
) -> str
```
Reverse the string.


##### Parameters

