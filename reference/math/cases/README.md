
# cases

```
math.cases(
    delim: none str array symbol
    reverse: bool
    gap: relative
    content
) -> content
```
A case distinction.

Content across different branches can be aligned with the `&` symbol.

## Example

<div class="previewed-code">

    $ f(x, y) := cases(
      1 "if" (x dot y)/2 <= 0,
      2 "if" x "is even",
      3 "if" x in NN,
      4 "else",
    ) $

<div class="preview">

![Preview](/assets/d17d4014f0e278177d8e26b02a9734f8.png)

</div>

</div>


### Parameters


### delim: none, str, array, symbol | _named_

The delimiter to use.

Can be a single character specifying the left delimiter, in which case
the right delimiter is inferred. Otherwise, can be an array containing a
left and a right delimiter.


#### Example

<div class="previewed-code">

    #set math.cases(delim: "[")
    $ x = cases(1, 2) $

<div class="preview">

![Preview](/assets/6c4add3875963902d22adb31b49798e5.png)

</div>

</div>


### reverse: bool | _named_

Whether the direction of cases should be reversed.


#### Example

<div class="previewed-code">

    #set math.cases(reverse: true)
    $ cases(1, 2) = x $

<div class="preview">

![Preview](/assets/cfa01064a26c1fd9ccf797ba030d211a.png)

</div>

</div>


### gap: relative | _named_

The gap between branches.


#### Example

<div class="previewed-code">

    #set math.cases(gap: 1em)
    $ x = cases(1, 2) $

<div class="preview">

![Preview](/assets/fb1b1c7f3447e03c3a622e530afa6457.png)

</div>

</div>


### children: content | _required_ _positional_

The branches of the case distinction.

