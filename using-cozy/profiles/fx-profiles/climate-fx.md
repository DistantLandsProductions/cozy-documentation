---
icon: thermometer
---

# Climate FX

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Profiles/FX/ClimateFX.cs" class="button secondary" data-icon="code">View on GitHub</a>

`ClimateFX` is a parameter FX for applying short-lived climate offsets to the active simulation. It modifies values such as temperature, humidity, pressure, UV index, and air quality in a controlled way when a weather or ambience profile is active.

## What it does

The profile taps into the active `IClimateModule` and offsets the current climate values using `Overridable<T>` objects:

- `temperature`
- `humidity`
- `pressure`
- `uvIndex`
- `airQuality`

This is ideal for temporary climate states such as a hot dry gust, a cool evening front, or a dense air-pressure event.

## Typical use cases

### Temporary climate shifts

Apply a small increase in humidity or a drop in temperature during a foggy or rainy weather state.

### Event-based atmospheric changes

Use Climate FX to create short-lived environmental jolts without changing the underlying seasonal climate profile.

### Weather-specific microclimate tuning

A weather profile can layer a small climate offset onto the world so the state feels more physical and less static.

## Notes

- This is a high-level weather-state modifier rather than a direct physical effect.
- It works by altering the current climate module values, not by adding a visible actor to the world.
- Because it uses `Overridable<T>`, it can be conditional and profile-aware.
