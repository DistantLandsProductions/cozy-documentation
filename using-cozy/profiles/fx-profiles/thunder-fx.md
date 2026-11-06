---
icon: bolt-lightning
---

# Thunder FX

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Profiles/FX/ThunderFX.cs" class="button secondary" data-icon="code">View on GitHub</a>

`ThunderFX` is a reference FX for weather-driven lightning events. It creates and drives a runtime thunder manager that can emit lightning flashes, thunder audio, and lighting intensity changes based on a stormy weather state.

## What it does

This FX is designed for storm scenarios and sets up a `CozyThunderManager` with values such as:

- `timeBetweenStrikes`
- `thunderPrefab`
- `thunderSounds`
- `sunLightDimming`
- `lightningLightIntensityCurve`
- `lightningLightIntensity`
- `thunderAudioDelay`

It then uses the active effect weight to drive lightning flashes, sound timing, and dramatic light pulses.

## Typical use cases

### Thunderstorms

Use `ThunderFX` on strong storm weather profiles to create lightning flashes, thunder rumbles, and sudden darkening light shifts.

### Event-driven dramatic weather

This is ideal for intense weather transitions where the sky should visibly react with flashes and sudden brightness changes.

### Ambient storm mood

Even without frequent strikes, a lighter thunder FX can add a sense of tension and environmental energy to a stormy state.

## Notes

- This is one of the more specialized reference FX profiles and is designed for heavy storm environments.
- It usually works best with `CloudFX`, `FogFX`, and `PrecipitationFX` for a full storm mood.
- It relies on runtime thunder-manager behavior rather than direct parameter changes.

