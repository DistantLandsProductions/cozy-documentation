# Ambience Profile

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Profiles/AmbienceProfile.cs" class="button secondary" data-icon="code">View on GitHub</a>

An ambience profile defines a non-weather atmospheric state that can be played by the ambience system. It behaves similarly to a weather profile, but instead of directly representing precipitation or storm conditions, it represents an ambient mood or a looped atmospheric state such as calm night, eerie fog, or a quiet desert hush.

## What it does

Ambience profiles are used to create and transition between atmospheric states that are not strictly weather events. Each profile stores:

- a duration range (`MinTime` and `MaxTime`)
- a chance value for selection
- a list of weather profiles that it should not play during
- one or more FX profiles to apply while the ambience state is active

This makes ambience a reusable scene-state system that lives alongside weather rather than replacing it.

## Typical use cases

### Ambient mood states

Create ambience profiles for mood variations like quiet evening, dense fog, nightfall, or moody stillness.

### Avoiding conflicting events

Use `dontPlayDuring` to prevent an ambience from playing while a specific weather profile is active, keeping the scene coherent.

### Bridging gameplay and visuals

Ambience profiles can drive environmental FX without requiring serialization of every effect directly into gameplay code.

## Core API

```csharp
public class AmbienceProfile : CozyProfile, IStateMachineProfile
```

Key members:

- `MeridiemTimeDelta MinTime`
- `MeridiemTimeDelta MaxTime`
- `WeatherProfile[] dontPlayDuring`
- `WeightedRandomChance Chance`
- `float GetChance(CozyWeather weather)`
- `float GetChance(ConditionSnapshot condition)`
- `void Play(float weightVal)`

### `WeightedRandomChance`

This value controls how likely an ambience state is to be selected relative to other profiles in the same state machine.

## Example usage

```csharp
AmbienceProfile ambienceProfile = CozyWeather.Instance.Ambience.CurrentProfile;
if (ambienceProfile != null)
{
    Debug.Log($"Ambience chance: {ambienceProfile.GetChance(CozyWeather.Instance)}");
}
```

## Notes

- Ambience profiles often complement weather states rather than replacing them.
- They are useful for subtle environmental layers and gentle transitions.
- The `dontPlayDuring` list helps keep the scene from blending contradictory moods.

