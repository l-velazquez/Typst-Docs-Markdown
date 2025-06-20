
# sizes

Forced size styles for expressions within formulas.

These functions allow manual configuration of the size of equation
elements to make them look as in a display/inline equation or as if used
in a root or sub/superscripts.

## display

```
math.display(
    content
    cramped: bool
) -> content
```
Forced display style in math.

This is the normal size for block equations.


#### Parameters


#### body: content | _required_ _positional_

The content to size.


#### cramped: bool | _named_

Whether to impose a height restriction for exponents, like regular sub-
and superscripts do.


### Example

<div class="previewed-code">

    $sum_i x_i/2 = display(sum_i x_i/2)$

<div class="preview">

![Preview](/assets/2b0ff12851291bbf6c19c8a6e5b87b4a.png)

</div>

</div>


## inline

```
math.inline(
    content
    cramped: bool
) -> content
```
Forced inline (text) style in math.

This is the normal size for inline equations.


#### Parameters


#### body: content | _required_ _positional_

The content to size.


#### cramped: bool | _named_

Whether to impose a height restriction for exponents, like regular sub-
and superscripts do.


### Example

<div class="previewed-code">

    $ sum_i x_i/2
        = inline(sum_i x_i/2) $

<div class="preview">

![Preview](/assets/ca187288080f6bcfd264bcfb9cdb4da8.png)

</div>

</div>


## script

```
math.script(
    content
    cramped: bool
) -> content
```
Forced script style in math.

This is the smaller size used in powers or sub- or superscripts.


#### Parameters


#### body: content | _required_ _positional_

The content to size.


#### cramped: bool | _named_

Whether to impose a height restriction for exponents, like regular sub-
and superscripts do.


### Example

<div class="previewed-code">

    $sum_i x_i/2 = script(sum_i x_i/2)$

<div class="preview">

![Preview](/assets/5003b4082132e3646b44993ac60fe58e.png)

</div>

</div>


## sscript

```
math.sscript(
    content
    cramped: bool
) -> content
```
Forced second script style in math.

This is the smallest size, used in second-level sub- and superscripts
(script of the script).


#### Parameters


#### body: content | _required_ _positional_

The content to size.


#### cramped: bool | _named_

Whether to impose a height restriction for exponents, like regular sub-
and superscripts do.


### Example

<div class="previewed-code">

    $sum_i x_i/2 = sscript(sum_i x_i/2)$

<div class="preview">

![Preview](/assets/129983a09889adf6cdee40342a6eee8f.png)

</div>

</div>

