---
tags:
  - profile
---

# Weather Profile

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Profiles/WeatherProfile.cs" class="button secondary" data-icon="code">View on GitHub</a>

A weather profile describes one concrete weather state in COZY, such as clear skies, heavy rain, thunderstorm, fog, or snow. It packages the data needed to schedule a weather state, determine when it can occur, and trigger the associated FX when it is active.

## What it does

Weather profiles are the main runtime data used by the weather system. Each profile stores:

* a duration range (`MinTime` and `MaxTime`)
* a chance value used for random or weighted selection
* a weather tag (`WeatherTag`)
* optional restrictions for what can follow it in a forecast
* one or more FX profiles to play when the weather is active
* optional lateral weather shifts for dynamic condition-driven transitions

The profile is primarily a state definition: when the weather module selects it, the profile's FX and metadata become the active state for the scene.

## Typical use cases

### Configure a weather state

Create a separate weather profile for each distinct condition in your world: clear, overcast, rain, storm, snow, or fog-heavy conditions.

### Forecast and sequencing

Set `forecastNext` rules to decide which weather states may legitimately follow one another. This prevents impossible transitions and helps make the weather feel coherent.

### Attach FX to a weather state

Use the serialized FX list to synchronize particle systems, fog changes, precipitation, lighting, filters, or audio with the active state.

## Core API

```csharp
public class WeatherProfile : CozyProfile, IStateMachineProfile
```

Key members:

* `MeridiemTimeDelta MinTime`
* `MeridiemTimeDelta MaxTime`
* `float Chance`
* `WeatherTag Tag`
* `WeatherProfile[] forecastNext`
* `ForecastModifierMethod forecastModifierMethod`
* `float GetChance(ConditionSnapshot conditions)`
* `void Play(float weightVal)`

### `WeatherTag`

```csharp
[Flags]
public enum WeatherTag
{
    Sunny = 1,
    Cloudy = 2,
    Stormy = 4,
    Rainy = 8,
    Snowy = 16,
    Windy = 32,
    Fog = 64,
    Chain = 128,
}
```

This enum classifies the type of weather for comparisons, filtering, and forecasting logic.

### `WeatherChangeCondition`

The weather profile can participate in conditional lateral shifts through `WeatherChangeCondition` and `LateralWeatherShift`. These allow a profile to transition into another weather state when climate or time conditions match.

## Example usage

```csharp
WeatherProfile clearWeather = CozyWeather.Instance.Weather.CurrentProfile;

if (clearWeather != null)
{
    Debug.Log($"Current weather tag: {clearWeather.Tag}");
    Debug.Log($"Minimum duration: {clearWeather.MinTime}");
}
```

## Notes

* Weather profiles are state assets, not mutable runtime objects.
* A profile can play custom FX by attaching one or more `CozyFXProfile` assets.
* The `forecastNext` data and `ForecastProfile` work together to generate believable transitions.
