
# calc

Module for calculations and processing of numeric values.

These definitions are part of the `calc` module and not imported by
default. In addition to the functions listed below, the `calc` module
also defines the constants `pi`, `tau`, `e`, and `inf`.

## abs

```
calc.abs(
    int float length angle ratio fraction decimal
) -> any
```
Calculates the absolute value of a numeric value.


#### Parameters


#### value: int, float, length, angle, ratio, fraction, decimal | _required_ _positional_

The value whose absolute value to calculate.


### Example

<div class="previewed-code">

    #calc.abs(-5) \
    #calc.abs(5pt - 2cm) \
    #calc.abs(2fr) \
    #calc.abs(decimal("-342.440"))

<div class="preview">

![Preview](/assets/d673cd93e440c975041eb02ccf20a752.png)

</div>

</div>


## pow

```
calc.pow(
    int float decimal
    int float
) -> int float decimal
```
Raises a value to some exponent.


#### Parameters


#### base: int, float, decimal | _required_ _positional_

The base of the power.

If this is a [`decimal`](/reference/foundations/decimal/ "`decimal`"),
the exponent can only be an [integer](/reference/foundations/int/).


#### exponent: int, float | _required_ _positional_

The exponent of the power.


### Example

<div class="previewed-code">

    #calc.pow(2, 3) \
    #calc.pow(decimal("2.5"), 2)

<div class="preview">

![Preview](/assets/610a0eb053713c4816d1bfa7f41fd5ac.png)

</div>

</div>


## exp

```
calc.exp(
    int float
) -> float
```
Raises a value to some exponent of e.


#### Parameters


#### exponent: int, float | _required_ _positional_

The exponent of the power.


### Example

<div class="previewed-code">

    #calc.exp(1)

<div class="preview">

![Preview](/assets/f78e20399a0a10231e8c567e0ecb8cf.png)

</div>

</div>


## sqrt

```
calc.sqrt(
    int float
) -> float
```
Calculates the square root of a number.


#### Parameters


#### value: int, float | _required_ _positional_

The number whose square root to calculate. Must be non-negative.


### Example

<div class="previewed-code">

    #calc.sqrt(16) \
    #calc.sqrt(2.5)

<div class="preview">

![Preview](/assets/ad28f3d5b5a490a62ac665a3c5ecc54f.png)

</div>

</div>


## root

```
calc.root(
    float
    int
) -> float
```
Calculates the real nth root of a number.

If the number is negative, then n must be odd.


#### Parameters


#### radicand: float | _required_ _positional_

The expression to take the root of


#### index: int | _required_ _positional_

Which root of the radicand to take


### Example

<div class="previewed-code">

    #calc.root(16.0, 4) \
    #calc.root(27.0, 3)

<div class="preview">

![Preview](/assets/837af196aa131a0a028cbb6213b6dc28.png)

</div>

</div>


## sin

```
calc.sin(
    int float angle
) -> float
```
Calculates the sine of an angle.

When called with an integer or a float, they will be interpreted as
radians.


#### Parameters


#### angle: int, float, angle | _required_ _positional_

The angle whose sine to calculate.


### Example

<div class="previewed-code">

    #calc.sin(1.5) \
    #calc.sin(90deg)

<div class="preview">

![Preview](/assets/d1cfe7fae09be11ecb26e1681210bd9.png)

</div>

</div>


## cos

```
calc.cos(
    int float angle
) -> float
```
Calculates the cosine of an angle.

When called with an integer or a float, they will be interpreted as
radians.


#### Parameters


#### angle: int, float, angle | _required_ _positional_

The angle whose cosine to calculate.


### Example

<div class="previewed-code">

    #calc.cos(1.5) \
    #calc.cos(90deg)

<div class="preview">

![Preview](/assets/45079cea074917942f470664bc8fb9d2.png)

</div>

</div>


## tan

```
calc.tan(
    int float angle
) -> float
```
Calculates the tangent of an angle.

When called with an integer or a float, they will be interpreted as
radians.


#### Parameters


#### angle: int, float, angle | _required_ _positional_

The angle whose tangent to calculate.


### Example

<div class="previewed-code">

    #calc.tan(1.5) \
    #calc.tan(90deg)

<div class="preview">

![Preview](/assets/32ee947cdff8e3ae0a261cbbf30be9ff.png)

</div>

</div>


## asin

```
calc.asin(
    int float
) -> angle
```
Calculates the arcsine of a number.


#### Parameters


#### value: int, float | _required_ _positional_

The number whose arcsine to calculate. Must be between -1 and 1.


### Example

<div class="previewed-code">

    #calc.asin(0) \
    #calc.asin(1)

<div class="preview">

![Preview](/assets/47e7cfd9bb0aa9e93a0ab1d1c6c9a5bd.png)

</div>

</div>


## acos

```
calc.acos(
    int float
) -> angle
```
Calculates the arccosine of a number.


#### Parameters


#### value: int, float | _required_ _positional_

The number whose arcsine to calculate. Must be between -1 and 1.


### Example

<div class="previewed-code">

    #calc.acos(0) \
    #calc.acos(1)

<div class="preview">

![Preview](/assets/df8b6fb603d1c7d65bd28150b5d9049e.png)

</div>

</div>


## atan

```
calc.atan(
    int float
) -> angle
```
Calculates the arctangent of a number.


#### Parameters


#### value: int, float | _required_ _positional_

The number whose arctangent to calculate.


### Example

<div class="previewed-code">

    #calc.atan(0) \
    #calc.atan(1)

<div class="preview">

![Preview](/assets/2ace6207833059734055779232284324.png)

</div>

</div>


## atan2

```
calc.atan2(
    int float
    int float
) -> angle
```
Calculates the four-quadrant arctangent of a coordinate.

The arguments are `(x, y)`, not `(y, x)`.


#### Parameters


#### x: int, float | _required_ _positional_

The X coordinate.


#### y: int, float | _required_ _positional_

The Y coordinate.


### Example

<div class="previewed-code">

    #calc.atan2(1, 1) \
    #calc.atan2(-2, -3)

<div class="preview">

![Preview](/assets/4773e07ed6084d1b122d805e42a29edf.png)

</div>

</div>


## sinh

```
calc.sinh(
    float
) -> float
```
Calculates the hyperbolic sine of a hyperbolic angle.


#### Parameters


#### value: float | _required_ _positional_

The hyperbolic angle whose hyperbolic sine to calculate.


### Example

<div class="previewed-code">

    #calc.sinh(0) \
    #calc.sinh(1.5)

<div class="preview">

![Preview](/assets/4a2ecb56bdb6d32fb28ebe9fac3e6661.png)

</div>

</div>


## cosh

```
calc.cosh(
    float
) -> float
```
Calculates the hyperbolic cosine of a hyperbolic angle.


#### Parameters


#### value: float | _required_ _positional_

The hyperbolic angle whose hyperbolic cosine to calculate.


### Example

<div class="previewed-code">

    #calc.cosh(0) \
    #calc.cosh(1.5)

<div class="preview">

![Preview](/assets/56eb7fba31d6f1e9c901d388f79bfa6e.png)

</div>

</div>


## tanh

```
calc.tanh(
    float
) -> float
```
Calculates the hyperbolic tangent of an hyperbolic angle.


#### Parameters


#### value: float | _required_ _positional_

The hyperbolic angle whose hyperbolic tangent to calculate.


### Example

<div class="previewed-code">

    #calc.tanh(0) \
    #calc.tanh(1.5)

<div class="preview">

![Preview](/assets/f289872963045e1f65b5cb16a66e110d.png)

</div>

</div>


## log

```
calc.log(
    int float
    base: float
) -> float
```
Calculates the logarithm of a number.

If the base is not specified, the logarithm is calculated in base 10.


#### Parameters


#### value: int, float | _required_ _positional_

The number whose logarithm to calculate. Must be strictly positive.


#### base: float | _named_

The base of the logarithm. May not be zero.


### Example

<div class="previewed-code">

    #calc.log(100)

<div class="preview">

![Preview](/assets/e2d7be7cfdc41587fd0857d74cd78b6e.png)

</div>

</div>


## ln

```
calc.ln(
    int float
) -> float
```
Calculates the natural logarithm of a number.


#### Parameters


#### value: int, float | _required_ _positional_

The number whose logarithm to calculate. Must be strictly positive.


### Example

<div class="previewed-code">

    #calc.ln(calc.e)

<div class="preview">

![Preview](/assets/6a1320737d2e55a5cc749c787fd6fbea.png)

</div>

</div>


## fact

```
calc.fact(
    int
) -> int
```
Calculates the factorial of a number.


#### Parameters


#### number: int | _required_ _positional_

The number whose factorial to calculate. Must be non-negative.


### Example

<div class="previewed-code">

    #calc.fact(5)

<div class="preview">

![Preview](/assets/1f1d2fc9d5edb4d45425b6dd0d2bc697.png)

</div>

</div>


## perm

```
calc.perm(
    int
    int
) -> int
```
Calculates a permutation.

Returns the `k`-permutation of `n`, or the number of ways to choose `k`
items from a set of `n` with regard to order.


#### Parameters


#### base: int | _required_ _positional_

The base number. Must be non-negative.


#### numbers: int | _required_ _positional_

The number of permutations. Must be non-negative.


### Example

<div class="previewed-code">

    $ "perm"(n, k) &= n!/((n - k)!) \
      "perm"(5, 3) &= #calc.perm(5, 3) $

<div class="preview">

![Preview](/assets/ee601fe2c3e685eeab28acda98113e88.png)

</div>

</div>


## binom

```
calc.binom(
    int
    int
) -> int
```
Calculates a binomial coefficient.

Returns the `k`-combination of `n`, or the number of ways to choose `k`
items from a set of `n` without regard to order.


#### Parameters


#### n: int | _required_ _positional_

The upper coefficient. Must be non-negative.


#### k: int | _required_ _positional_

The lower coefficient. Must be non-negative.


### Example

<div class="previewed-code">

    #calc.binom(10, 5)

<div class="preview">

![Preview](/assets/ddebd0735304e1e42a6f35e1ae627994.png)

</div>

</div>


## gcd

```
calc.gcd(
    int
    int
) -> int
```
Calculates the greatest common divisor of two integers.


#### Parameters


#### a: int | _required_ _positional_

The first integer.


#### b: int | _required_ _positional_

The second integer.


### Example

<div class="previewed-code">

    #calc.gcd(7, 42)

<div class="preview">

![Preview](/assets/a8e2304325e90a7ad290e3403a720380.png)

</div>

</div>


## lcm

```
calc.lcm(
    int
    int
) -> int
```
Calculates the least common multiple of two integers.


#### Parameters


#### a: int | _required_ _positional_

The first integer.


#### b: int | _required_ _positional_

The second integer.


### Example

<div class="previewed-code">

    #calc.lcm(96, 13)

<div class="preview">

![Preview](/assets/6c499406e76ffdf79446f73811ba6b8.png)

</div>

</div>


## floor

```
calc.floor(
    int float decimal
) -> int
```
Rounds a number down to the nearest integer.

If the number is already an integer, it is returned unchanged.

Note that this function will always return an
[integer](/reference/foundations/int/), and will error if the resulting
[`float`](/reference/foundations/float/ "`float`") or
[`decimal`](/reference/foundations/decimal/ "`decimal`") is larger than
the maximum 64-bit signed integer or smaller than the minimum for that
type.


#### Parameters


#### value: int, float, decimal | _required_ _positional_

The number to round down.


### Example

<div class="previewed-code">

    #calc.floor(500.1)
    #assert(calc.floor(3) == 3)
    #assert(calc.floor(3.14) == 3)
    #assert(calc.floor(decimal("-3.14")) == -4)

<div class="preview">

![Preview](/assets/de93166c89228f4f7046079b0f8dd542.png)

</div>

</div>


## ceil

```
calc.ceil(
    int float decimal
) -> int
```
Rounds a number up to the nearest integer.

If the number is already an integer, it is returned unchanged.

Note that this function will always return an
[integer](/reference/foundations/int/), and will error if the resulting
[`float`](/reference/foundations/float/ "`float`") or
[`decimal`](/reference/foundations/decimal/ "`decimal`") is larger than
the maximum 64-bit signed integer or smaller than the minimum for that
type.


#### Parameters


#### value: int, float, decimal | _required_ _positional_

The number to round up.


### Example

<div class="previewed-code">

    #calc.ceil(500.1)
    #assert(calc.ceil(3) == 3)
    #assert(calc.ceil(3.14) == 4)
    #assert(calc.ceil(decimal("-3.14")) == -3)

<div class="preview">

![Preview](/assets/5d517a01bc439d7c26ada18df8487532.png)

</div>

</div>


## trunc

```
calc.trunc(
    int float decimal
) -> int
```
Returns the integer part of a number.

If the number is already an integer, it is returned unchanged.

Note that this function will always return an
[integer](/reference/foundations/int/), and will error if the resulting
[`float`](/reference/foundations/float/ "`float`") or
[`decimal`](/reference/foundations/decimal/ "`decimal`") is larger than
the maximum 64-bit signed integer or smaller than the minimum for that
type.


#### Parameters


#### value: int, float, decimal | _required_ _positional_

The number to truncate.


### Example

<div class="previewed-code">

    #calc.trunc(15.9)
    #assert(calc.trunc(3) == 3)
    #assert(calc.trunc(-3.7) == -3)
    #assert(calc.trunc(decimal("8493.12949582390")) == 8493)

<div class="preview">

![Preview](/assets/d0049da245a68400b1a7771b741cd28b.png)

</div>

</div>


## fract

```
calc.fract(
    int float decimal
) -> int float decimal
```
Returns the fractional part of a number.

If the number is an integer, returns `0`.


#### Parameters


#### value: int, float, decimal | _required_ _positional_

The number to truncate.


### Example

<div class="previewed-code">

    #calc.fract(-3.1)
    #assert(calc.fract(3) == 0)
    #assert(calc.fract(decimal("234.23949211")) == decimal("0.23949211"))

<div class="preview">

![Preview](/assets/dd31885a1d8c1061480c007c0b59c440.png)

</div>

</div>


## round

```
calc.round(
    int float decimal
    digits: int
) -> int float decimal
```
Rounds a number to the nearest integer.

Half-integers are rounded away from zero.

Optionally, a number of decimal places can be specified. If negative,
its absolute value will indicate the amount of significant integer
digits to remove before the decimal point.

Note that this function will return the same type as the operand. That
is, applying `round` to a
[`float`](/reference/foundations/float/ "`float`") will return a
`float`, and to a
[`decimal`](/reference/foundations/decimal/ "`decimal`"), another
`decimal`. You may explicitly convert the output of this function to an
integer with [`int`](/reference/foundations/int/ "`int`"), but note that
such a conversion will error if the `float` or `decimal` is larger than
the maximum 64-bit signed integer or smaller than the minimum integer.

In addition, this function can error if there is an attempt to round
beyond the maximum or minimum integer or `decimal`. If the number is a
`float`, such an attempt will cause
`float`<span class="typ-punct">`.`</span>`inf` or
<span class="typ-op">`-`</span>`float`<span class="typ-punct">`.`</span>`inf`
to be returned for maximum and minimum respectively.


#### Parameters


#### value: int, float, decimal | _required_ _positional_

The number to round.


#### digits: int | _named_

If positive, the number of decimal places.

If negative, the number of significant integer digits that should be
removed before the decimal point.


### Example

<div class="previewed-code">

    #calc.round(3.1415, digits: 2)
    #assert(calc.round(3) == 3)
    #assert(calc.round(3.14) == 3)
    #assert(calc.round(3.5) == 4.0)
    #assert(calc.round(3333.45, digits: -2) == 3300.0)
    #assert(calc.round(-48953.45, digits: -3) == -49000.0)
    #assert(calc.round(3333, digits: -2) == 3300)
    #assert(calc.round(-48953, digits: -3) == -49000)
    #assert(calc.round(decimal("-6.5")) == decimal("-7"))
    #assert(calc.round(decimal("7.123456789"), digits: 6) == decimal("7.123457"))
    #assert(calc.round(decimal("3333.45"), digits: -2) == decimal("3300"))
    #assert(calc.round(decimal("-48953.45"), digits: -3) == decimal("-49000"))

<div class="preview">

![Preview](/assets/4b67d730d70fca54eaeaec25ed9469a0.png)

</div>

</div>


## clamp

```
calc.clamp(
    int float decimal
    int float decimal
    int float decimal
) -> int float decimal
```
Clamps a number between a minimum and maximum value.


#### Parameters


#### value: int, float, decimal | _required_ _positional_

The number to clamp.


#### min: int, float, decimal | _required_ _positional_

The inclusive minimum value.


#### max: int, float, decimal | _required_ _positional_

The inclusive maximum value.


### Example

<div class="previewed-code">

    #calc.clamp(5, 0, 4)
    #assert(calc.clamp(5, 0, 10) == 5)
    #assert(calc.clamp(5, 6, 10) == 6)
    #assert(calc.clamp(decimal("5.45"), 2, decimal("45.9")) == decimal("5.45"))
    #assert(calc.clamp(decimal("5.45"), decimal("6.75"), 12) == decimal("6.75"))

<div class="preview">

![Preview](/assets/213edda085367c7d5425fd04fd23dce9.png)

</div>

</div>


## min

```
calc.min(
    any
) -> any
```
Determines the minimum of a sequence of values.


#### Parameters


#### values: any | _required_ _positional_

The sequence of values from which to extract the minimum. Must not be
empty.


### Example

<div class="previewed-code">

    #calc.min(1, -3, -5, 20, 3, 6) \
    #calc.min("typst", "is", "cool")

<div class="preview">

![Preview](/assets/69f392ae374e01cff5473cd4da1c5422.png)

</div>

</div>


## max

```
calc.max(
    any
) -> any
```
Determines the maximum of a sequence of values.


#### Parameters


#### values: any | _required_ _positional_

The sequence of values from which to extract the maximum. Must not be
empty.


### Example

<div class="previewed-code">

    #calc.max(1, -3, -5, 20, 3, 6) \
    #calc.max("typst", "is", "cool")

<div class="preview">

![Preview](/assets/7cbdbb1568e2bb225b7e69185f0e217.png)

</div>

</div>


## even

```
calc.even(
    int
) -> bool
```
Determines whether an integer is even.


#### Parameters


#### value: int | _required_ _positional_

The number to check for evenness.


### Example

<div class="previewed-code">

    #calc.even(4) \
    #calc.even(5) \
    #range(10).filter(calc.even)

<div class="preview">

![Preview](/assets/61517eabdebf59e22801bc307aeaec00.png)

</div>

</div>


## odd

```
calc.odd(
    int
) -> bool
```
Determines whether an integer is odd.


#### Parameters


#### value: int | _required_ _positional_

The number to check for oddness.


### Example

<div class="previewed-code">

    #calc.odd(4) \
    #calc.odd(5) \
    #range(10).filter(calc.odd)

<div class="preview">

![Preview](/assets/e78c6254542743d14876022717403f8c.png)

</div>

</div>


## rem

```
calc.rem(
    int float decimal
    int float decimal
) -> int float decimal
```
Calculates the remainder of two numbers.

The value `calc.rem(x, y)` always has the same sign as `x`, and is
smaller in magnitude than `y`.

This can error if given a
[`decimal`](/reference/foundations/decimal/ "`decimal`") input and the
dividend is too small in magnitude compared to the divisor.


#### Parameters


#### dividend: int, float, decimal | _required_ _positional_

The dividend of the remainder.


#### divisor: int, float, decimal | _required_ _positional_

The divisor of the remainder.


### Example

<div class="previewed-code">

    #calc.rem(7, 3) \
    #calc.rem(7, -3) \
    #calc.rem(-7, 3) \
    #calc.rem(-7, -3) \
    #calc.rem(1.75, 0.5)

<div class="preview">

![Preview](/assets/87d90077c059ff8a9a6549bb59622981.png)

</div>

</div>


## div-euclid

```
calc.div-euclid(
    int float decimal
    int float decimal
) -> int float decimal
```
Performs euclidean division of two numbers.

The result of this computation is that of a division rounded to the
integer `n` such that the dividend is greater than or equal to `n` times
the divisor.


#### Parameters


#### dividend: int, float, decimal | _required_ _positional_

The dividend of the division.


#### divisor: int, float, decimal | _required_ _positional_

The divisor of the division.


### Example

<div class="previewed-code">

    #calc.div-euclid(7, 3) \
    #calc.div-euclid(7, -3) \
    #calc.div-euclid(-7, 3) \
    #calc.div-euclid(-7, -3) \
    #calc.div-euclid(1.75, 0.5) \
    #calc.div-euclid(decimal("1.75"), decimal("0.5"))

<div class="preview">

![Preview](/assets/e3de88195be86ab9661116a389316cfe.png)

</div>

</div>


## rem-euclid

```
calc.rem-euclid(
    int float decimal
    int float decimal
) -> int float decimal
```
This calculates the least nonnegative remainder of a division.

Warning: Due to a floating point round-off error, the remainder may
equal the absolute value of the divisor if the dividend is much smaller
in magnitude than the divisor and the dividend is negative. This only
applies for floating point inputs.

In addition, this can error if given a
[`decimal`](/reference/foundations/decimal/ "`decimal`") input and the
dividend is too small in magnitude compared to the divisor.


#### Parameters


#### dividend: int, float, decimal | _required_ _positional_

The dividend of the remainder.


#### divisor: int, float, decimal | _required_ _positional_

The divisor of the remainder.


### Example

<div class="previewed-code">

    #calc.rem-euclid(7, 3) \
    #calc.rem-euclid(7, -3) \
    #calc.rem-euclid(-7, 3) \
    #calc.rem-euclid(-7, -3) \
    #calc.rem-euclid(1.75, 0.5) \
    #calc.rem-euclid(decimal("1.75"), decimal("0.5"))

<div class="preview">

![Preview](/assets/cac5f61cb0beadf5800a29f08a061c5a.png)

</div>

</div>


## quo

```
calc.quo(
    int float decimal
    int float decimal
) -> int
```
Calculates the quotient (floored division) of two numbers.

Note that this function will always return an
[integer](/reference/foundations/int/), and will error if the resulting
[`float`](/reference/foundations/float/ "`float`") or
[`decimal`](/reference/foundations/decimal/ "`decimal`") is larger than
the maximum 64-bit signed integer or smaller than the minimum for that
type.


#### Parameters


#### dividend: int, float, decimal | _required_ _positional_

The dividend of the quotient.


#### divisor: int, float, decimal | _required_ _positional_

The divisor of the quotient.


### Example

<div class="previewed-code">

    $ "quo"(a, b) &= floor(a/b) \
      "quo"(14, 5) &= #calc.quo(14, 5) \
      "quo"(3.46, 0.5) &= #calc.quo(3.46, 0.5) $

<div class="preview">

![Preview](/assets/4848bce8e009c059a3418c08b43db5.png)

</div>

</div>


## norm

```
calc.norm(
    p: float
    float
) -> float
```
Calculates the p-norm of a sequence of values.


#### Parameters


#### p: float | _named_

The p value to calculate the p-norm of.


#### values: float | _required_ _positional_

The sequence of values from which to calculate the p-norm. Returns `0.0`
if empty.


### Example

<div class="previewed-code">

    #calc.norm(1, 2, -3, 0.5) \
    #calc.norm(p: 3, 1, 2)

<div class="preview">

![Preview](/assets/c838bb6a3d014d601035ea215b5bbe1c.png)

</div>

</div>

