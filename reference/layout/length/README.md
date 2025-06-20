
# Length

A size or distance, possibly expressed with contextual units.

Typst supports the following length units:

- Points: <span class="typ-num">`72pt`</span>
- Millimeters: <span class="typ-num">`254mm`</span>
- Centimeters: <span class="typ-num">`2.54cm`</span>
- Inches: <span class="typ-num">`1in`</span>
- Relative to font size: <span class="typ-num">`2.5em`</span>

You can multiply lengths with and divide them by integers and floats.

## Example

<div class="previewed-code">

    #rect(width: 20pt)
    #rect(width: 2em)
    #rect(width: 1in)

    #(3em + 5pt).em \
    #(20pt).em \
    #(40em + 2pt).abs \
    #(5em).abs

<div class="preview">

![Preview](/assets/829c0a1d2ef2db0201ec12311845e833.png)

</div>

</div>

## Fields

- `abs`: A length with just the absolute component of the current length
  (that is, excluding the `em` component).
- `em`: The amount of `em` units in this length, as a
  [float](/reference/foundations/float/ "float").


## Definitions


### pt

```
length.pt(
) -> float
```
Converts this length to points.

Fails with an error if this length has non-zero `em` units (such as
`5em + 2pt` instead of just `2pt`). Use the `abs` field (such as in
`(5em + 2pt).abs.pt()`) to ignore the `em` component of the length (thus
converting only its absolute component).


##### Parameters


### mm

```
length.mm(
) -> float
```
Converts this length to millimeters.

Fails with an error if this length has non-zero `em` units. See the
[`pt`](/reference/layout/length/#definitions-pt) method for more
details.


##### Parameters


### cm

```
length.cm(
) -> float
```
Converts this length to centimeters.

Fails with an error if this length has non-zero `em` units. See the
[`pt`](/reference/layout/length/#definitions-pt) method for more
details.


##### Parameters


### inches

```
length.inches(
) -> float
```
Converts this length to inches.

Fails with an error if this length has non-zero `em` units. See the
[`pt`](/reference/layout/length/#definitions-pt) method for more
details.


##### Parameters


### to-absolute

```
length.to-absolute(
) -> length
```
Resolve this length to an absolute length.


##### Parameters


#### Example

<div class="previewed-code">

    #set text(size: 12pt)
    #context [
      #(6pt).to-absolute() \
      #(6pt + 10em).to-absolute() \
      #(10em).to-absolute()
    ]

    #set text(size: 6pt)
    #context [
      #(6pt).to-absolute() \
      #(6pt + 10em).to-absolute() \
      #(10em).to-absolute()
    ]

<div class="preview">

![Preview](/assets/3bc7f89b14d9cfece24bb79c946032be.png)

</div>

</div>

