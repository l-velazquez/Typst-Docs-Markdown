
# text

```
text(
    font: str array dictionary
    fallback: bool
    style: str
    weight: int str
    stretch: ratio
    size: length
    fill: color gradient tiling
    stroke: none length color gradient stroke tiling dictionary
    tracking: length
    spacing: relative
    cjk-latin-spacing: none auto
    baseline: length
    overhang: bool
    top-edge: length str
    bottom-edge: length str
    lang: str
    region: none str
    script: auto str
    dir: auto direction
    hyphenate: auto bool
    costs: dictionary
    kerning: bool
    alternates: bool
    stylistic-set: none int array
    ligatures: bool
    discretionary-ligatures: bool
    historical-ligatures: bool
    number-type: auto str
    number-width: auto str
    slashed-zero: bool
    fractions: bool
    features: array dictionary
    content
    str
) -> content
```
Customizes the look and layout of text in a variety of ways.

This function is used frequently, both with set rules and directly.
While the set rule is often the simpler choice, calling the `text`
function directly can be useful when passing text as an argument to
another function.

## Example

<div class="previewed-code">

    #set text(18pt)
    With a set rule.

    #emph(text(blue)[
      With a function call.
    ])

<div class="preview">

![Preview](/assets/4c4d532afa86c376a347a8e7de9857ba.png)

</div>

</div>


### Parameters


### font: str, array, dictionary | _named_

A font family descriptor or priority list of font family descriptor.

A font family descriptor can be a plain string representing the family
name or a dictionary with the following keys:

- `name` (required): The font family name.
- `covers` (optional): Defines the Unicode codepoints for which the
  family shall be used. This can be:
  - A predefined coverage set:
    - <span class="typ-str">`"latin-in-cjk"`</span> covers all
      codepoints except for those which exist in Latin fonts, but should
      preferrably be taken from CJK fonts.
  - A [regular expression](/reference/foundations/regex/) that defines
    exactly which codepoints shall be covered. Accepts only the subset
    of regular expressions which consist of exactly one dot, letter, or
    character class.

When processing text, Typst tries all specified font families in order
until it finds a font that has the necessary glyphs. In the example
below, the font `Inria Serif` is preferred, but since it does not
contain Arabic glyphs, the arabic text uses `Noto Sans Arabic` instead.

The collection of available fonts differs by platform:

- In the web app, you can see the list of available fonts by clicking on
  the "Ag" button. You can provide additional fonts by uploading `.ttf`
  or `.otf` files into your project. They will be discovered
  automatically. The priority is: project fonts \> server fonts.

- Locally, Typst uses your installed system fonts or embedded fonts in
  the CLI, which are `Libertinus Serif`, `New Computer Modern`,
  `New Computer Modern Math`, and `DejaVu Sans Mono`. In addition, you
  can use the `--font-path` argument or `TYPST_FONT_PATHS` environment
  variable to add directories that should be scanned for fonts. The
  priority is: `--font-paths` \> system fonts \> embedded fonts. Run
  `typst fonts` to see the fonts that Typst has discovered on your
  system. Note that you can pass the `--ignore-system-fonts` parameter
  to the CLI to ensure Typst won't search for system fonts.


#### Example

<div class="previewed-code">

    #set text(font: "PT Sans")
    This is sans-serif.

    #set text(font: (
      "Inria Serif",
      "Noto Sans Arabic",
    ))

    This is Latin. \
    هذا عربي.

    // Change font only for numbers.
    #set text(font: (
      (name: "PT Sans", covers: regex("[0-9]")),
      "Libertinus Serif"
    ))

    The number 123.

    // Mix Latin and CJK fonts.
    #set text(font: (
      (name: "Inria Serif", covers: "latin-in-cjk"),
      "Noto Serif CJK SC"
    ))
    分别设置“中文”和English字体

<div class="preview">

![Preview](/assets/b0e6e547c4953ea23eb13ec24204d5b7.png)

</div>

</div>


### fallback: bool | _named_

Whether to allow last resort font fallback when the primary font list
contains no match. This lets Typst search through all available fonts
for the most similar one that has the necessary glyphs.

*Note:* Currently, there are no warnings when fallback is disabled and
no glyphs are found. Instead, your text shows up in the form of "tofus":
Small boxes that indicate the lack of an appropriate glyph. In the
future, you will be able to instruct Typst to issue warnings so you know
something is up.


#### Example

<div class="previewed-code">

    #set text(font: "Inria Serif")
    هذا عربي

    #set text(fallback: false)
    هذا عربي

<div class="preview">

![Preview](/assets/b1af15aac61b74295296a8b4f2a27284.png)

</div>

</div>


### style: str | _named_

The desired font style.

When an italic style is requested and only an oblique one is available,
it is used. Similarly, the other way around, an italic style can stand
in for an oblique one. When neither an italic nor an oblique style is
available, Typst selects the normal style. Since most fonts are only
available either in an italic or oblique style, the difference between
italic and oblique style is rarely observable.

If you want to emphasize your text, you should do so using the
[emph](/reference/model/emph/ "emph") function instead. This makes it
easy to adapt the style later if you change your mind about how to
signify the emphasis.


#### Example

<div class="previewed-code">

    #text(font: "Libertinus Serif", style: "italic")[Italic]
    #text(font: "DejaVu Sans", style: "oblique")[Oblique]

<div class="preview">

![Preview](/assets/4b9c5a65c56818bb674ffd17c1b3d251.png)

</div>

</div>


### weight: int, str | _named_

The desired thickness of the font's glyphs. Accepts an integer between
<span class="typ-num">`100`</span> and
<span class="typ-num">`900`</span> or one of the predefined weight
names. When the desired weight is not available, Typst selects the font
from the family that is closest in weight.

If you want to strongly emphasize your text, you should do so using the
[strong](/reference/model/strong/ "strong") function instead. This makes
it easy to adapt the style later if you change your mind about how to
signify the strong emphasis.


#### Example

<div class="previewed-code">

    #set text(font: "IBM Plex Sans")

    #text(weight: "light")[Light] \
    #text(weight: "regular")[Regular] \
    #text(weight: "medium")[Medium] \
    #text(weight: 500)[Medium] \
    #text(weight: "bold")[Bold]

<div class="preview">

![Preview](/assets/1cb609109c98561040c24d4d7062598d.png)

</div>

</div>


### stretch: ratio | _named_

The desired width of the glyphs. Accepts a ratio between
<span class="typ-num">`50%`</span> and
<span class="typ-num">`200%`</span>. When the desired width is not
available, Typst selects the font from the family that is closest in
stretch. This will only stretch the text if a condensed or expanded
version of the font is available.

If you want to adjust the amount of space between characters instead of
stretching the glyphs itself, use the
[`tracking`](/reference/text/text/#parameters-tracking) property
instead.


#### Example

<div class="previewed-code">

    #text(stretch: 75%)[Condensed] \
    #text(stretch: 100%)[Normal]

<div class="preview">

![Preview](/assets/4217023c40ad8ed765f87693da4748a1.png)

</div>

</div>


### size: length | _named_

The size of the glyphs. This value forms the basis of the `em` unit:
<span class="typ-num">`1em`</span> is equivalent to the font size.

You can also give the font size itself in `em` units. Then, it is
relative to the previous font size.


#### Example

<div class="previewed-code">

    #set text(size: 20pt)
    very #text(1.5em)[big] text

<div class="preview">

![Preview](/assets/6e585e03ae4380e535964b253a81e276.png)

</div>

</div>


### fill: color, gradient, tiling | _named_

The glyph fill paint.


#### Example

<div class="previewed-code">

    #set text(fill: red)
    This text is red.

<div class="preview">

![Preview](/assets/863753af3dc1d479c0b515c24534ed18.png)

</div>

</div>


### stroke: none, length, color, gradient, stroke, tiling, dictionary | _named_

How to stroke the text.


#### Example

<div class="previewed-code">

    #text(stroke: 0.5pt + red)[Stroked]

<div class="preview">

![Preview](/assets/f5723c110d4ceab3aeb120d14486da3d.png)

</div>

</div>


### tracking: length | _named_

The amount of space that should be added between characters.


#### Example

<div class="previewed-code">

    #set text(tracking: 1.5pt)
    Distant text.

<div class="preview">

![Preview](/assets/fd6e5930cbe089796fe41f2f23ab1b71.png)

</div>

</div>


### spacing: relative | _named_

The amount of space between words.

Can be given as an absolute length, but also relative to the width of
the space character in the font.

If you want to adjust the amount of space between characters rather than
words, use the [`tracking`](/reference/text/text/#parameters-tracking)
property instead.


#### Example

<div class="previewed-code">

    #set text(spacing: 200%)
    Text with distant words.

<div class="preview">

![Preview](/assets/34b6ad97bc5efcf7ed5e92bc788d564a.png)

</div>

</div>


### cjk-latin-spacing: none, auto | _named_

Whether to automatically insert spacing between CJK and Latin
characters.


#### Example

<div class="previewed-code">

    #set text(cjk-latin-spacing: auto)
    第4章介绍了基本的API。

    #set text(cjk-latin-spacing: none)
    第4章介绍了基本的API。

<div class="preview">

![Preview](/assets/57151e3356efb0bcf28257a871999050.png)

</div>

</div>


### baseline: length | _named_

An amount to shift the text baseline by.


#### Example

<div class="previewed-code">

    A #text(baseline: 3pt)[lowered]
    word.

<div class="preview">

![Preview](/assets/29cd44f53b3d9b58b7d1dbed7f9ca642.png)

</div>

</div>


### overhang: bool | _named_

Whether certain glyphs can hang over into the margin in justified text.
This can make justification visually more pleasing.


#### Example

<div class="previewed-code">

    #set page(width: 220pt)

    #set par(justify: true)
    This justified text has a hyphen in
    the paragraph's second line. Hanging
    the hyphen slightly into the margin
    results in a clearer paragraph edge.

    #set text(overhang: false)
    This justified text has a hyphen in
    the paragraph's second line. Hanging
    the hyphen slightly into the margin
    results in a clearer paragraph edge.

<div class="preview">

![Preview](/assets/7e85841a82173928a86915f16412adee.png)

</div>

</div>


### top-edge: length, str | _named_

The top end of the conceptual frame around the text used for layout and
positioning. This affects the size of containers that hold text.


#### Example

<div class="previewed-code">

    #set rect(inset: 0pt)
    #set text(size: 20pt)

    #set text(top-edge: "ascender")
    #rect(fill: aqua)[Typst]

    #set text(top-edge: "cap-height")
    #rect(fill: aqua)[Typst]

<div class="preview">

![Preview](/assets/2c378c736222a9bffd2f76a3d6536ba6.png)

</div>

</div>


### bottom-edge: length, str | _named_

The bottom end of the conceptual frame around the text used for layout
and positioning. This affects the size of containers that hold text.


#### Example

<div class="previewed-code">

    #set rect(inset: 0pt)
    #set text(size: 20pt)

    #set text(bottom-edge: "baseline")
    #rect(fill: aqua)[Typst]

    #set text(bottom-edge: "descender")
    #rect(fill: aqua)[Typst]

<div class="preview">

![Preview](/assets/97858b07ae2015fa6533e6c33d7ee911.png)

</div>

</div>


### lang: str | _named_

An [ISO 639-1/2/3 language code.](https://en.wikipedia.org/wiki/ISO_639)

Setting the correct language affects various parts of Typst:

- The text processing pipeline can make more informed choices.
- Hyphenation will use the correct patterns for the language.
- [Smart quotes](/reference/text/smartquote/) turns into the correct
  quotes for the language.
- And all other things which are language-aware.


#### Example

<div class="previewed-code">

    #set text(lang: "de")
    #outline()

    = Einleitung
    In diesem Dokument, ...

<div class="preview">

![Preview](/assets/a55fee9de08b4e55ff7ed7e4e19248d5.png)

</div>

</div>


### region: none, str | _named_

An [ISO 3166-1 alpha-2 region
code.](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)

This lets the text processing pipeline make more informed choices.


### script: auto, str | _named_

The OpenType writing script.

The combination of `lang` and `script` determine how font features, such
as glyph substitution, are implemented. Frequently the value is a
modified (all-lowercase) ISO 15924 script identifier, and the `math`
writing script is used for features appropriate for mathematical
symbols.

When set to <span class="typ-key">`auto`</span>, the default and
recommended setting, an appropriate script is chosen for each block of
characters sharing a common Unicode script property.


#### Example

<div class="previewed-code">

    #set text(
      font: "Libertinus Serif",
      size: 20pt,
    )

    #let scedilla = [Ş]
    #scedilla // S with a cedilla

    #set text(lang: "ro", script: "latn")
    #scedilla // S with a subscript comma

    #set text(lang: "ro", script: "grek")
    #scedilla // S with a cedilla

<div class="preview">

![Preview](/assets/209a2fa5b7b5739ad1afd0ccfca461be.png)

</div>

</div>


### dir: auto, direction | _named_

The dominant direction for text and inline objects. Possible values are:

- <span class="typ-key">`auto`</span>: Automatically infer the direction
  from the `lang` property.
- `ltr`: Layout text from left to right.
- `rtl`: Layout text from right to left.

When writing in right-to-left scripts like Arabic or Hebrew, you should
set the [text language](/reference/text/text/#parameters-lang) or
direction. While individual runs of text are automatically layouted in
the correct direction, setting the dominant direction gives the
bidirectional reordering algorithm the necessary information to
correctly place punctuation and inline objects. Furthermore, setting the
direction affects the alignment values `start` and `end`, which are
equivalent to `left` and `right` in `ltr` text and the other way around
in `rtl` text.

If you set this to `rtl` and experience bugs or in some way bad looking
output, please get in touch with us through the
[Forum](https://forum.typst.app/), [Discord
server](https://discord.gg/2uDybryKPe), or our [contact
form](https://typst.app/contact).


#### Example

<div class="previewed-code">

    #set text(dir: rtl)
    هذا عربي.

<div class="preview">

![Preview](/assets/2ab58031e2803cdb2db3e977e02ade98.png)

</div>

</div>


### hyphenate: auto, bool | _named_

Whether to hyphenate text to improve line breaking. When
<span class="typ-key">`auto`</span>, text will be hyphenated if and only
if justification is enabled.

Setting the [text language](/reference/text/text/#parameters-lang)
ensures that the correct hyphenation patterns are used.


#### Example

<div class="previewed-code">

    #set page(width: 200pt)

    #set par(justify: true)
    This text illustrates how
    enabling hyphenation can
    improve justification.

    #set text(hyphenate: false)
    This text illustrates how
    enabling hyphenation can
    improve justification.

<div class="preview">

![Preview](/assets/e0f69f8acf03bf5192584f1d224031db.png)

</div>

</div>


### costs: dictionary | _named_

The "cost" of various choices when laying out text. A higher cost means
the layout engine will make the choice less often. Costs are specified
as a ratio of the default cost, so <span class="typ-num">`50%`</span>
will make text layout twice as eager to make a given choice, while
<span class="typ-num">`200%`</span> will make it half as eager.

Currently, the following costs can be customized:

- `hyphenation`: splitting a word across multiple lines
- `runt`: ending a paragraph with a line with a single word
- `widow`: leaving a single line of paragraph on the next page
- `orphan`: leaving single line of paragraph on the previous page

Hyphenation is generally avoided by placing the whole word on the next
line, so a higher hyphenation cost can result in awkward justification
spacing. Note: Hyphenation costs will only be applied when the
[`linebreaks`](/reference/model/par/#parameters-linebreaks) are set to
"optimized". (For example by default implied by
[`justify`](/reference/model/par/#parameters-justify).)

Runts are avoided by placing more or fewer words on previous lines, so a
higher runt cost can result in more awkward in justification spacing.

Text layout prevents widows and orphans by default because they are
generally discouraged by style guides. However, in some contexts they
are allowed because the prevention method, which moves a line to the
next page, can result in an uneven number of lines between pages. The
`widow` and `orphan` costs allow disabling these modifications.
(Currently, <span class="typ-num">`0%`</span> allows widows/orphans;
anything else, including the default of
<span class="typ-num">`100%`</span>, prevents them. More nuanced cost
specification for these modifications is planned for the future.)


#### Example

<div class="previewed-code">

    #set text(hyphenate: true, size: 11.4pt)
    #set par(justify: true)

    #lorem(10)

    // Set hyphenation to ten times the normal cost.
    #set text(costs: (hyphenation: 1000%))

    #lorem(10)

<div class="preview">

![Preview](/assets/93d24bc3ca8855420d6a462b9efe749c.png)

</div>

</div>


### kerning: bool | _named_

Whether to apply kerning.

When enabled, specific letter pairings move closer together or further
apart for a more visually pleasing result. The example below
demonstrates how decreasing the gap between the "T" and "o" results in a
more natural look. Setting this to <span class="typ-key">`false`</span>
disables kerning by turning off the OpenType `kern` font feature.


#### Example

<div class="previewed-code">

    #set text(size: 25pt)
    Totally

    #set text(kerning: false)
    Totally

<div class="preview">

![Preview](/assets/ec68f84e39f03f441f48e7898bb74a74.png)

</div>

</div>


### alternates: bool | _named_

Whether to apply stylistic alternates.

Sometimes fonts contain alternative glyphs for the same codepoint.
Setting this to <span class="typ-key">`true`</span> switches to these by
enabling the OpenType `salt` font feature.


#### Example

<div class="previewed-code">

    #set text(
      font: "IBM Plex Sans",
      size: 20pt,
    )

    0, a, g, ß

    #set text(alternates: true)
    0, a, g, ß

<div class="preview">

![Preview](/assets/23407cf20817ff1de3ab95b59af59522.png)

</div>

</div>


### stylistic-set: none, int, array | _named_

Which stylistic sets to apply. Font designers can categorize alternative
glyphs forms into stylistic sets. As this value is highly font-specific,
you need to consult your font to know which sets are available.

This can be set to an integer or an array of integers, all of which must
be between <span class="typ-num">`1`</span> and
<span class="typ-num">`20`</span>, enabling the corresponding OpenType
feature(s) from `ss01` to `ss20`. Setting this to
<span class="typ-key">`none`</span> will disable all stylistic sets.


#### Example

<div class="previewed-code">

    #set text(font: "IBM Plex Serif")
    ß vs #text(stylistic-set: 5)[ß] \
    10 years ago vs #text(stylistic-set: (1, 2, 3))[10 years ago]

<div class="preview">

![Preview](/assets/5b86c1ea81329b78b01ff35d79046c10.png)

</div>

</div>


### ligatures: bool | _named_

Whether standard ligatures are active.

Certain letter combinations like "fi" are often displayed as a single
merged glyph called a *ligature.* Setting this to
<span class="typ-key">`false`</span> disables these ligatures by turning
off the OpenType `liga` and `clig` font features.


#### Example

<div class="previewed-code">

    #set text(size: 20pt)
    A fine ligature.

    #set text(ligatures: false)
    A fine ligature.

<div class="preview">

![Preview](/assets/2109cb14aa0ab28c51ca1477a526df8b.png)

</div>

</div>


### discretionary-ligatures: bool | _named_

Whether ligatures that should be used sparingly are active. Setting this
to <span class="typ-key">`true`</span> enables the OpenType `dlig` font
feature.


### historical-ligatures: bool | _named_

Whether historical ligatures are active. Setting this to
<span class="typ-key">`true`</span> enables the OpenType `hlig` font
feature.


### number-type: auto, str | _named_

Which kind of numbers / figures to select. When set to
<span class="typ-key">`auto`</span>, the default numbers for the font
are used.


#### Example

<div class="previewed-code">

    #set text(font: "Noto Sans", 20pt)
    #set text(number-type: "lining")
    Number 9.

    #set text(number-type: "old-style")
    Number 9.

<div class="preview">

![Preview](/assets/265e723c8ff8a57dd46dc563ab1239fd.png)

</div>

</div>


### number-width: auto, str | _named_

The width of numbers / figures. When set to
<span class="typ-key">`auto`</span>, the default numbers for the font
are used.


#### Example

<div class="previewed-code">

    #set text(font: "Noto Sans", 20pt)
    #set text(number-width: "proportional")
    A 12 B 34. \
    A 56 B 78.

    #set text(number-width: "tabular")
    A 12 B 34. \
    A 56 B 78.

<div class="preview">

![Preview](/assets/ea208c5a3d005bd6d214a049e3cb5d8b.png)

</div>

</div>


### slashed-zero: bool | _named_

Whether to have a slash through the zero glyph. Setting this to
<span class="typ-key">`true`</span> enables the OpenType `zero` font
feature.


#### Example

<div class="previewed-code">

    0, #text(slashed-zero: true)[0]

<div class="preview">

![Preview](/assets/36a92f135283b6fae64a02899e67d15b.png)

</div>

</div>


### fractions: bool | _named_

Whether to turn numbers into fractions. Setting this to
<span class="typ-key">`true`</span> enables the OpenType `frac` font
feature.

It is not advisable to enable this property globally as it will mess
with all appearances of numbers after a slash (e.g., in URLs). Instead,
enable it locally when you want a fraction.


#### Example

<div class="previewed-code">

    1/2 \
    #text(fractions: true)[1/2]

<div class="preview">

![Preview](/assets/45e2f75869630730e77d31deca609719.png)

</div>

</div>


### features: array, dictionary | _named_

Raw OpenType features to apply.

- If given an array of strings, sets the features identified by the
  strings to <span class="typ-num">`1`</span>.
- If given a dictionary mapping to numbers, sets the features identified
  by the keys to the values.


#### Example

<div class="previewed-code">

    // Enable the `frac` feature manually.
    #set text(features: ("frac",))
    1/2

<div class="preview">

![Preview](/assets/618fc07c7aaf3b0656b530737e00ef33.png)

</div>

</div>


### body: content | _required_ _positional_

Content in which all text is styled according to the other arguments.


### text: str | _required_ _positional_

The text.

