---
icon: timer
tags:
  - data
  - api
---

# MeridiemTimeDelta

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Data/Time/MeridiemTimeDuration.cs" class="button secondary" data-icon="code">View on GitHub</a>

[meridiemtimedelta.md](meridiemtimedelta.md "mention") is COZY's structured duration type for representing elapsed time. Unlike [meridiemtime.md](meridiemtime.md "mention"), which represents a specific point on the clock, [meridiemtimedelta.md](meridiemtimedelta.md "mention") represents a length of time such as 2 hours, 45 minutes, or 30 seconds. Deltas can also exceed 24 hours in length leading to values above 1 when converted to a float.

## Overview

The [meridiemtimedelta.md](meridiemtimedelta.md "mention") struct is used whenever a system needs to represent a duration rather than an absolute time-of-day value. This makes it ideal for operations such as:

* skipping forward or backward in time
* applying a timed event window
* expressing animation, fade, or transition durations
* combining or subtracting time spans from a current time value

Because the type is structured and explicit, it avoids ambiguity between “a time of day” and “an amount of time” while still remaining easy to work with in code.

### Common Usage Examples

#### Create a 2-hour duration

```csharp
MeridiemTimeDelta delta = new MeridiemTimeDelta(2, 0);
```

#### Create a duration with seconds and milliseconds

```csharp
MeridiemTimeDelta delta = new MeridiemTimeDelta(1, 30, 15, 250);
```

#### Add a time delta to the current time

```csharp
timeModule.CurrentTime += new MeridiemTimeDelta(1, 0);
```

#### Skip time forward by a duration

```csharp
CozyWeather.Instance.Skip(new MeridiemTimeDelta(2, 0));
```

## API

### Properties

| Name            | Type                | Description                                              |
| --------------- | ------------------- | -------------------------------------------------------- |
| `hours`         | `int`               | The hour component of the duration.                      |
| `minutes`       | `int`               | The minute component of the duration.                    |
| `seconds`       | `int`               | The second component of the duration.                    |
| `milliseconds`  | `int`               | The millisecond component of the duration.               |
| `FloorToMinute` | `MeridiemTimeDelta` | Returns the duration rounded down to the nearest minute. |
| `FloorToHour`   | `MeridiemTimeDelta` | Returns the duration rounded down to the nearest hour.   |

### Functions / Methods

| Name         | Type     | Description                                                        |
| ------------ | -------- | ------------------------------------------------------------------ |
| `ToString()` | `string` | Returns the duration as a formatted string such as `02:30:00:000`. |

## Notes

* Use [meridiemtimedelta.md](meridiemtimedelta.md "mention") when you mean “how long” rather than “what time.”
* [meridiemtime.md](meridiemtime.md "mention") and [meridiemtimedelta.md](meridiemtimedelta.md "mention") are related but semantically different: one is a clock point, the other is a span of time.
* This type supports implicit conversions to and from `float` and `double`, making it convenient for percentage-based workflows and interpolation scenarios.
