
# eval

```
eval(
    str
    mode: str
    scope: dictionary
) -> any
```
Evaluates a string as Typst code.

This function should only be used as a last resort.

## Example

<div class="previewed-code">

    #eval("1 + 1") \
    #eval("(1, 2, 3, 4)").len() \
    #eval("*Markup!*", mode: "markup") \

<div class="preview">

![Preview](/assets/2997ea0d9ffb5751252b8ba6f78bef8f.png)

</div>

</div>


### Parameters


### source: str | _required_ _positional_

A string of Typst code to evaluate.


### mode: str | _named_

The [syntactical mode](/reference/syntax/#modes) in which the string is
parsed.


#### Example

<div class="previewed-code">

    #eval("= Heading", mode: "markup")
    #eval("1_2^3", mode: "math")

<div class="preview">

![Preview](/assets/e0e6267dbae8e994f5b5de63e11e70c8.png)

</div>

</div>


### scope: dictionary | _named_

A scope of definitions that are made available.


#### Example

<div class="previewed-code">

    #eval("x + 1", scope: (x: 2)) \
    #eval(
      "abc/xyz",
      mode: "math",
      scope: (
        abc: $a + b + c$,
        xyz: $x + y + z$,
      ),
    )

<div class="preview">

![Preview](/assets/d2f0fe3b3499c315f41aa9a6f3f4a4f4.png)

</div>

</div>

