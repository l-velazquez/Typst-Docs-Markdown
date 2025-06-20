
# Integer

A whole number.

The number can be negative, zero, or positive. As Typst uses 64 bits to
store integers, integers cannot be smaller than
<span class="typ-op">`-`</span><span class="typ-num">`9223372036854775808`</span>
or larger than <span class="typ-num">`9223372036854775807`</span>.
Integer literals are always positive, so a negative integer such as
<span class="typ-op">`-`</span><span class="typ-num">`1`</span> is
semantically the negation `-` of the positive literal `1`. A positive
integer greater than the maximum value and a negative integer less than
or equal to the minimum value cannot be represented as an integer
literal, and are instead parsed as a `float`. The minimum integer value
can still be obtained through integer arithmetic.

The number can also be specified as hexadecimal, octal, or binary by
starting it with a zero followed by either `x`, `o`, or `b`.

You can convert a value to an integer with this type's constructor.

## Example

<div class="previewed-code">

    #(1 + 2) \
    #(2 - 5) \
    #(3 + 4 < 8)

    #0xff \
    #0o10 \
    #0b1001

<div class="preview">

![Preview](/assets/c1fa714490d9acd7860c0dd18c480526.png)

</div>

</div>


## int

```
int(
    bool int float str decimal
) -> int
```
Converts a value to an integer. Raises an error if there is an attempt
to produce an integer larger than the maximum 64-bit signed integer or
smaller than the minimum 64-bit signed integer.

- Booleans are converted to `0` or `1`.
- Floats and decimals are truncated to the next 64-bit integer.
- Strings are parsed in base 10.


#### Parameters


#### value: bool, int, float, str, decimal | _required_ _positional_

The value that should be converted to an integer.


### Example

<div class="previewed-code">

    #int(false) \
    #int(true) \
    #int(2.7) \
    #int(decimal("3.8")) \
    #(int("27") + int("4"))

<div class="preview">

![Preview](/assets/e2f0ccff01ef1801aace21ddf72d8b41.png)

</div>

</div>


## Definitions


### signum

```
int.signum(
) -> int
```
Calculates the sign of an integer.

- If the number is positive, returns <span class="typ-num">`1`</span>.
- If the number is negative, returns
  <span class="typ-op">`-`</span><span class="typ-num">`1`</span>.
- If the number is zero, returns <span class="typ-num">`0`</span>.


##### Parameters


#### Example

<div class="previewed-code">

    #(5).signum() \
    #(-5).signum() \
    #(0).signum()

<div class="preview">

![Preview](/assets/562726d9517a67df2c82335941895a06.png)

</div>

</div>


### bit-not

```
int.bit-not(
) -> int
```
Calculates the bitwise NOT of an integer.

For the purposes of this function, the operand is treated as a signed
integer of 64 bits.


##### Parameters


#### Example

<div class="previewed-code">

    #4.bit-not() \
    #(-1).bit-not()

<div class="preview">

![Preview](/assets/dc060efa9e84fb3dd52c7e2f3725842a.png)

</div>

</div>


### bit-and

```
int.bit-and(
    int
) -> int
```
Calculates the bitwise AND between two integers.

For the purposes of this function, the operands are treated as signed
integers of 64 bits.


##### Parameters


##### rhs: int | _required_ _positional_

The right-hand operand of the bitwise AND.


#### Example

<div class="previewed-code">

    #128.bit-and(192)

<div class="preview">

![Preview](/assets/927c13ad6f976e3e6ca9b71dcdaedec2.png)

</div>

</div>


### bit-or

```
int.bit-or(
    int
) -> int
```
Calculates the bitwise OR between two integers.

For the purposes of this function, the operands are treated as signed
integers of 64 bits.


##### Parameters


##### rhs: int | _required_ _positional_

The right-hand operand of the bitwise OR.


#### Example

<div class="previewed-code">

    #64.bit-or(32)

<div class="preview">

![Preview](/assets/cda54a333b5f8fef1521f6cb5de24550.png)

</div>

</div>


### bit-xor

```
int.bit-xor(
    int
) -> int
```
Calculates the bitwise XOR between two integers.

For the purposes of this function, the operands are treated as signed
integers of 64 bits.


##### Parameters


##### rhs: int | _required_ _positional_

The right-hand operand of the bitwise XOR.


#### Example

<div class="previewed-code">

    #64.bit-xor(96)

<div class="preview">

![Preview](/assets/2943eab0e2f921759c1927c0845a4beb.png)

</div>

</div>


### bit-lshift

```
int.bit-lshift(
    int
) -> int
```
Shifts the operand's bits to the left by the specified amount.

For the purposes of this function, the operand is treated as a signed
integer of 64 bits. An error will occur if the result is too large to
fit in a 64-bit integer.


##### Parameters


##### shift: int | _required_ _positional_

The amount of bits to shift. Must not be negative.


#### Example

<div class="previewed-code">

    #33.bit-lshift(2) \
    #(-1).bit-lshift(3)

<div class="preview">

![Preview](/assets/9085484b226c6c6a4ade4fdfbb9f4ed8.png)

</div>

</div>


### bit-rshift

```
int.bit-rshift(
    int
    logical: bool
) -> int
```
Shifts the operand's bits to the right by the specified amount. Performs
an arithmetic shift by default (extends the sign bit to the left, such
that negative numbers stay negative), but that can be changed by the
`logical` parameter.

For the purposes of this function, the operand is treated as a signed
integer of 64 bits.


##### Parameters


##### shift: int | _required_ _positional_

The amount of bits to shift. Must not be negative.

Shifts larger than 63 are allowed and will cause the return value to
saturate. For non-negative numbers, the return value saturates at
<span class="typ-num">`0`</span>, while, for negative numbers, it
saturates at
<span class="typ-op">`-`</span><span class="typ-num">`1`</span> if
`logical` is set to <span class="typ-key">`false`</span>, or
<span class="typ-num">`0`</span> if it is
<span class="typ-key">`true`</span>. This behavior is consistent with
just applying this operation multiple times. Therefore, the shift will
always succeed.


##### logical: bool | _named_

Toggles whether a logical (unsigned) right shift should be performed
instead of arithmetic right shift. If this is
<span class="typ-key">`true`</span>, negative operands will not preserve
their sign bit, and bits which appear to the left after the shift will
be <span class="typ-num">`0`</span>. This parameter has no effect on
non-negative operands.


#### Example

<div class="previewed-code">

    #64.bit-rshift(2) \
    #(-8).bit-rshift(2) \
    #(-8).bit-rshift(2, logical: true)

<div class="preview">

![Preview](/assets/81e6da07e0993b30ed9ef7e30df8ed4e.png)

</div>

</div>


### from-bytes

```
int.from-bytes(
    bytes
    endian: str
    signed: bool
) -> int
```
Converts bytes to an integer.


##### Parameters


##### bytes: bytes | _required_ _positional_

The bytes that should be converted to an integer.

Must be of length at most 8 so that the result fits into a 64-bit signed
integer.


##### endian: str | _named_

The endianness of the conversion.


##### signed: bool | _named_

Whether the bytes should be treated as a signed integer. If this is
<span class="typ-key">`true`</span> and the most significant bit is set,
the resulting number will negative.


#### Example

<div class="previewed-code">

    #int.from-bytes(bytes((0, 0, 0, 0, 0, 0, 0, 1))) \
    #int.from-bytes(bytes((1, 0, 0, 0, 0, 0, 0, 0)), endian: "big")

<div class="preview">

![Preview](/assets/2342cf4345948a2d1fb61703db4728b0.png)

</div>

</div>


### to-bytes

```
int.to-bytes(
    endian: str
    size: int
) -> bytes
```
Converts an integer to bytes.


##### Parameters


##### endian: str | _named_

The endianness of the conversion.


##### size: int | _named_

The size in bytes of the resulting bytes (must be at least zero). If the
integer is too large to fit in the specified size, the conversion will
truncate the remaining bytes based on the endianness. To keep the same
resulting value, if the endianness is big-endian, the truncation will
happen at the rightmost bytes. Otherwise, if the endianness is
little-endian, the truncation will happen at the leftmost bytes.

Be aware that if the integer is negative and the size is not enough to
make the number fit, when passing the resulting bytes to
`int.from-bytes`, the resulting number might be positive, as the most
significant bit might not be set to 1.


#### Example

<div class="previewed-code">

    #array(10000.to-bytes(endian: "big")) \
    #array(10000.to-bytes(size: 4))

<div class="preview">

![Preview](/assets/145ee0196e1e54e1216232195f2f0122.png)

</div>

</div>

