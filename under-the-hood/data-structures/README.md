---
icon: database
---

# Data Structures

COZY relies on a small set of intentionally structured value types instead of raw floats and ad hoc dictionaries. These data structures are designed to make the weather, climate, time, and calendar systems easier to read, serialize, and react to in gameplay code.

This section focuses on the user-facing value types that most people will interact with when building scenes, profiles, or custom modules.

## Major types

### Time and calendar

- [Meridiem Architecture](meridiem-architecture/README.md) — the core time system for dates, clock times, durations, named day blocks, and scheduled events.
  - [MeridiemTime](meridiem-architecture/meridiemtime.md)
  - [MeridiemDate](meridiem-architecture/meridiemdate.md)
  - [MeridiemTimeDelta](meridiem-architecture/meridiemtimedelta.md)
  - [MeridiemBlock](meridiem-architecture/meridiemblock.md)
  - [MeridiemEvent](meridiem-architecture/meridiemevent.md)

### Climate and environment

- [Climate](climate/README.md) — the data layer for temperature, humidity, pressure, UV index, air quality, and seasonal ranges.
  - [Temperature](climate/temperature.md)
  - [Humidity](climate/humidity.md)
  - [Pressure](climate/pressure.md)
  - [Air Quality](climate/air-quality.md)
  - [UV Index](climate/uv-index.md)
  - [Precipitation Chance](climate/precipitation-chance.md)
  - [Season](climate/season.md)

## Why these matter

These types let COZY do several important things:

- distinguish a clock time from a duration
- represent dates and day-of-year values without float-based ambiguity
- manage seasonal climate ranges with smooth interpolation and variation curves
- keep code readable when building weather logic, transitions, state machine timing, and event scheduling

## Typical use cases

- query the current date or time of day
- determine whether a scene is in Dawn, Day, Twilight, or Night
- read current temperature or pressure values for gameplay rules
- build a deterministic weather cycle using seasonal ranges and climate snapshots
- schedule events or transitions using calendar-aware data types

These types are foundational to COZY’s runtime model, and they are the structures most custom scripts or integrations will likely read or manipulate.

