---
icon: clock
tags:
  - data
  - api
---

# MeridiemTime

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Data/Time/MeridiemTime.cs" class="button secondary" data-icon="code">View on GitHub</a>

The [meridiemtime.md](meridiemtime.md "mention") struct is COZY’s core clock value for representing a time of day. It stores a 12-hour-style time with AM/PM semantics, while internally converting that value into a normalized 24-hour timeline for comparisons, arithmetic, and formatting.

It is designed for use anywhere a scene needs to track a specific moment in the day, such as sunrise, noon, nightfall, event start times, or user-defined time-of-day values. It is also highly flexible and converts to a 0-1 float for easy conversion to the old time system.

## What MeridiemTime Represents

A [meridiemtime.md](meridiemtime.md "mention") contains:

* hours
* minutes
* seconds
* milliseconds
* meridiem (AM or PM)

## Key Features

#### Structured time values

[meridiemtime.md](meridiemtime.md "mention") can represent exact times such as:

* 6:00 AM
* 12:30 PM
* 11:59 PM

#### Automatic balancing

The struct safely normalizes values into a valid daily range. This makes it useful for operations that cross midnight or wrap around the 24-hour cycle.

#### Percentage conversion

A [meridiemtime.md](meridiemtime.md "mention") can be converted to a normalized daily percentage using `AsPercentage()`.

#### Formatting helpers

You can output the value in several forms:

* `StandardTime()` → e.g. `6:30 AM`
* `FullString()` → e.g. `6:30:15:000 AM`
* `MilitaryTime()` → e.g. `06:30`
* `FullMilitaryTime()` → e.g. `06:30:15:000`

## Example Usage

```csharp
MeridiemTime sunrise = new MeridiemTime(6, 30, Meridiem.AM);
MeridiemTime noon = MeridiemTime.Noon;

float timePercent = sunrise;
string display = sunrise.StandardTime();
```

## API

### Properties

<table><thead><tr><th width="183.6666259765625">Name</th><th width="157">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>hours</code></td><td><code>int</code></td><td>The hour component of the time, using 12-hour semantics.</td></tr><tr><td><code>minutes</code></td><td><code>int</code></td><td>The minute component of the time.</td></tr><tr><td><code>seconds</code></td><td><code>int</code></td><td>The second component of the time.</td></tr><tr><td><code>milliseconds</code></td><td><code>int</code></td><td>The millisecond component of the time.</td></tr><tr><td><code>meridiem</code></td><td><code>Meridiem</code></td><td>The AM/PM designation for the time.</td></tr><tr><td><code>AbsoluteHour</code></td><td><code>int</code></td><td>Converts the value to a 24-hour hour index, where <code>12 AM</code> is <code>0</code> and <code>12 PM</code> is <code>12</code>.</td></tr><tr><td><code>AsPercentage()</code></td><td><code>float</code></td><td>Returns the time as a normalized percentage of the full day, from <code>0</code> to <code>1</code>.</td></tr><tr><td><code>FloorToMinute</code></td><td><code>MeridiemTime</code></td><td>Returns a version of the current time rounded down to the nearest minute.</td></tr><tr><td><code>FloorToHour</code></td><td><code>MeridiemTime</code></td><td>Returns a version of the current time rounded down to the nearest hour.</td></tr></tbody></table>

### Functions / Methods

<table><thead><tr><th>Name</th><th width="210.3333740234375">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>From24Hour(int hour, int minute, int second = 0, int millisecond = 0)</code></td><td><code>static MeridiemTime</code></td><td>Creates a <code>MeridiemTime</code> from a 24-hour clock value.</td></tr><tr><td><code>ToClamped(float value)</code></td><td><code>static MeridiemTime</code></td><td>Converts a normalized day percentage into a clamped <code>MeridiemTime</code>.</td></tr><tr><td><code>StandardTime()</code></td><td><code>string</code></td><td>Returns the time in standard 12-hour format, such as <code>6:30 AM</code>.</td></tr><tr><td><code>FullString()</code></td><td><code>string</code></td><td>Returns the time in full detail, including seconds and milliseconds.</td></tr><tr><td><code>MilitaryTime()</code></td><td><code>string</code></td><td>Returns the time in 24-hour format, such as <code>06:30</code>.</td></tr><tr><td><code>FullMilitaryTime()</code></td><td><code>string</code></td><td>Returns the time in 24-hour format including seconds and milliseconds.</td></tr><tr><td><code>ToString()</code></td><td><code>string</code></td><td>Returns the time as a string using the current configured time display preference.</td></tr></tbody></table>

### Static Properties

<table><thead><tr><th width="122.33331298828125">Name</th><th width="196.66668701171875">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>Sunrise</code></td><td><code>MeridiemTime</code></td><td>The configured sunrise time, read from the transit system when available.</td></tr><tr><td><code>Sunset</code></td><td><code>MeridiemTime</code></td><td>The configured sunset time, read from the transit system when available.</td></tr><tr><td><code>Noon</code></td><td><code>MeridiemTime</code></td><td>A convenience value representing noon.</td></tr><tr><td><code>Midnight</code></td><td><code>MeridiemTime</code></td><td>A convenience value representing midnight.</td></tr><tr><td><code>SixPM</code></td><td><code>MeridiemTime</code></td><td>A convenience value representing <code>6:00 PM</code>.</td></tr><tr><td><code>SixAM</code></td><td><code>MeridiemTime</code></td><td>A convenience value representing <code>6:00 AM</code>.</td></tr></tbody></table>

## Notes

* [meridiemtime.md](meridiemtime.md "mention") should be used when you want to represent an actual time of day.
* [meridiemtimedelta.md](meridiemtimedelta.md "mention") should be used when you want to represent a duration of time.
* This struct supports implicit conversion to and from percentage-based values, which makes it convenient for time-based systems and UI code.
