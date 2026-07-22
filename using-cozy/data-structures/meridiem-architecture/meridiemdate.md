---
icon: calendar
tags:
  - data
  - api
---

# MeridiemDate

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Data/Time/MeridiemDate.cs" class="button secondary" data-icon="code">View on GitHub</a>

[meridiemdate.md](meridiemdate.md "mention") is COZY's structured calendar date type. It represents a date using a year, month, and day triplet and provides helpers for converting that date into absolute day values, checking weekdays, and normalizing date values across month/year boundaries.

## Overview

The [meridiemdate.md](meridiemdate.md "mention") struct is used anywhere COZY needs to represent a specific calendar date rather than a raw numeric day value. It is the date counterpart to [meridiemtime.md](meridiemtime.md "mention"), allowing the time system to track not only the current hour but also the current day, month, and year.

This type is especially useful for:

* tracking the current in-world date
* determining what day of the year a value represents
* comparing two dates
* converting dates to and from absolute day indices
* driving day-based calendars and event scheduling

{% hint style="info" %}
You can configure your year settings in the [preferences.md](../../preferences.md "mention") window. Year settings are global and shared across your entire project.
{% endhint %}

### Common Usage Examples

#### Create a dated value using month, day, and year

```csharp
MeridiemDate date = new MeridiemDate(4, 15, 2026);
```

#### Create a date from an absolute day index

```csharp
MeridiemDate date = new MeridiemDate(120);
```

#### Compare two dates

```csharp
if (dateA > dateB)
{
    Debug.Log("dateA is later than dateB");
}
```

#### Advance the date by 7 days

```csharp
MeridiemDate nextWeek = date + 7;
```

#### Get the current day of the year percentage

```csharp
float yearPercent = timeModule.CurrentDate.YearPercentage;
```

## API

### Properties

| Name                | Type           | Description                                                                              |
| ------------------- | -------------- | ---------------------------------------------------------------------------------------- |
| `year`              | `int`          | The year component of the date.                                                          |
| `month`             | `int`          | The month component of the date.                                                         |
| `day`               | `int`          | The day component of the date.                                                           |
| `AbsoluteDay`       | `int`          | Returns the date as an absolute day count from the start of the calendar system.         |
| `AbsoluteDayInYear` | `int`          | Returns the day index within the current year, counting from the start of the year.      |
| `Weekday`           | `DayOfWeek`    | Returns the weekday for the current date.                                                |
| `YearPercentage`    | `float`        | Returns the normalized percentage of the current year elapsed by the given date.         |
| `IsWeekend`         | `bool`         | Returns `true` when the date falls on Saturday or Sunday.                                |
| `DaysInMonth`       | `int`          | Returns the number of days in the current month.                                         |
| `MonthName`         | `string`       | Returns the localized or configured name of the current month.                           |
| `Yearless`          | `MeridiemDate` | Returns a date object that keeps the same month/day values but removes the year context. |

### Functions / Methods

| Name                 | Type           | Description                                                                                             |
| -------------------- | -------------- | ------------------------------------------------------------------------------------------------------- |
| `ToString()`         | `string`       | Returns the date in the configured display format (`MDY`, `DMY`, or `YMD`).                             |
| `ToBalanced()`       | `MeridiemDate` | Normalizes the date so that month and day values remain valid within the configured calendar structure. |
| `Equals(object obj)` | `bool`         | Compares this date to another object and returns whether they represent the same date.                  |
| `GetHashCode()`      | `int`          | Returns the hash code for the date.                                                                     |

### Static Properties

This type does not expose any public static properties.

### Operators

| Name                                  | Type           | Description                                                         |
| ------------------------------------- | -------------- | ------------------------------------------------------------------- |
| `operator <`                          | `bool`         | Compares two dates to determine whether one comes before the other. |
| `operator >`                          | `bool`         | Compares two dates to determine whether one comes after the other.  |
| `operator ==`                         | `bool`         | Compares two dates for equality.                                    |
| `operator !=`                         | `bool`         | Compares two dates for inequality.                                  |
| `operator -`                          | `int`          | Calculates the absolute difference between two dates.               |
| `operator +`                          | `MeridiemDate` | Advances a date by a given absolute day count.                      |
| `operator -`                          | `MeridiemDate` | Rewinds a date by a given absolute day count.                       |
| `implicit operator MeridiemDate(int)` | `MeridiemDate` | Converts an absolute-day integer into a `MeridiemDate`.             |
| `implicit operator int(MeridiemDate)` | `int`          | Converts a `MeridiemDate` into an absolute-day integer.             |

## Notes

* The date system is built to support structured calendar behavior across month/year boundaries and based on the configured COZY preferences.
* Configure your year settings in the [preferences.md](../../preferences.md "mention") window
