---
icon: sliders
---

# Filter FX

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Profiles/FX/FilterFX.cs" class="button secondary" data-icon="code">View on GitHub</a>

`FilterFX` alters the filter and color grading settings used by COZY’s visual FX provider. It is a parameter FX for adjusting saturation, value, and color filters applied to the scene during a weather state.

## What it does

This FX modifies `FXParameters` values such as:

- `filterSaturation`
- `filterValue`
- `filterColor`
- `sunFilter`
- `cloudFilter`

It is typically used to add stylized color casts or cinematic filter layers when stormy or dreamlike weather states activate.

## Typical use cases

### Stylized weather color grading

A thunderstorm can push the scene toward a cool gray or blue filter, while a warm sunset state can give the filter a golden cast.

### Mood layering

Use filter adjustments to make a weather state feel more dramatic without changing the whole scene lighting setup.

### Post-processed scene style presets

This is a good way to add a layer of atmospheric stylization tied directly to weather.

## Notes

- This is not a scene object; it writes back to the active `FXParameters` provider.
- It is best used when you want a subtle, state-driven color treatment instead of a full custom render setup.
- It blends with the existing scene filters and can be combined with other FX.
