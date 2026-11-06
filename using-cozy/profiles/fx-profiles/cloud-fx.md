---
icon: cloud
---

# Cloud FX

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Profiles/FX/CloudFX.cs" class="button secondary" data-icon="code">View on GitHub</a>

`CloudFX` changes the sky’s cloud coverage values in COZY. It is a parameter-based FX profile that adjusts cumulative cloud coverage over the active scene, allowing weather states to change cloud depth and layer density without hand-tweaking every material or sky setting.

## What it does

This FX modifies the active `FXParameters` values for cloud layers such as:

- cumulus coverage
- altocumulus coverage
- contrails
- cirrostratus
- cirrus
- border clouds
- cumulonimbus

It is most useful when a weather state should gradually add or reduce cloud coverage as part of a storm or clearing cycle.

## Typical use cases

### Storm fronts

Use a Cloud FX to increase cumulonimbus coverage and dense layered cloud bands during a thunderstorm or heavy rain state.

### Clear-sky transition

Fade cloud density down when moving from overcast to sunny weather so the sky opens up gradually.

### Layered weather mood

Rather than hard-coding cloud values into every weather profile, one Cloud FX can be reused across multiple profiles and states.

## Notes

- This profile is parameter-driven, not a scene object on its own.
- It depends on the `CozyWeather` instance and the active cloud system being enabled in the current style.
- It is most effective as part of a weather profile or ambience profile transition system.
