# Writing in Typst

Let's get started! Suppose you got assigned to write a technical report
for university. It will contain prose, maths, headings, and figures. To
get started, you create a new project on the Typst app. You'll be taken
to the editor where you see two panels: A source panel where you compose
your document and a preview panel where you see the rendered document.

![Typst app screenshot](/assets/1-writing-app.png)

You already have a good angle for your report in mind. So let's start by
writing the introduction. Enter some text in the editor panel. You'll
notice that the text immediately appears on the previewed page.

<div class="previewed-code">

    In this report, we will explore the
    various factors that influence fluid
    dynamics in glaciers and how they
    contribute to the formation and
    behaviour of these natural structures.

<div class="preview">

![Preview](/assets/78f97553ed9aef0f2a9266f708b97fa0.png)

</div>

</div>

*Throughout this tutorial, we'll show code examples like this one. Just
like in the app, the first panel contains markup and the second panel
shows a preview. We shrunk the page to fit the examples so you can see
what's going on.*

The next step is to add a heading and emphasize some text. Typst uses
simple markup for the most common formatting tasks. To add a heading,
enter the `=` character and to emphasize some text with italics, enclose
it in <span class="typ-emph">`_underscores_`</span>.

<div class="previewed-code">

    = Introduction
    In this report, we will explore the
    various factors that influence _fluid
    dynamics_ in glaciers and how they
    contribute to the formation and
    behaviour of these natural structures.

<div class="preview">

![Preview](/assets/a7be6ffb3ed0a950a1a6507637c1d97f.png)

</div>

</div>

That was easy! To add a new paragraph, just add a blank line in between
two lines of text. If that paragraph needs a subheading, produce it by
typing `==` instead of `=`. The number of `=` characters determines the
nesting level of the heading.

Now we want to list a few of the circumstances that influence glacier
dynamics. To do that, we use a numbered list. For each item of the list,
we type a `+` character at the beginning of the line. Typst will
automatically number the items.

<div class="previewed-code">

    + The climate
    + The topography
    + The geology

<div class="preview">

![Preview](/assets/53720741b852350f277645c8bff80fae.png)

</div>

</div>

If we wanted to add a bulleted list, we would use the `-` character
instead of the `+` character. We can also nest lists: For example, we
can add a sub-list to the first item of the list above by indenting it.

<div class="previewed-code">

    + The climate
      - Temperature
      - Precipitation
    + The topography
    + The geology

<div class="preview">

![Preview](/assets/c664be04f88cfe00c791693dfee844fe.png)

</div>

</div>

## Adding a figure

You think that your report would benefit from a figure. Let's add one.
Typst supports images in the formats PNG, JPEG, GIF, SVG, and WebP. To
add an image file to your project, first open the *file panel* by
clicking the box icon in the left sidebar. Here, you can see a list of
all files in your project. Currently, there is only one: The main Typst
file you are writing in. To upload another file, click the button with
the arrow in the top-right corner. This opens the upload dialog, in
which you can pick files to upload from your computer. Select an image
file for your report.

![Upload dialog](/assets/1-writing-upload.png)

We have seen before that specific symbols (called *markup*) have
specific meaning in Typst. We can use `=`, `-`, `+`, and `_` to create
headings, lists and emphasized text, respectively. However, having a
special symbol for everything we want to insert into our document would
soon become cryptic and unwieldy. For this reason, Typst reserves markup
symbols only for the most common things. Everything else is inserted
with *functions.* For our image to show up on the page, we use Typst's
[`image`](/reference/visualize/image/ "`image`") function.

<div class="previewed-code">

    #image("glacier.jpg")

<div class="preview">

![Preview](/assets/2b02a560255bdae159a99f1a6eddfe82.png)

</div>

</div>

In general, a function produces some output for a set of *arguments*.
When you *call* a function within markup, you provide the arguments and
Typst inserts the result (the function's *return value*) into the
document. In our case, the `image` function takes one argument: The path
to the image file. To call a function in markup, we first need to type
the `#` character, immediately followed by the name of the function.
Then, we enclose the arguments in parentheses. Typst recognizes many
different data types within argument lists. Our file path is a short
[string of text](/reference/foundations/str/), so we need to enclose it
in double quotes.

The inserted image uses the whole width of the page. To change that,
pass the `width` argument to the `image` function. This is a *named*
argument and therefore specified as a `name: value` pair. If there are
multiple arguments, they are separated by commas, so we first need to
put a comma behind the path.

<div class="previewed-code">

    #image("glacier.jpg", width: 70%)

<div class="preview">

![Preview](/assets/96969d2883b3704b1ffcc1a849e66084.png)

</div>

</div>

The `width` argument is a [relative
length](/reference/layout/relative/). In our case, we specified a
percentage, determining that the image shall take up
<span class="typ-num">`70%`</span> of the page's width. We also could
have specified an absolute value like <span class="typ-num">`1cm`</span>
or <span class="typ-num">`0.7in`</span>.

Just like text, the image is now aligned at the left side of the page by
default. It's also lacking a caption. Let's fix that by using the
[figure](/reference/model/figure/ "figure") function. This function
takes the figure's contents as a positional argument and an optional
caption as a named argument.

Within the argument list of the `figure` function, Typst is already in
code mode. This means, you now have to remove the hash before the image
function call. The hash is only needed directly in markup (to
disambiguate text from function calls).

The caption consists of arbitrary markup. To give markup to a function,
we enclose it in square brackets. This construct is called a *content
block.*

<div class="previewed-code">

    #figure(
      image("glacier.jpg", width: 70%),
      caption: [
        _Glaciers_ form an important part
        of the earth's climate system.
      ],
    )

<div class="preview">

![Preview](/assets/bf93a745e50ef1f0f945f8f6689655c9.png)

</div>

</div>

You continue to write your report and now want to reference the figure.
To do that, first attach a label to figure. A label uniquely identifies
an element in your document. Add one after the figure by enclosing some
name in angle brackets. You can then reference the figure in your text
by writing an <span class="typ-ref">`@`</span> symbol followed by that
name. Headings and equations can also be labelled to make them
referenceable.

<div class="previewed-code">

    Glaciers as the one shown in
    @glaciers will cease to exist if
    we don't take action soon!

    #figure(
      image("glacier.jpg", width: 70%),
      caption: [
        _Glaciers_ form an important part
        of the earth's climate system.
      ],
    ) <glaciers>

<div class="preview">

![Preview](/assets/730675da2437f41e0bfbfc10c213b64c.png)

</div>

</div>

<div class="info-box">

So far, we've passed content blocks (markup in square brackets) and
strings (text in double quotes) to our functions. Both seem to contain
text. What's the difference?

A content block can contain text, but also any other kind of markup,
function calls, and more, whereas a string is really just a *sequence of
characters* and nothing else.

For example, the image function expects a path to an image file. It
would not make sense to pass, e.g., a paragraph of text or another image
as the image's path parameter. That's why only strings are allowed here.
In contrast, strings work wherever content is expected because text is a
valid kind of content.

</div>

## Adding a bibliography

As you write up your report, you need to back up some of your claims.
You can add a bibliography to your document with the
[`bibliography`](/reference/model/bibliography/ "`bibliography`")
function. This function expects a path to a bibliography file.

Typst's native bibliography format is
[Hayagriva](https://github.com/typst/hayagriva/blob/main/docs/file-format.md),
but for compatibility you can also use BibLaTeX files. As your classmate
has already done a literature survey and sent you a `.bib` file, you'll
use that one. Upload the file through the file panel to access it in
Typst.

Once the document contains a bibliography, you can start citing from it.
Citations use the same syntax as references to a label. As soon as you
cite a source for the first time, it will appear in the bibliography
section of your document. Typst supports different citation and
bibliography styles. Consult the
[reference](/reference/model/bibliography/#parameters-style) for more
details.

<div class="previewed-code">

    = Methods
    We follow the glacier melting models
    established in @glacier-melt.

    #bibliography("works.bib")

<div class="preview">

![Preview](/assets/4063c74f5e24b1d79ad2bffcbf2d3558.png)

</div>

</div>

## Maths

After fleshing out the methods section, you move on to the meat of the
document: Your equations. Typst has built-in mathematical typesetting
and uses its own math notation. Let's start with a simple equation. We
wrap it in `$` signs to let Typst know it should expect a mathematical
expression:

<div class="previewed-code">

    The equation $Q = rho A v + C$
    defines the glacial flow rate.

<div class="preview">

![Preview](/assets/feee418cba0c141654db383539650b76.png)

</div>

</div>

The equation is typeset inline, on the same line as the surrounding
text. If you want to have it on its own line instead, you should insert
a single space at its start and end:

<div class="previewed-code">

    The flow rate of a glacier is
    defined by the following equation:

    $ Q = rho A v + C $

<div class="preview">

![Preview](/assets/1972349af18eaaa482d7ae624532be43.png)

</div>

</div>

We can see that Typst displayed the single letters `Q`, `A`, `v`, and
`C` as-is, while it translated `rho` into a Greek letter. Math mode will
always show single letters verbatim. Multiple letters, however, are
interpreted as symbols, variables, or function names. To imply a
multiplication between single letters, put spaces between them.

If you want to have a variable that consists of multiple letters, you
can enclose it in quotes:

<div class="previewed-code">

    The flow rate of a glacier is given
    by the following equation:

    $ Q = rho A v + "time offset" $

<div class="preview">

![Preview](/assets/2526a88c6062287f852db218a9e59280.png)

</div>

</div>

You'll also need a sum formula in your paper. We can use the `sum`
symbol and then specify the range of the summation in sub- and
superscripts:

<div class="previewed-code">

    Total displaced soil by glacial flow:

    $ 7.32 beta +
      sum_(i=0)^nabla Q_i / 2 $

<div class="preview">

![Preview](/assets/ad30f24c6c4995728f44726e6f700b46.png)

</div>

</div>

To add a subscript to a symbol or variable, type a `_` character and
then the subscript. Similarly, use the `^` character for a superscript.
If your sub- or superscript consists of multiple things, you must
enclose them in round parentheses.

The above example also showed us how to insert fractions: Simply put a
`/` character between the numerator and the denominator and Typst will
automatically turn it into a fraction. Parentheses are smartly resolved,
so you can enter your expression as you would into a calculator and
Typst will replace parenthesized sub-expressions with the appropriate
notation.

<div class="previewed-code">

    Total displaced soil by glacial flow:

    $ 7.32 beta +
      sum_(i=0)^nabla
        (Q_i (a_i - epsilon)) / 2 $

<div class="preview">

![Preview](/assets/1e0781d81c792e1ddae4d3df17a58477.png)

</div>

</div>

Not all math constructs have special syntax. Instead, we use functions,
just like the `image` function we have seen before. For example, to
insert a column vector, we can use the [`vec`](/reference/math/vec/)
function. Within math mode, function calls don't need to start with the
`#` character.

<div class="previewed-code">

    $ v := vec(x_1, x_2, x_3) $

<div class="preview">

![Preview](/assets/9e3d2932792ea17dade45677ff1e982b.png)

</div>

</div>

Some functions are only available within math mode. For example, the
[`cal`](/reference/math/variants/#functions-cal) function is used to
typeset calligraphic letters commonly used for sets. The [math section
of the reference](/reference/math/) provides a complete list of all
functions that math mode makes available.

One more thing: Many symbols, such as the arrow, have a lot of variants.
You can select among these variants by appending a dot and a modifier
name to a symbol's name:

<div class="previewed-code">

    $ a arrow.squiggly b $

<div class="preview">

![Preview](/assets/d068108ad373e358feef9177152ea203.png)

</div>

</div>

This notation is also available in markup mode, but the symbol name must
be preceded with `#sym.` there. See the [symbols
section](/reference/symbols/sym/) for a list of all available symbols.

## Review

You have now seen how to write a basic document in Typst. You learned
how to emphasize text, write lists, insert images, align content, and
typeset mathematical expressions. You also learned about Typst's
functions. There are many more kinds of content that Typst lets you
insert into your document, such as [tables](/reference/model/table/),
[shapes](/reference/visualize/), and [code
blocks](/reference/text/raw/). You can peruse the
[reference](/reference/ "reference") to learn more about these and other
features.

For the moment, you have completed writing your report. You have already
saved a PDF by clicking on the download button in the top right corner.
However, you think the report could look a bit less plain. In the next
section, we'll learn how to customize the look of our document.
