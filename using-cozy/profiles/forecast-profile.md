---
tags:
  - profile
---

# Forecast Profile

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Profiles/ForecastProfile.cs" class="button secondary" data-icon="code">View on GitHub</a>

A forecast profile defines which weather states are allowed to appear next and under what conditions. It acts as the decision layer for the weather system, deciding whether a given weather profile can be scheduled after another and whether it should appear with a modified chance.

## What it does

The forecast profile stores a list of `ForecastableWeather` entries. Each entry describes:

* a weather profile
* the rules that determine when it can forecast next
* optional modifier rules such as forced inclusion, forced exclusion, or adjusted chance

This allows you to encode weather logic like:

* rain may only follow cloudy or stormy weather
* snow may be excluded during summer
* a storm profile may become much less likely on certain favorable days

## Typical use cases

### Controlled weather progression

Use a forecast profile to keep weather transitions coherent. For example, a desert scene may forecast a dust storm only after a dry, high-wind state rather than by random chance.

### Weighted transitions

A `ForecastNextModifierType` can change the probability of a given profile within a forecast step. This is useful for making a storm more or less likely depending on season or current conditions.

### Scenario-specific weather rules

If you want your region to experience seasonal or event-based weather flows, a forecast profile gives you a structured way to express those rules without a custom script for every branch.

## Core API

```csharp
public class ForecastProfile : CozyProfile, ISerializationCallbackReceiver
```

Key members:

* `List<ForecastableWeather> profiles`
* `int forecastAheadAmount`
* `HashSet<WeatherProfile> ForecastableWeatherProfiles`
* `WeatherProfile RandomWeatherProfile`
* `ForecastableWeather GetForecastingBehavior(WeatherProfile profile)`

### `ForecastableWeather`

```csharp
public struct ForecastableWeather
```

This struct encapsulates a weather profile and the set of `ForecastNext` rules that pertain to it.

### `ForecastNext`

```csharp
public struct ForecastNext
{
    public enum ForecastNextMethod
    {
        Any,
        ByTag,
        ByProfile
    }

    public enum ForecastNextModifierType
    {
        ForceInclude,
        ForceExclude,
        ModifiedChance
    }
}
```

The rules can target any profile, a specific tag, or a specific profile list. You can then either force a transition, block it, or scale its chance.

## Example usage

```csharp
ForecastProfile forecast = CozyWeather.Instance.Weather.ForecastProfile;
WeatherProfile next = forecast.RandomWeatherProfile;
```

You can also inspect a specific profile's forecast behavior:

```csharp
ForecastProfile.ForecastableWeather behavior = forecast.GetForecastingBehavior(rainProfile);
```

## Notes

* Forecast logic is more about viable transitions than immediate conditions.
* `ForecastProfile` is a higher-level rule set, while `WeatherProfile` is the actual state definition.
* The forecast can be used with random selection or weighted selection depending on your weather system configuration.
