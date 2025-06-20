
# image

```
image(
    str bytes
    format: auto str dictionary
    width: auto relative
    height: auto relative fraction
    alt: none str
    fit: str
    scaling: auto str
    icc: auto str bytes
) -> content
```
A raster or vector graphic.

You can wrap the image in a
[`figure`](/reference/model/figure/ "`figure`") to give it a number and
caption.

Like most elements, images are *block-level* by default and thus do not
integrate themselves into adjacent paragraphs. To force an image to
become inline, put it into a [`box`](/reference/layout/box/ "`box`").

## Example

<div class="previewed-code">

    #figure(
      image("molecular.jpg", width: 80%),
      caption: [
        A step in the molecular testing
        pipeline of our lab.
      ],
    )

<div class="preview">

![Preview](/assets/ce75a73e1e074f91aba6411c6e77cec4.png)

</div>

</div>


### Parameters


### source: str, bytes | _required_ _positional_

A [path](/reference/syntax/#paths) to an image file or raw bytes making
up an image in one of the supported
[formats](/reference/visualize/image/#parameters-format).

Bytes can be used to specify raw pixel data in a row-major,
left-to-right, top-to-bottom format.


#### Example

<div class="previewed-code">

    #let original = read("diagram.svg")
    #let changed = original.replace(
      "#2B80FF", // blue
      green.to-hex(),
    )

    #image(bytes(original))
    #image(bytes(changed))

<div class="preview">

![Preview](/assets/8c4900221f249ebaf7a8713761a0df51.png)

</div>

</div>


### format: auto, str, dictionary | _named_

The image's format.

By default, the format is detected automatically. Typically, you thus
only need to specify this when providing raw bytes as the
[`source`](/reference/visualize/image/#parameters-source) (even then,
Typst will try to figure out the format automatically, but that's not
always possible).

Supported formats are <span class="typ-str">`"png"`</span>,
<span class="typ-str">`"jpg"`</span>,
<span class="typ-str">`"gif"`</span>,
<span class="typ-str">`"svg"`</span>,
<span class="typ-str">`"webp"`</span> as well as raw pixel data.
Embedding PDFs as images is [not currently
supported](https://github.com/typst/typst/issues/145).

When providing raw pixel data as the `source`, you must specify a
dictionary with the following keys as the `format`:

- `encoding` ([str](/reference/foundations/str/ "str")): The encoding of
  the pixel data. One of:
  - <span class="typ-str">`"rgb8"`</span> (three 8-bit channels: red,
    green, blue)
  - <span class="typ-str">`"rgba8"`</span> (four 8-bit channels: red,
    green, blue, alpha)
  - <span class="typ-str">`"luma8"`</span> (one 8-bit channel)
  - <span class="typ-str">`"lumaa8"`</span> (two 8-bit channels: luma
    and alpha)
- `width` ([int](/reference/foundations/int/ "int")): The pixel width of
  the image.
- `height` ([int](/reference/foundations/int/ "int")): The pixel height
  of the image.

The pixel width multiplied by the height multiplied by the channel count
for the specified encoding must then match the `source` data.


#### Example

<div class="previewed-code">

    #image(
      read(
        "tetrahedron.svg",
        encoding: none,
      ),
      format: "svg",
      width: 2cm,
    )

    #image(
      bytes(range(16).map(x => x * 16)),
      format: (
        encoding: "luma8",
        width: 4,
        height: 4,
      ),
      width: 2cm,
    )

<div class="preview">

![Preview](/assets/10ff96fc3a10fde3da637ec12b56637a.png)

</div>

</div>


### width: auto, relative | _named_

The width of the image.


### height: auto, relative, fraction | _named_

The height of the image.


### alt: none, str | _named_

A text describing the image.


### fit: str | _named_

How the image should adjust itself to a given area (the area is defined
by the `width` and `height` fields). Note that `fit` doesn't visually
change anything if the area's aspect ratio is the same as the image's
one.


#### Example

<div class="previewed-code">

    #set page(width: 300pt, height: 50pt, margin: 10pt)
    #image("tiger.jpg", width: 100%, fit: "cover")
    #image("tiger.jpg", width: 100%, fit: "contain")
    #image("tiger.jpg", width: 100%, fit: "stretch")

<div class="preview">

![Preview](/assets/a194706a6a99674a7fb55f288a8631c6.png)

</div>

</div>


### scaling: auto, str | _named_

A hint to viewers how they should scale the image.

When set to <span class="typ-key">`auto`</span>, the default is left up
to the viewer. For PNG export, Typst will default to smooth scaling,
like most PDF and SVG viewers.

*Note:* The exact look may differ across PDF viewers.


### icc: auto, str, bytes | _named_

An ICC profile for the image.

ICC profiles define how to interpret the colors in an image. When set to
<span class="typ-key">`auto`</span>, Typst will try to extract an ICC
profile from the image.


## Definitions


### decode

```
image.decode(
    str bytes
    format: auto str dictionary
    width: auto relative
    height: auto relative fraction
    alt: none str
    fit: str
    scaling: auto str
) -> content
```
Decode a raster or vector graphic from bytes or a string.


##### Parameters


##### data: str, bytes | _required_ _positional_

The data to decode as an image. Can be a string for SVGs.


##### format: auto, str, dictionary | _named_

The image's format. Detected automatically by default.


##### width: auto, relative | _named_

The width of the image.


##### height: auto, relative, fraction | _named_

The height of the image.


##### alt: none, str | _named_

A text describing the image.


##### fit: str | _named_

How the image should adjust itself to a given area.


##### scaling: auto, str | _named_

A hint to viewers how they should scale the image.

