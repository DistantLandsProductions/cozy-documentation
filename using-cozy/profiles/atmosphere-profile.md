# Atmosphere Profile

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Profiles/AtmosphereProfile.cs" class="button secondary" data-icon="code">View on GitHub</a>

An atmosphere profile is a container for atmospheric overrides used to shape the scene’s visual environment. Rather than describing a single weather state, it stores a structured set of atmosphere settings that can be applied as a whole and re-used across multiple weather states or transitions.

## What it does

The atmosphere profile holds a list of `AtmosphereOverride` entries. Each override maps to a specific atmospheric feature or visual parameter such as sky color, fog density, sun intensity, or other atmosphere-driven options exposed by COZY.

It is designed for modular scene control: a weather profile may choose a different atmosphere profile to produce a more dramatic night look, a brighter midday look, or a storm-heavy visual pass without rebuilding all scene settings by hand.

## Typical use cases

### Scene mood presets

Use an atmosphere profile to define distinct painterly looks for different states of the world, such as dawn, dusk, storm, or moody night.

### Weather layering

Atmosphere settings are often layered in combination with a weather profile and FX. The weather profile provides the active state, while the atmosphere profile supplies the visual baseline that that state sits on.

### Reusable visual templates

Because it is a ScriptableObject asset, an atmosphere profile can be reused across multiple scenes or weather transitions without duplicating material and lighting tweaks.

## Core API

```csharp
public class AtmosphereProfile : CozyProfile
```

Key members:

- `presetParameters`
- `List<AtmosphereOverride> overrides`
- `void OnValidate()`

`AtmosphereOverride` items are serialized through the `AtmosphereOverridesList` attribute, which exposes the override list in the inspector and lets the runtime rebuild the atmosphere model when the profile changes.

## Example usage

```csharp
AtmosphereProfile profile = CozyWeather.Instance.Atmosphere.Profile;
if (profile != null)
{
    // The module will update the atmospheric model based on this profile
    CozyWeather.Instance.Atmosphere.UpdateModel();
}
```

## Notes

- Atmosphere profiles are output-focused: they define how the environment should look.
- They work alongside weather profiles, not as a replacement for them.
- The profile can be updated at edit time and re-applied through the connected atmosphere module.

