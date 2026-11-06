---
icon: cloud-fog
---

# Fog FX

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Profiles/FX/FogFX.cs" class="button secondary" data-icon="code">View on GitHub</a>

`FogFX` is a parameter-based FX profile used to modulate fog density and fog height coverage. It is one of the most common weather-state effect layers because fog often needs to react dynamically to weather intensity.

## What it does

This profile updates the active world fog parameters via the current `FXParameters`:

- `fogCoverage`
- `fogHeightCoverage`

It can smoothly increase or decrease the fog during a weather transition, rather than forcing a hard cutoff.

## Typical use cases

### Dense weather states

Use this to make fog stronger during rain, mist, or night scenes.

### Controlled scene transitions

Blend fog in or out as the weather shifts between clear and stormy modes.

### Mood-driven atmospheric changes

Helpful for low-visibility scenes, valley haze, or haunted atmospheric conditions.

## Notes

- This is a parameter FX, so it alters the current fog provider rather than creating a new object.
- It is most useful when fog should respond to weather intensity or environmental transitions.
- It can be combined with Cloud FX and Filter FX to create a more layered mood.
