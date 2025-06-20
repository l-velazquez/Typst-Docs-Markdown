
# roots

Square and non-square roots.

## Example

<div class="previewed-code">

    $ sqrt(3 - 2 sqrt(2)) = sqrt(2) - 1 $
    $ root(3, x) $

<div class="preview">

![Preview](/assets/609310fb74b9404b029e8b188a39ef2b.png)

</div>

</div>

## root

```
math.root(
    none content
    content
) -> content
```
A general root.


#### Parameters


#### index: none, content | _positional_

Which root of the radicand to take.


#### radicand: content | _required_ _positional_

The expression to take the root of.


### Example

<div class="previewed-code">

    $ root(3, x) $

<div class="preview">

![Preview](/assets/e5d701286528c37ac6ad4075120fe08f.png)

</div>

</div>


## sqrt

```
math.sqrt(
    content
) -> content
```
A square root.


#### Parameters


#### radicand: content | _required_ _positional_

The expression to take the square root of.


### Example

<div class="previewed-code">

    $ sqrt(3 - 2 sqrt(2)) = sqrt(2) - 1 $

<div class="preview">

![Preview](/assets/e6d87229d2ccd4badf9b9dc82c95aa69.png)

</div>

</div>

