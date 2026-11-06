---
icon: wind
---

# Wind FX

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Profiles/FX/WindFX.cs" class="button secondary" data-icon="code">View on GitHub</a>

`WindFX` changes the active wind state of COZY. It is used when a weather or ambience profile should increase turbulence, direction, or gusting behavior without hard-coding wind values into the scene.

## What it does

This profile modifies the active `IWindModule` parameters, including:

- `windStrength`
- `windSpeed`
- `heading`
- `gustingPower`
- `gustingFrequency`

It can be used to make a weather state feel more turbulent, dynamic, or directional.

## Typical use cases

### Storm gusts

Use this to make a weather state feel physically dynamic with stronger gusting and a more intense wind field.

### Seasonal transitions

Blend the wind profile during a seasonal weather change without editing the underlying climate module directly.

### Spatially consistent atmosphere changes

Wind is often a key part of the mood of a weather state, so this FX helps keep it synchronized with the overall atmosphere.

## Notes

- This affects the wind system rather than generating a visible object.
- The effect is often paired with `CloudFX`, `FogFX`, or `PrecipitationFX` to create a fully weather-driven environment.
- It is best suited for states where wind is a major part of the scene mood.
