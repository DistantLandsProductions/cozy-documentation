---
tags:
  - extension
  - module
  - atmosphere
  - api
---

# Eclipse

Eclipse is a COZY atmosphere extension that adds solar-eclipse-driven lighting and sky changes to your weather system. It can react to the real sky alignment of the sun and moon, or it can be driven manually to create dramatic story beats, cinematic events, or environmental scripting.

The module works as an atmosphere override layer: it does not replace the active COZY atmosphere, but instead blends configured atmosphere values toward a target state as eclipse strength rises from 0 to 1. This makes it useful for time-limited events, cinematic moments, and world-state transitions where the world briefly becomes darker, cooler, and more uncanny.

## What it does

At a high level, Eclipse does three things:

- Tracks whether the system is in a manual or automatic eclipse state.
- Calculates an `EclipseRatio` from the sun/moon relationship and the configured alignment threshold.
- Applies generated override values to atmosphere parameters, including sky, fog, lighting, clouds, and the sun/mood disk rendering.

This allows you to build scenes such as:

- a total eclipse in a fantasy or sci-fi world
- an eerie midday darkening with stronger shadows and lower ambient light
- special events triggered at a specific in-game date/time
- a cinematic “ring of fire” where the moon masks the sun but leaves a thin bright ring

## Typical use cases

### Story and world events

Use a manual eclipse to trigger a milestone, ritual, or major event. The profile can push the sky toward a dark, dramatic state while leaving all other weather logic intact.

### Realistic astronomical alignment

Set the module to `Automatic` and use the existing sun and moon direction data to calculate eclipse strength. The module can also estimate the next solar-eclipse peak with `TryPredictNextSolarEclipse`.

### Cinematic lighting control

Because Eclipse applies generated atmosphere overrides, you can tune sky gradients, fog density, cloud coverage, sun disk brightness, and ambient lighting without rewriting the weather system.

## Core API

### `EclipseModule`

```csharp
public class EclipseModule : CozyBiomeModule<EclipseModule>
```

Key members:

- `EclipseProfile Profile`
- `EclipseStyle Style`
- `float EclipseRatio`
- `float EclipseMoonSize`
- `bool TryPredictNextSolarEclipse(out SolarEclipsePrediction prediction, int maximumDaysToSearch = 365)`
- `override Type[] ModuleRequirements`

### `EclipseStyle`

```csharp
public enum EclipseStyle
{
    Manual,
    Automatic
}
```

Set `Manual` if you want to control eclipse strength directly. Set `Automatic` to let the module compute strength from the sun and moon alignment.

### `SolarEclipsePrediction`

```csharp
public struct SolarEclipsePrediction
{
    public MeridiemDate Date { get; }
    public MeridiemTime Time { get; }
    public float DaysUntil { get; }
    public float EclipseRatio { get; }
}
```

This result is returned by `TryPredictNextSolarEclipse` and gives you the predicted peak time and strength of the next alignment.

### `EclipseProfile`

```csharp
public class EclipseProfile : CozyProfile
```

- `List<EclipseOverride> overrides`
- `void ApplyToAtmosphere(AtmosphereParameters parameters, float weight)`

Eclipse profiles are collections of generated override objects. Each override toggles a specific atmosphere property, such as sky color, fog height, cloud density, or solar disk brightness.

### `EclipseOverride`

```csharp
public class EclipseOverride
```

The generated override classes derive from this base type and contain the specific values used when eclipse strength increases. Each override supports:

- `active`
- `FeatureEnabledGlobally`
- `ApplyToAtmosphere(AtmosphereParameters parameters, float weight)`

## Example usage

```csharp
var eclipse = weather.GetModule<EclipseModule>();
if (eclipse != null)
{
    eclipse.Style = EclipseModule.EclipseStyle.Manual;
    eclipse.EclipseRatio = 0.8f;
}
```

Or let the system compute it automatically:

```csharp
var eclipse = weather.GetModule<EclipseModule>();
if (eclipse != null)
{
    eclipse.Style = EclipseModule.EclipseStyle.Automatic;
    eclipse.TryPredictNextSolarEclipse(out var prediction);
}
```

## Notes

- The module requires a COZY atmosphere module and time module.
- It blends targeted atmosphere parameters instead of replacing the whole profile.
- `EclipseMoonSize` controls the rendered moon mask, allowing a thin ring effect when set below `1`.
- Overrides are generated from COZY's atmosphere variable definitions and can be regenerated when core atmosphere values change.
