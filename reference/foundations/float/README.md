
# Float

A floating-point number.

A limited-precision representation of a real number. Typst uses 64 bits
to store floats. Wherever a float is expected, you can also pass an
[integer](/reference/foundations/int/).

You can convert a value to a float with this type's constructor.

NaN and positive infinity are available as
`float`<span class="typ-punct">`.`</span>`nan` and
`float`<span class="typ-punct">`.`</span>`inf` respectively.

## Example

<div class="previewed-code">

    #3.14 \
    #1e4 \
    #(10 / 4)

<div class="preview">

![Preview](/assets/3a1ecfc8f2a14871dcc151f80926f42b.png)

</div>

</div>


## float

```
float(
    bool int float ratio str decimal
) -> float
```
Converts a value to a float.

- Booleans are converted to `0.0` or `1.0`.
- Integers are converted to the closest 64-bit float. For integers with
  absolute value less than
  `calc`<span class="typ-punct">`.`</span><span class="typ-func">`pow`</span><span class="typ-punct">`(`</span><span class="typ-num">`2`</span><span class="typ-punct">`,`</span>` `<span class="typ-num">`53`</span><span class="typ-punct">`)`</span>,
  this conversion is exact.
- Ratios are divided by 100%.
- Strings are parsed in base 10 to the closest 64-bit float. Exponential
  notation is supported.


#### Parameters


#### value: bool, int, float, ratio, str, decimal | _required_ _positional_

The value that should be converted to a float.


### Example

<div class="previewed-code">

    #float(false) \
    #float(true) \
    #float(4) \
    #float(40%) \
    #float("2.7") \
    #float("1e5")

<div class="preview">

![Preview](/assets/3cc6be1ea65a2f8fbe14dff52343876a.png)

</div>

</div>


## Definitions


### is-nan

```
float.is-nan(
) -> bool
```
Checks if a float is not a number.

In IEEE 754, more than one bit pattern represents a NaN. This function
returns `true` if the float is any of those bit patterns.


##### Parameters


#### Example

<div class="previewed-code">

    #float.is-nan(0) \
    #float.is-nan(1) \
    #float.is-nan(float.nan)

<div class="preview">

![Preview](/assets/f6377c8713dcba71fb09d0925d677577.png)

</div>

</div>


### is-infinite

```
float.is-infinite(
) -> bool
```
Checks if a float is infinite.

Floats can represent positive infinity and negative infinity. This
function returns <span class="typ-key">`true`</span> if the float is an
infinity.


##### Parameters


#### Example

<div class="previewed-code">

    #float.is-infinite(0) \
    #float.is-infinite(1) \
    #float.is-infinite(float.inf)

<div class="preview">

![Preview](/assets/8a0a86fa68abec5eb9e8923c3f4eee.png)

</div>

</div>


### signum

```
float.signum(
) -> float
```
Calculates the sign of a floating point number.

- If the number is positive (including
  <span class="typ-op">`+`</span><span class="typ-num">`0.0`</span>),
  returns <span class="typ-num">`1.0`</span>.
- If the number is negative (including
  <span class="typ-op">`-`</span><span class="typ-num">`0.0`</span>),
  returns
  <span class="typ-op">`-`</span><span class="typ-num">`1.0`</span>.
- If the number is NaN, returns
  `float`<span class="typ-punct">`.`</span>`nan`.


##### Parameters


#### Example

<div class="previewed-code">

    #(5.0).signum() \
    #(-5.0).signum() \
    #(0.0).signum() \
    #float.nan.signum()

<div class="preview">

![Preview](/assets/1c7a7ea657572682dba8012c83fda699.png)

</div>

</div>


### from-bytes

```
float.from-bytes(
    bytes
    endian: str
) -> float
```
Interprets bytes as a float.


##### Parameters


##### bytes: bytes | _required_ _positional_

The bytes that should be converted to a float.

Must have a length of either 4 or 8. The bytes are then interpreted in
[IEEE 754](https://en.wikipedia.org/wiki/IEEE_754)'s binary32
(single-precision) or binary64 (double-precision) format depending on
the length of the bytes.


##### endian: str | _named_

The endianness of the conversion.


#### Example

<div class="previewed-code">

    #float.from-bytes(bytes((0, 0, 0, 0, 0, 0, 240, 63))) \
    #float.from-bytes(bytes((63, 240, 0, 0, 0, 0, 0, 0)), endian: "big")

<div class="preview">

![Preview](/assets/4db0a29eaaeeef524a3a6ef790e25877.png)

</div>

</div>


### to-bytes

```
float.to-bytes(
    endian: str
    size: int
) -> bytes
```
Converts a float to bytes.


##### Parameters


##### endian: str | _named_

The endianness of the conversion.


##### size: int | _named_

The size of the resulting bytes.

This must be either 4 or 8. The call will return the representation of
this float in either [IEEE
754](https://en.wikipedia.org/wiki/IEEE_754)'s binary32
(single-precision) or binary64 (double-precision) format depending on
the provided size.


#### Example

<div class="previewed-code">

    #array(1.0.to-bytes(endian: "big")) \
    #array(1.0.to-bytes())

<div class="preview">

![Preview](/assets/a32cf9d2d1c83a84118ffe5633a2486c.png)

</div>

</div>

