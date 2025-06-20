
# Datetime

Represents a date, a time, or a combination of both.

Can be created by either specifying a custom datetime using this type's
constructor function or getting the current date with
[`datetime.today`](/reference/foundations/datetime/#definitions-today).

## Example

<div class="previewed-code">

    #let date = datetime(
      year: 2020,
      month: 10,
      day: 4,
    )

    #date.display() \
    #date.display(
      "y:[year repr:last_two]"
    )

    #let time = datetime(
      hour: 18,
      minute: 2,
      second: 23,
    )

    #time.display() \
    #time.display(
      "h:[hour repr:12][period]"
    )

<div class="preview">

![Preview](/assets/689464aa0d75be9b3106ad0dcea028d2.png)

</div>

</div>

## Datetime and Duration

You can get a [duration](/reference/foundations/duration/ "duration") by
subtracting two datetime:

<div class="previewed-code">

    #let first-of-march = datetime(day: 1, month: 3, year: 2024)
    #let first-of-jan = datetime(day: 1, month: 1, year: 2024)
    #let distance = first-of-march - first-of-jan
    #distance.hours()

<div class="preview">

![Preview](/assets/c4920f9ef579222c3ca2c76488051bfc.png)

</div>

</div>

You can also add/subtract a datetime and a duration to retrieve a new,
offset datetime:

<div class="previewed-code">

    #let date = datetime(day: 1, month: 3, year: 2024)
    #let two-days = duration(days: 2)
    #let two-days-earlier = date - two-days
    #let two-days-later = date + two-days

    #date.display() \
    #two-days-earlier.display() \
    #two-days-later.display()

<div class="preview">

![Preview](/assets/47e04f8fac503056ac0313359f787f8b.png)

</div>

</div>

## Format

You can specify a customized formatting using the
[`display`](/reference/foundations/datetime/#definitions-display)
method. The format of a datetime is specified by providing *components*
with a specified number of *modifiers*. A component represents a certain
part of the datetime that you want to display, and with the help of
modifiers you can define how you want to display that component. In
order to display a component, you wrap the name of the component in
square brackets (e.g. `[year]` will display the year). In order to add
modifiers, you add a space after the component name followed by the name
of the modifier, a colon and the value of the modifier (e.g.
`[month repr:short]` will display the short representation of the
month).

The possible combination of components and their respective modifiers is
as follows:

- `year`: Displays the year of the datetime.
  - `padding`: Can be either `zero`, `space` or `none`. Specifies how
    the year is padded.
  - `repr` Can be either `full` in which case the full year is displayed
    or `last_two` in which case only the last two digits are displayed.
  - `sign`: Can be either `automatic` or `mandatory`. Specifies when the
    sign should be displayed.
- `month`: Displays the month of the datetime.
  - `padding`: Can be either `zero`, `space` or `none`. Specifies how
    the month is padded.
  - `repr`: Can be either `numerical`, `long` or `short`. Specifies if
    the month should be displayed as a number or a word. Unfortunately,
    when choosing the word representation, it can currently only display
    the English version. In the future, it is planned to support
    localization.
- `day`: Displays the day of the datetime.
  - `padding`: Can be either `zero`, `space` or `none`. Specifies how
    the day is padded.
- `week_number`: Displays the week number of the datetime.
  - `padding`: Can be either `zero`, `space` or `none`. Specifies how
    the week number is padded.
  - `repr`: Can be either `ISO`, `sunday` or `monday`. In the case of
    `ISO`, week numbers are between 1 and 53, while the other ones are
    between 0 and 53.
- `weekday`: Displays the weekday of the date.
  - `repr` Can be either `long`, `short`, `sunday` or `monday`. In the
    case of `long` and `short`, the corresponding English name will be
    displayed (same as for the month, other languages are currently not
    supported). In the case of `sunday` and `monday`, the numerical
    value will be displayed (assuming Sunday and Monday as the first day
    of the week, respectively).
  - `one_indexed`: Can be either `true` or `false`. Defines whether the
    numerical representation of the week starts with 0 or 1.
- `hour`: Displays the hour of the date.
  - `padding`: Can be either `zero`, `space` or `none`. Specifies how
    the hour is padded.
  - `repr`: Can be either `24` or `12`. Changes whether the hour is
    displayed in the 24-hour or 12-hour format.
- `period`: The AM/PM part of the hour
  - `case`: Can be `lower` to display it in lower case and `upper` to
    display it in upper case.
- `minute`: Displays the minute of the date.
  - `padding`: Can be either `zero`, `space` or `none`. Specifies how
    the minute is padded.
- `second`: Displays the second of the date.
  - `padding`: Can be either `zero`, `space` or `none`. Specifies how
    the second is padded.

Keep in mind that not always all components can be used. For example, if
you create a new datetime with
<span class="typ-func">`datetime`</span><span class="typ-punct">`(`</span>`year`<span class="typ-punct">`:`</span>` `<span class="typ-num">`2023`</span><span class="typ-punct">`,`</span>` month`<span class="typ-punct">`:`</span>` `<span class="typ-num">`10`</span><span class="typ-punct">`,`</span>` day`<span class="typ-punct">`:`</span>` `<span class="typ-num">`13`</span><span class="typ-punct">`)`</span>,
it will be stored as a plain date internally, meaning that you cannot
use components such as `hour` or `minute`, which would only work on
datetimes that have a specified time.


## datetime

```
datetime(
    year: int
    month: int
    day: int
    hour: int
    minute: int
    second: int
) -> datetime
```
Creates a new datetime.

You can specify the
[datetime](/reference/foundations/datetime/ "datetime") using a year,
month, day, hour, minute, and second.

*Note*: Depending on which components of the datetime you specify, Typst
will store it in one of the following three ways:

- If you specify year, month and day, Typst will store just a date.
- If you specify hour, minute and second, Typst will store just a time.
- If you specify all of year, month, day, hour, minute and second, Typst
  will store a full datetime.

Depending on how it is stored, the
[`display`](/reference/foundations/datetime/#definitions-display) method
will choose a different formatting by default.


#### Parameters


#### year: int | _named_

The year of the datetime.


#### month: int | _named_

The month of the datetime.


#### day: int | _named_

The day of the datetime.


#### hour: int | _named_

The hour of the datetime.


#### minute: int | _named_

The minute of the datetime.


#### second: int | _named_

The second of the datetime.


### Example

<div class="previewed-code">

    #datetime(
      year: 2012,
      month: 8,
      day: 3,
    ).display()

<div class="preview">

![Preview](/assets/ea6a67351ca9372b235ef5ecb52a2e8b.png)

</div>

</div>


## Definitions


### today

```
datetime.today(
    offset: auto int
) -> datetime
```
Returns the current date.


##### Parameters


##### offset: auto, int | _named_

An offset to apply to the current UTC date. If set to
<span class="typ-key">`auto`</span>, the offset will be the local
offset.


#### Example

<div class="previewed-code">

    Today's date is
    #datetime.today().display().

<div class="preview">

![Preview](/assets/48e483281c9fcbf61b1db93b35e8e039.png)

</div>

</div>


### display

```
datetime.display(
    auto str
) -> str
```
Displays the datetime in a specified format.

Depending on whether you have defined just a date, a time or both, the
default format will be different. If you specified a date, it will be
`[year]-[month]-[day]`. If you specified a time, it will be
`[hour]:[minute]:[second]`. In the case of a datetime, it will be
`[year]-[month]-[day] [hour]:[minute]:[second]`.

See the [format syntax](/reference/foundations/datetime/#format) for
more information.


##### Parameters


##### pattern: auto, str | _positional_

The format used to display the datetime.


### year

```
datetime.year(
) -> none int
```
The year if it was specified, or <span class="typ-key">`none`</span> for
times without a date.


##### Parameters


### month

```
datetime.month(
) -> none int
```
The month if it was specified, or <span class="typ-key">`none`</span>
for times without a date.


##### Parameters


### weekday

```
datetime.weekday(
) -> none int
```
The weekday (counting Monday as 1) or
<span class="typ-key">`none`</span> for times without a date.


##### Parameters


### day

```
datetime.day(
) -> none int
```
The day if it was specified, or <span class="typ-key">`none`</span> for
times without a date.


##### Parameters


### hour

```
datetime.hour(
) -> none int
```
The hour if it was specified, or <span class="typ-key">`none`</span> for
dates without a time.


##### Parameters


### minute

```
datetime.minute(
) -> none int
```
The minute if it was specified, or <span class="typ-key">`none`</span>
for dates without a time.


##### Parameters


### second

```
datetime.second(
) -> none int
```
The second if it was specified, or <span class="typ-key">`none`</span>
for dates without a time.


##### Parameters


### ordinal

```
datetime.ordinal(
) -> none int
```
The ordinal (day of the year), or <span class="typ-key">`none`</span>
for times without a date.


##### Parameters

