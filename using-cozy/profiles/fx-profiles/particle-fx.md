---
icon: sparkles
---

# Particle FX

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Profiles/FX/ParticleFX.cs" class="button secondary" data-icon="code">View on GitHub</a>

`ParticleFX` is the COZY particle-based effect profile for Unity’s legacy particle system (Shuriken). It creates and drives a runtime particle instance based on a prefab and plays it with a target weighting.

## What it does

The `ShurikenFX` implementation stores a `CozyShurikenInstance` prefab and a target layer. When the effect is active, it calls `instance.Play(weight)`, which drives the particle emission and weighting of the instantiated effect.

## Typical use cases

### Rain, snow, dust, and sparks

Use this to spawn particle-based weather or event effects that react to weather intensity.

### Temporary visual bursts

Use particle FX for localized bursts of dust, ash, smoke, or sparkle effects during a weather transition.

### Layered scene performance control

Because it creates a runtime instance, it can be reused and managed by COZY without storing all particles directly on the profile.

## Notes

- This is a reference FX: it maintains a runtime instance controlled by COZY.
- The actual effect is driven by the `CozyShurikenInstance` prefab.
- It is intended for particle-system-based effects rather than full render-feature or post-processing setups.
