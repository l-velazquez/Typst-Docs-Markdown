
# strike

```
strike(
    stroke: auto length color gradient stroke tiling dictionary
    offset: auto length
    extent: length
    background: bool
    content
) -> content
```
Strikes through text.

## Example

<div class="previewed-code">

    This is #strike[not] relevant.

<div class="preview">

![Preview](/assets/8189864734cb2541923731f3119141de.png)

</div>

</div>


### Parameters


### stroke: auto, length, color, gradient, stroke, tiling, dictionary | _named_

How to [stroke](/reference/visualize/stroke/ "stroke") the line.

If set to <span class="typ-key">`auto`</span>, takes on the text's color
and a thickness defined in the current font.

*Note:* Please don't use this for real redaction as you can still copy
paste the text.


#### Example

<div class="previewed-code">

    This is #strike(stroke: 1.5pt + red)[very stricken through]. \
    This is #strike(stroke: 10pt)[redacted].

<div class="preview">

![Preview](/assets/cf96e26cbdace6727d460e5d550728e5.png)

</div>

</div>


### offset: auto, length | _named_

The position of the line relative to the baseline. Read from the font
tables if <span class="typ-key">`auto`</span>.

This is useful if you are unhappy with the offset your font provides.


#### Example

<div class="previewed-code">

    #set text(font: "Inria Serif")
    This is #strike(offset: auto)[low-ish]. \
    This is #strike(offset: -3.5pt)[on-top].

<div class="preview">

![Preview](/assets/d4e11d77bfdfd0e135abff2328454799.png)

</div>

</div>


### extent: length | _named_

The amount by which to extend the line beyond (or within if negative)
the content.


#### Example

<div class="previewed-code">

    This #strike(extent: -2pt)[skips] parts of the word.
    This #strike(extent: 2pt)[extends] beyond the word.

<div class="preview">

![Preview](/assets/12a783f0ebc265e7a2f246c8f13e53d0.png)

</div>

</div>


### background: bool | _named_

Whether the line is placed behind the content.


#### Example

<div class="previewed-code">

    #set strike(stroke: red)
    #strike(background: true)[This is behind.] \
    #strike(background: false)[This is in front.]

<div class="preview">

![Preview](/assets/e41cc1fba2e5beb8482cdf79d7ed8ab9.png)

</div>

</div>


### body: content | _required_ _positional_

The content to strike through.

