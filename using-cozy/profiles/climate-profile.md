---
icon: thermometer
tags:
  - profile
  - climate
  - api
---

# Climate Profile

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Profiles/ClimateProfile.cs" class="button secondary" data-icon="code">View on GitHub</a>

A climate profile defines the seasonal envelope that COZY uses to generate realistic in-world conditions over the course of a year. It does not represent a single weather event; instead, it establishes the ranges and transitions for temperature, humidity, pressure, UV, and related climate variables across spring, summer, fall, and winter.

## What it does

The climate profile acts as the long-term baseline for the weather simulation. It stores four `Season` entries:

- `spring`
- `summer`
- `fall`
- `winter`

Each season contains a `ClimateRanges` payload with values for:

- temperature
- humidity
- pressure
- UV index
- precipitation chance and related climate data
- seasonal metadata

COZY then blends those ranges to produce the current climate state for the active date and time.

## Typical use cases

### Seasonal realism

Use a climate profile when you want a scene to feel like a temperate mountain valley, a dry desert, a temperate coastal zone, or a cold northern biome. The profile drives how temperatures and weather tendencies shift over the year.

### Long-range weather tuning

Weather profiles can decide the immediate condition, but climate determines the general environment that makes a weather state feel plausible. This is useful for making rain more likely in one season or very low UV in another.

### Procedural simulation

If you are constructing a world with no hard-coded weather calendar, the climate profile gives the system a stable yearly baseline that all other modules can read.

## Core API

```csharp
public class ClimateProfile : CozyProfile
```

Key members:

- `Season spring`
- `Season summer`
- `Season fall`
- `Season winter`
- `SeasonalTemperatureSmoothness temperatureSmoothness`
- `void GetClimateRanges(MeridiemDate date, out ClimateRanges climateRanges)`

### `SeasonalTemperatureSmoothness`

```csharp
public enum SeasonalTemperatureSmoothness
{
    Smooth,
    Steps
}
```

This enum chooses whether seasonal temperature transitions are blended smoothly or snap between seasonal bands.

### `GetClimateRanges(...)`

`GetClimateRanges` computes the current active climate ranges for a given date, using the season start days and the configured smoothness mode. This makes it easy for modules to sample realistic ongoing climate conditions without manually calculating season transitions.

## Example usage

```csharp
ClimateProfile climateProfile = CozyWeather.Instance.Climate.Profile;

if (climateProfile != null)
{
    climateProfile.GetClimateRanges(CozyWeather.Instance.Calendar.CurrentDate, out ClimateRanges ranges);
    Debug.Log($"Current seasonal temperature: {ranges.temperature.low} to {ranges.temperature.high}");
}
```

## Notes

- Climate profiles are global seasonal baselines rather than direct weather states.
- The active `WeatherProfile` can still override the scene mood, but the climate profile gives the system believable long-term behavior.
- `temperatureSmoothness` is especially useful when you want seasonal changes to feel natural instead of abrupt.
