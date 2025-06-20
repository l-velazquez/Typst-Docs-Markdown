
# Duration

Represents a positive or negative span of time.


## duration

```
duration(
    seconds: int
    minutes: int
    hours: int
    days: int
    weeks: int
) -> duration
```
Creates a new duration.

You can specify the
[duration](/reference/foundations/duration/ "duration") using weeks,
days, hours, minutes and seconds. You can also get a duration by
subtracting two [datetimes](/reference/foundations/datetime/).


#### Parameters


#### seconds: int | _named_

The number of seconds.


#### minutes: int | _named_

The number of minutes.


#### hours: int | _named_

The number of hours.


#### days: int | _named_

The number of days.


#### weeks: int | _named_

The number of weeks.


### Example

<div class="previewed-code">

    #duration(
      days: 3,
      hours: 12,
    ).hours()

<div class="preview">

![Preview](/assets/1a61bd24ab10644a9c59709ce7688889.png)

</div>

</div>


## Definitions


### seconds

```
duration.seconds(
) -> float
```
The duration expressed in seconds.

This function returns the total duration represented in seconds as a
floating-point number rather than the second component of the duration.


##### Parameters


### minutes

```
duration.minutes(
) -> float
```
The duration expressed in minutes.

This function returns the total duration represented in minutes as a
floating-point number rather than the second component of the duration.


##### Parameters


### hours

```
duration.hours(
) -> float
```
The duration expressed in hours.

This function returns the total duration represented in hours as a
floating-point number rather than the second component of the duration.


##### Parameters


### days

```
duration.days(
) -> float
```
The duration expressed in days.

This function returns the total duration represented in days as a
floating-point number rather than the second component of the duration.


##### Parameters


### weeks

```
duration.weeks(
) -> float
```
The duration expressed in weeks.

This function returns the total duration represented in weeks as a
floating-point number rather than the second component of the duration.


##### Parameters

