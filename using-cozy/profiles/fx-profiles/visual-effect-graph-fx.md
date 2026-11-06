---
icon: sparkles
---

# Visual Effect Graph FX

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Profiles/FX/VisualEffectGraphFX.cs" class="button secondary" data-icon="code">View on GitHub</a>

`VisualEffectGraphFX` is a reference FX for Unity Visual Effect Graph particle systems. It manages a runtime `CozyVFXInstance` and plays it at a given weight, making it suitable for atmospheric VFX such as fog wisps, embers, dust flurries, or lightning arcs.

## What it does

This profile stores a `CozyVFXInstance` prefab and a layer number. While the effect is enabled, it calls `instance.Play(weight, targetWeight)` to drive the runtime VFX instance according to the current effect intensity.

## Typical use cases

### Stylized storm effects

Trigger a VFX burst or continuous atmospheric effect during heavy weather or event states.

### Dynamic scene dust or embers

Use the effect to blend high-energy particles or volumetric bursts into the world while the profile is active.

### High-end visual effects without custom code

This profile is designed to slot into a weather or ambience profile directly rather than requiring custom runtime instantiation logic.

## Notes

- This is a reference FX for runtime effect instances.
- The weight is not just a binary toggle; it modulates the effect intensity across the active state.
- It is a strong fit for visually rich, layered weather transitions.
