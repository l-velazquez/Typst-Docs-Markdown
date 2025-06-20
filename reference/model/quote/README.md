
# quote

```
quote(
    block: bool
    quotes: auto bool
    attribution: none label content
    content
) -> content
```
Displays a quote alongside an optional attribution.

## Example

<div class="previewed-code">

    Plato is often misquoted as the author of #quote[I know that I know
    nothing], however, this is a derivation form his original quote:

    #set quote(block: true)

    #quote(attribution: [Plato])[
      ... ἔοικα γοῦν τούτου γε σμικρῷ τινι αὐτῷ τούτῳ σοφώτερος εἶναι, ὅτι
      ἃ μὴ οἶδα οὐδὲ οἴομαι εἰδέναι.
    ]
    #quote(attribution: [from the Henry Cary literal translation of 1897])[
      ... I seem, then, in just this little thing to be wiser than this man at
      any rate, that what I do not know I do not think I know either.
    ]

<div class="preview">

![Preview](/assets/489a5ed7392113f962651305e5c032e2.png)

</div>

</div>

By default block quotes are padded left and right by
<span class="typ-num">`1em`</span>, alignment and padding can be
controlled with show rules:

<div class="previewed-code">

    #set quote(block: true)
    #show quote: set align(center)
    #show quote: set pad(x: 5em)

    #quote[
      You cannot pass... I am a servant of the Secret Fire, wielder of the
      flame of Anor. You cannot pass. The dark fire will not avail you,
      flame of Udûn. Go back to the Shadow! You cannot pass.
    ]

<div class="preview">

![Preview](/assets/40b36fe0f7e9d3304a4afc3121f6f2fb.png)

</div>

</div>


### Parameters


### block: bool | _named_

Whether this is a block quote.


#### Example

<div class="previewed-code">

    An inline citation would look like
    this: #quote(
      attribution: [René Descartes]
    )[
      cogito, ergo sum
    ], and a block equation like this:
    #quote(
      block: true,
      attribution: [JFK]
    )[
      Ich bin ein Berliner.
    ]

<div class="preview">

![Preview](/assets/6d82e3cc8b943b344ef47617ef14f5d7.png)

</div>

</div>


### quotes: auto, bool | _named_

Whether double quotes should be added around this quote.

The double quotes used are inferred from the `quotes` property on
[smartquote](/reference/text/smartquote/ "smartquote"), which is
affected by the `lang` property on [text](/reference/text/text/ "text").

- <span class="typ-key">`true`</span>: Wrap this quote in double quotes.
- <span class="typ-key">`false`</span>: Do not wrap this quote in double
  quotes.
- <span class="typ-key">`auto`</span>: Infer whether to wrap this quote
  in double quotes based on the `block` property. If `block` is
  <span class="typ-key">`false`</span>, double quotes are automatically
  added.


#### Example

<div class="previewed-code">

    #set text(lang: "de")

    Ein deutsch-sprechender Author
    zitiert unter umständen JFK:
    #quote[Ich bin ein Berliner.]

    #set text(lang: "en")

    And an english speaking one may
    translate the quote:
    #quote[I am a Berliner.]

<div class="preview">

![Preview](/assets/dd0b26e309b9aa03b7307ee1deb14808.png)

</div>

</div>


### attribution: none, label, content | _named_

The attribution of this quote, usually the author or source. Can be a
label pointing to a bibliography entry or any content. By default only
displayed for block quotes, but can be changed using a
<span class="typ-key">`show`</span> rule.


#### Example

<div class="previewed-code">

    #quote(attribution: [René Descartes])[
      cogito, ergo sum
    ]

    #show quote.where(block: false): it => {
      ["] + h(0pt, weak: true) + it.body + h(0pt, weak: true) + ["]
      if it.attribution != none [ (#it.attribution)]
    }

    #quote(
      attribution: link("https://typst.app/home")[typst.com]
    )[
      Compose papers faster
    ]

    #set quote(block: true)

    #quote(attribution: <tolkien54>)[
      You cannot pass... I am a servant
      of the Secret Fire, wielder of the
      flame of Anor. You cannot pass. The
      dark fire will not avail you, flame
      of Udûn. Go back to the Shadow! You
      cannot pass.
    ]

    #bibliography("works.bib", style: "apa")

<div class="preview">

![Preview](/assets/6c1d01df1df68254a7fe801396417a99.png)

</div>

</div>


### body: content | _required_ _positional_

The quote.

