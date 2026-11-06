---
icon: cloud-drizzle
---

# Precipitation FX

<a href="https://github.com/DistantLandsProductions/com.distantlands.cozyweather.core/blob/main/Runtime/Profiles/FX/PrecipitationFX.cs" class="button secondary" data-icon="code">View on GitHub</a>

`PrecipitationFX` modifies precipitation accumulation behavior for the active precipitation module. It is used when a weather state should increase or reduce how quickly rain or snow accumulates in the world.

## What it does

This effect modifies two values on the active precipitation module:

- `RainAccumulationSpeed`
- `SnowAccumulationSpeed`

It also respects the maximum allowed rain or snow amount before continuing to increase accumulation.

## Typical use cases

### Rain events

Use this to increase the accumulation speed during a wet, stormy state.

### Snowy conditions

Slow or accelerate snow buildup to simulate the transition into a cold front or thaw.

### Layered weather results

This is a great complement to `CloudFX` and `FogFX` when you want the atmosphere and the precipitation to evolve together.

## Notes

- This profile is tied directly to the active precipitation module and value accumulation system.
- It is not a visual object by itself; it influences the behavior and buildup of precipitation in the simulation.
- It is ideal for states where precipitation should feel heavier or more persistent over time.
