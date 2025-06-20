
# frac

```
math.frac(
    content
    content
) -> content
```
A mathematical fraction.

## Example

<div class="previewed-code">

    $ 1/2 < (x+1)/2 $
    $ ((x+1)) / 2 = frac(a, b) $

<div class="preview">

![Preview](/assets/f5116cafe55239b89e94f6f836bafecd.png)

</div>

</div>

## Syntax

This function also has dedicated syntax: Use a slash to turn
neighbouring expressions into a fraction. Multiple atoms can be grouped
into a single expression using round grouping parentheses. Such
parentheses are removed from the output, but you can nest multiple to
force them.


### Parameters


### num: content | _required_ _positional_

The fraction's numerator.


### denom: content | _required_ _positional_

The fraction's denominator.

