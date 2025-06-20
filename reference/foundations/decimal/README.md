
# Decimal

A fixed-point decimal number type.

This type should be used for precise arithmetic operations on numbers
represented in base 10. A typical use case is representing currency.

## Example

<div class="previewed-code">

    Decimal: #(decimal("0.1") + decimal("0.2")) \
    Float: #(0.1 + 0.2)

<div class="preview">

![Preview](/assets/5b7d4abe1e81bdf2204e021eab6b8811.png)

</div>

</div>

## Construction and casts

To create a decimal number, use the
<span class="typ-func">`decimal`</span><span class="typ-punct">`(`</span>`string`<span class="typ-punct">`)`</span>
constructor, such as in
<span class="typ-func">`decimal`</span><span class="typ-punct">`(`</span><span class="typ-str">`"3.141592653"`</span><span class="typ-punct">`)`</span>
**(note the double quotes!)**. This constructor preserves all given
fractional digits, provided they are representable as per the limits
specified below (otherwise, an error is raised).

You can also convert any [integer](/reference/foundations/int/) to a
decimal with the
<span class="typ-func">`decimal`</span><span class="typ-punct">`(`</span>`int`<span class="typ-punct">`)`</span>
constructor, e.g.
<span class="typ-func">`decimal`</span><span class="typ-punct">`(`</span><span class="typ-num">`59`</span><span class="typ-punct">`)`</span>.
However, note that constructing a decimal from a [floating-point
number](/reference/foundations/float/), while supported, **is an
imprecise conversion and therefore discouraged.** A warning will be
raised if Typst detects that there was an accidental `float` to
`decimal` cast through its constructor, e.g. if writing
<span class="typ-func">`decimal`</span><span class="typ-punct">`(`</span><span class="typ-num">`3.14`</span><span class="typ-punct">`)`</span>
(note the lack of double quotes, indicating this is an accidental
`float` cast and therefore imprecise). It is recommended to use strings
for constant decimal values instead (e.g.
<span class="typ-func">`decimal`</span><span class="typ-punct">`(`</span><span class="typ-str">`"3.14"`</span><span class="typ-punct">`)`</span>).

The precision of a `float` to `decimal` cast can be slightly improved by
rounding the result to 15 digits with
[`calc.round`](/reference/foundations/calc/#functions-round), but there
are still no precision guarantees for that kind of conversion.

## Operations

Basic arithmetic operations are supported on two decimals and on pairs
of decimals and integers.

Built-in operations between `float` and `decimal` are not supported in
order to guard against accidental loss of precision. They will raise an
error instead.

Certain `calc` functions, such as trigonometric functions and power
between two real numbers, are also only supported for `float` (although
raising `decimal` to integer exponents is supported). You can opt into
potentially imprecise operations with the
<span class="typ-func">`float`</span><span class="typ-punct">`(`</span>`decimal`<span class="typ-punct">`)`</span>
constructor, which casts the `decimal` number into a `float`, allowing
for operations without precision guarantees.

## Displaying decimals

To display a decimal, simply insert the value into the document. To only
display a certain number of digits,
[round](/reference/foundations/calc/#functions-round) the decimal first.
Localized formatting of decimals and other numbers is not yet supported,
but planned for the future.

You can convert decimals to strings using the
[`str`](/reference/foundations/str/ "`str`") constructor. This way, you
can post-process the displayed representation, e.g. to replace the
period with a comma (as a stand-in for proper built-in localization to
languages that use the comma).

## Precision and limits

A `decimal` number has a limit of 28 to 29 significant base-10 digits.
This includes the sum of digits before and after the decimal point. As
such, numbers with more fractional digits have a smaller range. The
maximum and minimum `decimal` numbers have a value of
<span class="typ-num">`79228162514264337593543950335`</span> and
<span class="typ-op">`-`</span><span class="typ-num">`79228162514264337593543950335`</span>
respectively. In contrast with
[`float`](/reference/foundations/float/ "`float`"), this type does not
support infinity or NaN, so overflowing or underflowing operations will
raise an error.

Typical operations between `decimal` numbers, such as addition,
multiplication, and [power](/reference/foundations/calc/#functions-pow)
to an integer, will be highly precise due to their fixed-point
representation. Note, however, that multiplication and division may not
preserve all digits in some edge cases: while they are considered
precise, digits past the limits specified above are rounded off and
lost, so some loss of precision beyond the maximum representable digits
is possible. Note that this behavior can be observed not only when
dividing, but also when multiplying by numbers between 0 and 1, as both
operations can push a number's fractional digits beyond the limits
described above, leading to rounding. When those two operations do not
surpass the digit limits, they are fully precise.


## decimal

```
decimal(
    bool int float str decimal
) -> decimal
```
Converts a value to a `decimal`.

It is recommended to use a string to construct the decimal number, or an
[integer](/reference/foundations/int/) (if desired). The string must
contain a number in the format <span class="typ-str">`"3.14159"`</span>
(or <span class="typ-str">`"-3.141519"`</span> for negative numbers).
The fractional digits are fully preserved; if that's not possible due to
the limit of significant digits (around 28 to 29) having been reached,
an error is raised as the given decimal number wouldn't be
representable.

While this constructor can be used with [floating-point
numbers](/reference/foundations/float/) to cast them to `decimal`, doing
so is **discouraged** as **this cast is inherently imprecise.** It is
easy to accidentally perform this cast by writing
<span class="typ-func">`decimal`</span><span class="typ-punct">`(`</span><span class="typ-num">`1.234`</span><span class="typ-punct">`)`</span>
(note the lack of double quotes), which is why Typst will emit a warning
in that case. Please write
<span class="typ-func">`decimal`</span><span class="typ-punct">`(`</span><span class="typ-str">`"1.234"`</span><span class="typ-punct">`)`</span>
instead for that particular case (initialization of a constant decimal).
Also note that floats that are NaN or infinite cannot be cast to
decimals and will raise an error.


#### Parameters


#### value: bool, int, float, str, decimal | _required_ _positional_

The value that should be converted to a decimal.


### Example

<div class="previewed-code">

    #decimal("1.222222222222222")

<div class="preview">

![Preview](/assets/45faa507ce50e6521579e6c9abb4659a.png)

</div>

</div>


## Definitions

