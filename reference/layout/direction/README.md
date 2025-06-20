
# Direction

The four directions into which content can be laid out.

Possible values are:

- `ltr`: Left to right.
- `rtl`: Right to left.
- `ttb`: Top to bottom.
- `btt`: Bottom to top.

These values are available globally and also in the direction type's
scope, so you can write either of the following two:

<div class="previewed-code">

    #stack(dir: rtl)[A][B][C]
    #stack(dir: direction.rtl)[A][B][C]

<div class="preview">

![Preview](/assets/e37ad93d1dfa28b65c7fc44b44b8d7d3.png)

</div>

</div>


## Definitions


### from

```
direction.from(
    alignment
) -> direction
```
Returns a direction from a starting point.


##### Parameters


##### side: alignment | _required_ _positional_




#### Example

<div class="previewed-code">

    direction.from(left) \
    direction.from(right) \
    direction.from(top) \
    direction.from(bottom)

<div class="preview">

![Preview](/assets/6bf3138749ebc5e6fb381c069448b8ec.png)

</div>

</div>


### to

```
direction.to(
    alignment
) -> direction
```
Returns a direction from an end point.


##### Parameters


##### side: alignment | _required_ _positional_




#### Example

<div class="previewed-code">

    direction.to(left) \
    direction.to(right) \
    direction.to(top) \
    direction.to(bottom)

<div class="preview">

![Preview](/assets/f8801e45272874c391ab2cfd9417cac1.png)

</div>

</div>


### axis

```
direction.axis(
) -> str
```
The axis this direction belongs to, either
<span class="typ-str">`"horizontal"`</span> or
<span class="typ-str">`"vertical"`</span>.


##### Parameters


#### Example

<div class="previewed-code">

    #ltr.axis() \
    #ttb.axis()

<div class="preview">

![Preview](/assets/26b36c48fb881b3e5df87cafa4a96644.png)

</div>

</div>


### sign

```
direction.sign(
) -> int
```
The corresponding sign, for use in calculations.


##### Parameters


#### Example

<div class="previewed-code">

    #ltr.sign() \
    #rtl.sign() \
    #ttb.sign() \
    #btt.sign()

<div class="preview">

![Preview](/assets/f96953c5545da5e408b9f96daa657aab.png)

</div>

</div>


### start

```
direction.start(
) -> alignment
```
The start point of this direction, as an alignment.


##### Parameters


#### Example

<div class="previewed-code">

    #ltr.start() \
    #rtl.start() \
    #ttb.start() \
    #btt.start()

<div class="preview">

![Preview](/assets/37d4500a4bb290d37816c260460d3a1a.png)

</div>

</div>


### end

```
direction.end(
) -> alignment
```
The end point of this direction, as an alignment.


##### Parameters


#### Example

<div class="previewed-code">

    #ltr.end() \
    #rtl.end() \
    #ttb.end() \
    #btt.end()

<div class="preview">

![Preview](/assets/3438dca5e28598aaa80867ab9a5c7574.png)

</div>

</div>


### inv

```
direction.inv(
) -> direction
```
The inverse direction.


##### Parameters


#### Example

<div class="previewed-code">

    #ltr.inv() \
    #rtl.inv() \
    #ttb.inv() \
    #btt.inv()

<div class="preview">

![Preview](/assets/9010ef0a4d8027d74f779654263c5c3a.png)

</div>

</div>

